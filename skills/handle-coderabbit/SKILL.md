---
name: handle-coderabbit
description: Triage CodeRabbit PR review comments — verify each finding against the current code, apply valid fixes, and post reasoned replies to skipped comments via the `gh` CLI. Use when the user asks to "handle CodeRabbit comments", "address the CodeRabbit review", "answer CodeRabbit on the PR", or pastes CodeRabbit feedback and wants it triaged.
---

# Handle CodeRabbit review comments

CodeRabbit is a bot reviewer. Its findings are often real but sometimes wrong on details it can't verify (path resolution at runtime, GHA ephemerality, framework idioms, whether a test is actually broken vs. stylistically odd). Treat every finding as a hypothesis to verify against the current code, not a correction to apply blindly.

## Workflow

### 1. Identify the PR

If the user didn't give a PR number, find it from the current branch:

```bash
gh pr list --head $(git branch --show-current) --json number,url,title
```

### 2. Fetch the CodeRabbit comments

One comment = one finding. Save to a file because there can be many and the JSON is large.

```bash
gh api repos/{owner}/{repo}/pulls/{pr}/comments --paginate > /tmp/cr-comments.json
```

Filter to CodeRabbit's top-level findings, **excluding ones that already have a human reply** (those are handled):

```bash
python3 -c "
import json
data = json.load(open('/tmp/cr-comments.json'))
replied = {c['in_reply_to_id'] for c in data if c.get('in_reply_to_id')}
for c in data:
    if 'coderabbit' not in c.get('user', {}).get('login', '').lower():
        continue
    if c.get('in_reply_to_id'):           # skip reply-to-reply chatter
        continue
    if c['id'] in replied:                # skip findings already answered
        continue
    print(f\"id={c['id']} path={c.get('path')} line={c.get('line') or c.get('original_line')}\")
    print(c.get('body', '')[:300])
    print()
"
```

The `id` is what you need for replies. Write down path, line, and the ID together — you'll need all three per finding.

The REST API doesn't expose thread resolution state — if you need to skip findings the user has manually resolved in the GitHub UI, switch to the GraphQL `reviewThreads` query. For most workflows the already-replied filter is enough.

### 3. Verify each finding against current code

**This is the load-bearing step.** Don't trust CodeRabbit's reasoning — check.

For each comment, open the referenced file at the referenced line and reason about the claim. Common failure modes in CodeRabbit's analysis:

- **Path resolution**: it guesses `Path.parents[N]` values instead of tracing. Always compute by hand.
- **GHA / CI runner model**: it sometimes worries about stale state that can't exist on ephemeral runners.
- **Test "assumptions"** that aren't actually enforced anywhere in the suite.
- **Security hardening** on paths that YAML/framework already constrains.
- **"Not yet landed"** language flagged as stale when the PR itself is what's landing it.

Only when you've reproduced the concern in the code should you treat it as real.

### 4. Classify: apply, skip, or ask

- **Apply**: valid finding with a clear fix. Edit directly with the `Edit` tool. Do not batch — fix as you go so the state stays consistent.
- **Skip**: finding is wrong, redundant, or a style preference that doesn't match the codebase. Collect the reasoning; you'll reply to these.
- **Ambiguous**: something you can't decide without a design call (e.g. "should this validate JSONB shape?"). Surface to the user.

### 5. Confirm skips with the user before posting

Before posting any skip replies, list the skips with one-sentence reasoning each and get the user's confirmation. Format as:

```
Skipping N of M findings:
- {id} {path}:{line} — {one-sentence reason}
- ...
Proceed to post replies?
```

Wait for explicit confirmation. This is the only gate — once the user says yes, post all replies without asking again for each one (the confirmation covers the batch).

### 6. Post replies via `gh`

The reply endpoint is `POST /repos/{owner}/{repo}/pulls/{pr}/comments/{comment_id}/replies`. One call per skip:

```bash
gh api --method POST \
  repos/{owner}/{repo}/pulls/{pr}/comments/{comment_id}/replies \
  -f body="Skipping. {reason}. {verification detail if relevant}."
```

Reply text conventions:

- Open with "Skipping." so CodeRabbit's dashboard shows the disposition at a glance.
- Give the verification, not just the verdict. ("`parents[2]` from `/app/src/seeder.py` is `/`, not `/app`" beats "CodeRabbit is wrong".)
- If the reviewer might still want to act on the finding in a follow-up (JSONB validation, test renames), say so explicitly — don't close doors.

**Shell-quoting footgun**: `-f body="..."` uses double quotes, so `$foo` and `` `cmd` `` inside the reply get expanded by the shell before the HTTP call. For any body containing `$`, backticks, or backslashes, use a heredoc via `--field body=@-`:

```bash
gh api --method POST repos/OWNER/REPO/pulls/PR/comments/ID/replies --field body=@- <<'EOF'
Skipping. `Path(__file__).parents[2]` from `/app/src/seeder.py` is `/`, not `/app`.
EOF
```

The `<<'EOF'` (single-quoted delimiter) disables expansion inside the body.

If a reply fails with 422, the usual cause is the parent comment having been resolved — resolved threads reject replies. Fall back to a regular PR comment via `gh pr comment PR --body "..."`.

### 7. Verify applied fixes

If you applied any edits, run the relevant tests or type-check before declaring done. An applied fix that breaks the suite is worse than a skipped finding. For this repo: `cd backend && uv run pytest tests/<affected-area>` — integration tests need `TEST_DATABASE_URL` (see `backend/CLAUDE.md`).

### 8. Do not push

Never `git push` as part of handling CodeRabbit feedback. Applied fixes stay local until the user explicitly asks to push. The replies on GitHub are independent of local commits — they go up via the API regardless of branch state.

## What not to do

- Don't apply CodeRabbit's suggested `suggestion` diff blocks without reading them against context. The committable-suggestion UI makes them look authoritative; they aren't.
- Don't post replies to every comment, only to skips. Applied fixes speak for themselves in the next push — CodeRabbit will re-review.
- Don't argue tone. If a finding is half-right, say which half and what you'll do about it.
- Don't invent a "follow-up ticket" you won't file. If you punt something, punt it clearly in the reply text and in the user-facing summary.

## Quick reference

```bash
# Find PR for current branch
gh pr list --head $(git branch --show-current) --json number,url

# Fetch all review comments (paginated)
gh api repos/OWNER/REPO/pulls/PR/comments --paginate > /tmp/cr.json

# Post one reply
gh api --method POST \
  repos/OWNER/REPO/pulls/PR/comments/COMMENT_ID/replies \
  -f body="Skipping. <reason>."
```
