# Section Recipes — Reference

Technical reference sections. Diagram syntax lives in `diagram-templates.md`; this file
covers when to include a section and how to shape its content.

---

## Table of Contents

- [How It Works](#how-it-works)
- [API](#api)
- [Commands](#commands)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Requirements](#requirements)
- [SDK Matrix](#sdk-matrix)
- [Scenario Matrix](#scenario-matrix)
- [Packages](#packages)

---

## How It Works

**Purpose:** expand the mechanics — how the project runs, in order and in detail.

**Include when:** a flow, workflow or architecture can be derived from the source. This is
the concrete counterpart to Overview: Overview says what the project is and why it exists;
this section lays out the phases, the diagram and the parameters. Omit it when there is
nothing to add beyond the overview.

**Include when:** the scan can derive a diagram from the source — services, modules, classes,
tables or pipelines carrying real names.

### Diagram selection

| Project shape | Diagram | Source |
|---|---|---|
| Microservice / Frontend–Backend / Monolithic / Event-Driven | Architecture Graph | `diagram-templates.md` §1–4 |
| Library with class hierarchies | Class Diagram | §5 |
| Database-heavy | ER Diagram | §6 |
| CLI Tool / Data Pipeline | Flowchart | §7 |
| API Service | Sequence Diagram | §8 |
| Stateful workflow | State Diagram | §9 |

### Shape

```
## How It Works

<optional: one line, omit when the diagram already tells the story>

```mermaid
<diagram from diagram-templates.md, colors applied>
```

<optional: 2–4 bullets on the design decisions the diagram cannot show>
```

### Rules

1. **Real names only.** Component, class, table and method names must come from the source.
2. **Colors are mandatory.** Every diagram declares `classDef` and applies `class`. A
   colorless diagram fails gate G4.
3. **No `<details>` wrapper.** The diagram is a primary content element — it must be
   visible immediately.
4. **No "the following diagram illustrates…"** preamble. Label it and place it.
5. **Cap at 8 nodes.** Beyond that, group related components into a single node and
   explain the grouping in prose.
6. **Label nodes as `Name<br/>Technology`** so the reader knows the stack at a glance — Latin
   only. A CJK label stays one short line; two-line CJK text overflows the node box
   (`diagram-templates.md` → *Label Width*).
7. **Add a second diagram** only when the project has a genuinely different second view
   (e.g. Architecture Graph + ER Diagram for a database-heavy service). Never add a
   second diagram for decoration.
8. **Design-decision bullets** are the highest-value part. Explain *why* the boundary sits
   where it does — synchronous vs asynchronous, why storage is separated, what the
   consistency model is.

### Where the value lies

A reader can see the boxes in the repository. What they cannot see is the reasoning. Spend
the prose budget on constraints and trade-offs, not on restating the diagram.

---

## API

**Purpose:** let a consumer integrate without opening the source.

Include only when the scan detected routes, schema files, or exported service definitions.

### REST shape

```
## API

### Authentication

<one line: how to obtain and present credentials>

### <Resource group>

| Method | Path | Description | Auth |
|---|---|---|---|
| `GET` | `/users` | List users | Bearer |
| `POST` | `/users` | Create a user | Bearer |
| `GET` | `/users/:id` | Fetch one user | Bearer |
```

### GraphQL shape

```
| Operation | Type | Returns |
|---|---|---|
| `user(id: ID!)` | Query | `User` |
| `createUser(input: UserInput!)` | Mutation | `User` |
```

### gRPC shape

```
| Service | Method | Request | Response |
|---|---|---|---|
| `UserService` | `GetUser` | `GetUserRequest` | `User` |
```

### Rules

1. **Group by resource or module**, matching the source's routing structure.
2. **Read the paths from the source.** Never invent an endpoint or a parameter.
3. **Mark authentication per row.** A reader must know what needs a token.
4. **Note the base path or version prefix** if one exists.
5. **Cap the table.** Beyond ~15 endpoints, show the core resource and link to full
   reference docs.
6. **Document the error shape once** if the project has a consistent error envelope.
7. **Do not include internal endpoints** that the source does not expose.

---

## Commands

**Purpose:** the command reference for CLI tools.

**Include when:** a CLI entrypoint exists — `bin` in a manifest, a `cmd/` directory, a
`[[bin]]` target, or a `[project.scripts]` entry.

### Shape

```
## Commands

| Command | Description | Example |
|---|---|---|
| `init` | Scaffold a configuration file | `tool init --template minimal` |
| `run` | Execute the pipeline | `tool run ./input.json` |
| `validate` | Check a config without running | `tool validate config.yml` |

### Global flags

| Flag | Description | Default |
|---|---|---|
| `--config` | Config file path | `./tool.config.yml` |
| `--verbose` | Increase log detail | `false` |

### <Subcommand>

```bash
<real invocation with real output>
```
```

### Rules

1. **Every command must exist** in the CLI definition (`bin` target, argument parser,
   `cmd/` directory).
2. **Every flag must exist.** Do not document an aspiration.
3. **Show real output** for the primary subcommand — a reader needs to know what success
   looks like.
4. **Group flags** into global vs per-command.
5. **Include an exit-code table** when the tool uses codes programmatically.

---

## Project Structure

**Purpose:** orient a contributor in ten seconds.

**Include when:** more than one top-level source directory exists.

### Shape

```
## Project Structure

```
src/
├── api/              # HTTP route handlers
│   ├── users.ts      # User endpoints
│   └── posts.ts      # Post endpoints
├── services/         # Business logic
├── models/           # Database models
└── index.ts          # Entry point
```
```

### Rules

1. **Exclude** build output, dependencies and caches:
   `node_modules`, `.git`, `build`, `dist`, `out`, `target`, `__pycache__`, `.venv`,
   `.next`, `coverage`, `vendor`.
2. **Depth ≤ 3 levels.** Deeper detail belongs in the directory's own README.
3. **Comment every listed entry** with its responsibility, not its contents.
   - Good: `# HTTP route handlers` — Bad: `# contains .ts files`
4. **Mark the entry point** explicitly.
5. **Use the real tree characters** `├──`, `│`, `└──`.
6. **Include key root files** (manifests, Dockerfile, compose file) when they matter to a
   contributor.
7. **For a workspace**, additionally show which directories are packages and which are apps.
8. **Cap the listing at ~20 entries.** Beyond that, show top-level only and link a
   per-package README.

---

## Tech Stack

**Purpose:** let a reader assess fit and familiarity at a glance.

**Include when:** dependencies are declared in a manifest.

### Shape

```
## Tech Stack

### Frontend
| Technology | Purpose |
|---|---|
| React 18 | UI framework |
| Zustand | Client state |

### Backend
| Technology | Purpose |
|---|---|
| Express | HTTP server |
| Prisma | Data access |

### Infrastructure
| Technology | Purpose |
|---|---|
| PostgreSQL | Primary datastore |
| Redis | Session store, pub/sub |
| Docker | Packaging |
```

### Rules

1. **Group by layer**: Frontend / Backend / Data / Infrastructure / Testing.
2. **Only include what is actually used.** Exclude transitive and unused dev dependencies.
3. **Include test and lint frameworks** when they are part of the contributor workflow.
4. **Use the product name, not the package string.** `Vue 3`, not `vue@^3.4.0`.
5. **No "Other Tools" bucket.** If a technology does not fit a layer, it does not belong.
6. **Do not duplicate the Features section.** This section answers "what is it built
   with", not "what does it do".
7. Cross-reference names against `badges.md` so the same vocabulary is used in the badge
   matrix.
8. **Prefer a list to a two-column table.** `- **Technology** — purpose` reads better than
   a Technology/Purpose table unless a layer carries several comparable columns
   (`writing-style.md` → *Tables*).

---

## Requirements

**Purpose:** answer "will this run on my machine" before installation.

Include when the scan found declared runtime, browser, OS or platform requirements.

### Shape

```
## Requirements

| Runtime | Supported |
|---|---|
| Node.js | 18, 20, 22 |
| Browsers | Latest two versions of Chrome, Firefox, Safari, Edge |
| Platforms | Linux, macOS, Windows |
```

For UI libraries, a browser icon row is readable:

```
| Chrome | Firefox | Safari | Edge |
| :-: | :-: | :-: | :-: |
| last 2 | last 2 | last 2 | last 2 |
```

### Rules

1. **Declared values only.** Read from `engines`, `browserslist`, CI matrix, or build
   targets. Never guess a version.
2. **When no version is declared**, state the tested range if CI proves it, otherwise omit
   the section.
3. **Icon rows must carry text alternatives** — an icon-only row fails gate G6 when the
   icon has no accessible label.
4. **Note server-side rendering or platform caveats** when the source shows them.
5. **With only a few entries, use a list.** A Runtime/Support table is warranted only when
   several rows share comparable values; otherwise `- **Runtime** — 18, 20, 22` reads
   better (`writing-style.md` → *Tables*).

---

## SDK Matrix

**Purpose:** for infrastructure projects that ship clients in several languages.

**Include when:** multiple client packages exist, each targeting a different language.

### Shape

```
## SDKs

| Language | Package | Status |
|---|---|---|
| Python | `project-python` | Stable |
| Go | `project-go/v2` | Stable |
| Java | `project-java` | Stable |
| Node.js | `project-node` | Beta |
| Rust | `project-rs` | Preview |
```

### Rules

1. **Read package names from the repository.** SDK folders or a monorepo packages table
   are the source.
2. **State status accurately** — Stable / Beta / Preview / Deprecated. Do not label a
   preview client stable.
3. **Link each package** to its registry or its directory.
4. **Add a community-clients row** separately when third-party clients exist, so they are
   not confused with official ones.
5. **Include a REST/gRPC fallback row** when the server exposes a protocol for languages
   without a client library.

---

## Scenario Matrix

**Purpose:** connect business use cases to the technical primitives that serve them.

**Include when:** the project documents scenarios that map to specific primitives or guides.

### Shape

```
## Scenarios

| Scenario | Tutorial | Primitives used |
|---|---|---|
| Retrieval-augmented generation | [Guide](link) | Dense vectors, metadata filter |
| Hybrid search | [Guide](link) | Dense + sparse vectors, reranking |
| Visual similarity | [Guide](link) | Multi-vector, hardware acceleration |
```

### Rules

1. **Only list scenarios the project documents.** This table is an index, not a wish list.
2. **Tutorial links must resolve** (gate G5). If no tutorial exists, drop the row.
3. **Name the primitives precisely** using the project's own vocabulary.
4. Prefer this table over prose — it answers "can it do my thing" faster than paragraphs.

---

## Packages

**Purpose:** the package inventory for a monorepo.

**Include when:** the workspace configuration declares multiple packages.

### Shape

```
## Packages

| Package | Purpose | Version |
|---|---|---|
| `@scope/core` | Runtime primitives | 1.4.0 |
| `@scope/react` | React bindings | 1.4.0 |
| `@scope/cli` | Command-line interface | 1.2.1 |
| `apps/docs` | Documentation site | — |
```

### Rules

1. **Read the list from the workspace configuration**, not from the filesystem alone.
2. **Distinguish packages from apps** — label or separate them.
3. **State per-package status** when they are not released together (private, experimental).
4. **Note license variance** when packages differ from the root license.
5. **Link each package** to its directory or registry page.
