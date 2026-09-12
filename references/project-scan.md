# Project Scan

Detection rules and evidence-map format for Phase 1.

> Read static files only. Never execute, modify or delete project files. Never run `git`
> or any other state-changing command.

---

## Table of Contents

- [Evidence Map](#evidence-map)
- [Detector Precedence](#detector-precedence)
- [Detectors](#detectors)
- [Manifest Reference](#manifest-reference)

---

## Evidence Map

The evidence map is the contract between Phase 1 and Phase 2. Phase 3 gate G1 verifies
that every claim in the README has a row here.

### Format

```
EVIDENCE MAP — <project name>
────────────────────────────────────────────────────────────────
claim                          level      source
────────────────────────────────────────────────────────────────
Language = TypeScript          declared   package.json → devDependencies.typescript
Framework = Express            declared   package.json → dependencies.express
Database = PostgreSQL          declared   package.json → dependencies.pg
ORM = Prisma                   declared   package.json → dependencies.@prisma/client
Default port = 3000            declared   src/config.ts:14
Node >= 18                     declared   package.json → engines.node
Build = npm run build          declared   package.json → scripts.build
Dev = npm run dev              declared   package.json → scripts.dev
CI = GitHub Actions            declared   .github/workflows/ci.yml
Docker = yes                   declared   Dockerfile, docker-compose.yml
License = Apache-2.0           declared   LICENSE:1
Contributors = 3               declared   CONTRIBUTORS
Architecture = layered         inferred   src/{api,services,models}/ present
Test framework = Vitest        declared   package.json → devDependencies.vitest
────────────────────────────────────────────────────────────────
```

### Rules

1. Every row needs a `source` that a human could open and verify. Line numbers where
   useful.
2. `declared` rows may be stated as fact in the README.
3. `inferred` rows must be softened ("appears to", "primarily", "suggests").
4. A claim with no row cannot be written. This is gate G1.
5. Do not invent a source. `package.json` without a `scripts.dev` key does not yield a
   dev command.

---

## Detector Precedence

Resolve conflicts in this order — earlier wins:

1. **Manifest parsing** — `package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`,
   `Gemfile`, `pom.xml`, `build.gradle`, `composer.json`, `*.csproj`
2. **Explicit dependency declarations** — `dependencies` / `devDependencies` / equivalent
3. **File-extension majority** — fallback only
4. **Filename heuristics** — last resort

If two manifests at different roots declare different languages, prompt the user to choose
the package root. Default precedence when they decline:
`package.json > pyproject.toml > go.mod > Cargo.toml > pom.xml > Gemfile`.

---

## Detectors

### 1. Language

| Source | Signal |
|---|---|
| `package.json` + `tsconfig.json` | TypeScript |
| `package.json` only | JavaScript |
| `pyproject.toml`, `requirements.txt`, `setup.py` | Python |
| `go.mod` | Go |
| `Cargo.toml` | Rust |
| `pom.xml`, `build.gradle` | Java / Kotlin |
| `Gemfile` | Ruby |
| `composer.json` | PHP |
| `*.csproj`, `*.sln` | C# |
| `mix.exs` | Elixir |

Read the declared runtime version from `engines`, `.python-version`, `.tool-versions`,
`.nvmrc`, `rust-toolchain.toml`. Version claims require `declared` evidence.

### 2. Framework

Parse the dependency block and match against `references/badges.md`. Use the framework
tables there as the canonical name list so the badge lookup always resolves.

### 3. Build & CI

| File | Yields |
|---|---|
| `Makefile` | Make targets |
| `CMakeLists.txt` | CMake build |
| `package.json#scripts` | Node scripts |
| `pyproject.toml#[tool.poetry.scripts]`, `[project.scripts]` | Python entrypoints |
| `Dockerfile`, `docker-compose.yml`, `compose.yaml` | Container workflow |
| `.github/workflows/*.yml` | GitHub Actions |
| `.gitlab-ci.yml` | GitLab CI |
| `Jenkinsfile` | Jenkins |
| `.circleci/config.yml` | CircleCI |

### 4. Database & ORM

| Signal | Meaning |
|---|---|
| `DATABASE_URL`, `DB_HOST`, `POSTGRES_*` in `.env.example` | Database present; read the scheme |
| `pg`, `psycopg2`, `asyncpg`, `postgres` driver | PostgreSQL |
| `mysql2`, `PyMySQL`, `mysql-connector` | MySQL |
| `mongoose`, `pymongo` | MongoDB |
| `ioredis`, `redis` | Redis |
| `prisma`, `typeorm`, `sequelize`, `sqlalchemy`, `gorm`, `activerecord` | ORM |
| `prisma/schema.prisma`, `alembic/`, `migrations/` | Migration tooling |

### 5. Architecture

| Signal | Classification |
|---|---|
| Multiple service folders + `.proto` / RPC clients | Microservice |
| `client/` + `server/`, or `frontend/` + `backend/` | Frontend–Backend Split |
| `controllers/` + `services/` + `models/` | Monolithic Layered |
| Kafka / RabbitMQ / NATS / SQS dependency | Event-Driven |
| `packages/` + `workspaces` field | Monorepo |

### 6. API Style

| Signal | Style |
|---|---|
| Route files (`routes/`, `api/`, controllers with decorators) | REST |
| `*.proto` + generated stubs | gRPC |
| `*.graphql`, `schema.graphql`, resolvers | GraphQL |
| `socket.io`, `ws`, WebSocket server setup | WebSocket |
| `trpc` dependency | tRPC |

### 7. License

Read the root `LICENSE` / `LICENSE.md` / `COPYING` and identify:
MIT, Apache-2.0, GPL-2.0/3.0, AGPL-3.0, LGPL, BSD-2/3-Clause, ISC, MPL-2.0,
Unlicense, CC0, Elastic-2.0.

| Situation | Behaviour |
|---|---|
| Single license file | State it, link it |
| No license file | Omit the section; add one line: `No LICENSE file detected. Add a LICENSE to clarify project licensing.` |
| Multiple conflicting files | List them and ask the user which applies |

### 8. Project Type

| Signal | Type |
|---|---|
| `publishConfig`, `files` field, no start script | Library |
| `dev` / `start` scripts, not published | Application |
| `bin` field, `cmd/` directory, single executable | CLI Tool |
| Component exports + Storybook + no server | UI Library |
| Frontend-only, no backend | Static Site / Demo |

### 9. Config Files

Scan the root and `config/`, `configs/`, `.config/` for `.env`, `.env.example`,
`*.config.{js,ts,mjs,cjs}`, `*.{yml,yaml}`, `*.toml`, `*.ini`.

Extract variable names only. Never copy values that look like credentials.

### 10. Git & Contributors

- Do **not** execute `git`.
- If `.git` or a static file (`CONTRIBUTORS`, `AUTHORS`, `MAINTAINERS`) is readable,
  extract names only — never emails.
- Commit conventions may be read only from static config
  (`.github/commit-convention.md`, `commitlint.config.*`, `CONTRIBUTING.md`).
- If unavailable, skip contributor detection and note:
  `Contributor history unavailable (no git metadata access).`

### 11. Documentation Corpus

Detect whether the project is documentation-heavy, which switches the archetype to
Knowledge Base:

| Signal | Meaning |
|---|---|
| >20 Markdown files, no build system | Knowledge Base |
| `docs/<locale>/` directories | Multilingual docs |
| `SUMMARY.md` / `mkdocs.yml` / `docusaurus.config.*` | Docs site |
| Large single README (>800 lines) | Needs the TOC funnel treatment |

### 12. Security & Governance Signals

| File | Enables section |
|---|---|
| `SECURITY.md`, `.github/SECURITY.md` | Security |
| `CODE_OF_CONDUCT.md` | Code of Conduct reference in Contributing |
| `CITATION.cff`, `@article` in README | Citation |
| `CHANGELOG.md`, releases automation | Changelog |
| `.github/FUNDING.yml`, `SPONSORS.md` | Sponsors |
| `ROADMAP.md`, milestone config | Roadmap |
| `docs/FAQ.md`, repeated issue themes | FAQ |

---

## Manifest Reference

### `package.json`

| Field | Evidence extracted |
|---|---|
| `name`, `description` | Project identity |
| `version` | Version |
| `dependencies` / `devDependencies` | Framework, database, tooling |
| `scripts` | Build, dev, test, lint commands |
| `engines` | Runtime version requirement |
| `bin` | CLI entrypoint |
| `workspaces` | Monorepo roots |
| `packageManager` | npm / pnpm / yarn / bun |
| `publishConfig` | Library vs application |

### `pyproject.toml`

| Field | Evidence extracted |
|---|---|
| `[project] name`, `description`, `version` | Identity |
| `[project] dependencies` | Runtime stack |
| `[project.optional-dependencies]` | Extras (document as install variants) |
| `[project.scripts]` | CLI entrypoints |
| `requires-python` | Python version |
| `[tool.poetry]`, `[tool.uv]` | Build backend |

### `go.mod`

| Field | Evidence extracted |
|---|---|
| `module` | Import path |
| `go` | Go version |
| `require` block | Framework and libraries |

### `Cargo.toml`

| Field | Evidence extracted |
|---|---|
| `[package] name`, `description`, `version` | Identity |
| `edition`, `rust-version` | Toolchain |
| `[dependencies]` | Stack |
| `[[bin]]` | CLI targets |

---

## Scan Output Template

```
SCAN SUMMARY — <project>
─────────────────────────────────────
Archetype        : <one of 8>
Maturity tier    : T1 | T2 | T3
Language         : <declared>
Framework        : <declared, comma-separated>
Database / ORM   : <declared>
Build / CI       : <declared>
Architecture     : <inferred>
API style        : <declared or inferred>
License          : <declared>
Project type     : <declared>
Config files     : <count> (<names>)
Docs corpus      : <light | standard | heavy>
Governance files : <SECURITY.md, CODE_OF_CONDUCT.md, ...>
Evidence rows    : <count>
─────────────────────────────────────
```
