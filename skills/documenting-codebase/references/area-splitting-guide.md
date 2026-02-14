# How to Split a Codebase into Areas

## Principle

Split by **domain boundaries**, not by file type or framework layer. Each area should answer "what does this part of the system _do_?" not "what kind of files are these?"

## Common Area Patterns by Stack Type

### Full-Stack Web App (React/Vue/Angular + API)

| #   | Area                  | Covers                                                        |
| --- | --------------------- | ------------------------------------------------------------- |
| 01  | Product & Domain      | Glossary, user roles, business rules, domain model            |
| 02  | Frontend Architecture | App shell, routing, auth flow, state management, UI library   |
| 03  | Database & Data Model | Schema, tables, relationships, migrations, access control     |
| 04  | API Layer             | Endpoints, auth, error handling, middleware, shared modules   |
| 05  | [Core Feature A]      | The primary thing the app does (e.g., chat, editor, pipeline) |
| 06  | [Core Feature B]      | Second major feature (e.g., scoring, analytics, search)       |
| 07  | [Data/Content System] | How content is managed (CMS, RAG, file storage)               |
| 08  | [User-Facing Flow]    | End-to-end UX for the main user journey                       |
| 09  | [Config/Integration]  | Third-party integrations, configuration management            |
| 10  | Admin & Operations    | Dashboards, monitoring, feature flags, deployment             |

### Backend API / Microservices

| #     | Area                | Covers                                          |
| ----- | ------------------- | ----------------------------------------------- |
| 01    | Domain Model        | Entities, value objects, business rules         |
| 02    | API Surface         | Routes, controllers, request/response contracts |
| 03    | Data Layer          | Database, ORM, migrations, repositories         |
| 04    | Auth & Security     | Authentication, authorization, RBAC, encryption |
| 05-08 | [Service Domains]   | One area per bounded context or service         |
| 09    | Infrastructure      | Message queues, caching, external APIs          |
| 10    | Ops & Observability | Logging, metrics, health checks, deployment     |

### CLI Tool / Library

| #     | Area                    | Covers                                    |
| ----- | ----------------------- | ----------------------------------------- |
| 01    | Overview & Design       | Purpose, architecture, key abstractions   |
| 02    | Command Interface       | CLI args, subcommands, config file format |
| 03    | Core Engine             | Main processing logic                     |
| 04-06 | [Feature Modules]       | One per major capability                  |
| 07    | Plugin/Extension System | If applicable                             |
| 08    | Testing & CI            | Test strategy, fixtures, CI pipeline      |

### Mobile App (Flutter/React Native/Swift)

| #     | Area                 | Covers                                             |
| ----- | -------------------- | -------------------------------------------------- |
| 01    | Product & Domain     | Features, user roles, business logic               |
| 02    | App Architecture     | Navigation, state management, dependency injection |
| 03    | Data Layer           | Local DB, API client, caching, sync                |
| 04    | Auth & Security      | Login flow, token management, biometrics           |
| 05-08 | [Feature Screens]    | One per major screen/flow                          |
| 09    | Platform Integration | Push notifications, deep links, native modules     |
| 10    | Build & Distribution | Flavors, signing, CI/CD, app store                 |

## How to Identify Areas

1. **List the nouns** in the app (users, orders, products, messages, scores)
2. **Group by lifecycle** -- things that are created/updated/consumed together
3. **Check coupling** -- if changing area A always requires changing area B, merge them
4. **Check size** -- if an area has 50+ files, consider splitting
5. **Check clarity** -- can you explain the area's purpose in one sentence?

## Area Size Guidelines

| Files in Area | Verdict                                |
| ------------- | -------------------------------------- |
| < 5           | Too small -- merge with a related area |
| 5-30          | Good size                              |
| 30-50         | Acceptable if cohesive                 |
| > 50          | Consider splitting                     |

## Anti-Patterns

- **"Components" area**: Too broad. Split by what the components _do_.
- **"Utils" area**: Distribute utils into the areas that use them.
- **"Types" area**: Types belong with the code they describe.
- **"Tests" area**: Tests belong with the code they test.
- **One area per file**: Too granular. Group by domain.
