# Archetype Profiles

Phase 0 resolves one archetype and one maturity tier. Together they determine which
sections are written, in what order, with what emphasis.

---

## Table of Contents

- [Maturity Tiers](#maturity-tiers)
- [Archetype Index](#archetype-index)
- [1. Library](#1-library)
- [2. Application](#2-application)
- [3. CLI Tool](#3-cli-tool)
- [4. UI Library](#4-ui-library)
- [5. AI App](#5-ai-app)
- [6. Knowledge Base](#6-knowledge-base)
- [7. Infrastructure](#7-infrastructure)
- [8. Monorepo](#8-monorepo)

---

## Maturity Tiers

Tier controls the section budget and which growth sections are enabled. Resolve the tier
before composing — it caps how much the README should contain.

| Tier | Signals (any two) | Section budget | Growth sections | Badge budget | Diagrams |
|---|---|---|---|---|---|
| **T1 Personal** | No CI · single author · no CONTRIBUTING · <500 stars | ≤ 7 | Contributing, License only | ≤ 5 | 1 |
| **T2 Community** | CI workflow · CONTRIBUTING.md · issue templates · 500–10k stars | ≤ 11 | + Community, Roadmap, Changelog | ≤ 12 | 1–2 |
| **T3 Flagship** | Release automation · docs site · multiple maintainers · >10k stars · sponsors | ≤ 16 | all | full matrix | 1–3 |

### Tier Rules

- Never exceed the budget. Drop the lowest-value optional sections instead.
- Tier is a ceiling, not a target. A T3 project with no sponsors writes no sponsor section.
- If the user requests a section the tier disables, honour the request and note the tier
  override in the report.
- When star data is unavailable, infer from static files and state the inference.

---

## Archetype Index

| Archetype | Primary diagram | Default tone | Onboarding style |
|---|---|---|---|
| Library | Class Diagram | Minimal | Single-line install + snippet |
| Application | Architecture Graph | Professional | Docker Compose in 4 lines |
| CLI Tool | Flowchart | Minimal | Multi-package-manager blocks |
| UI Library | Component tree / Architecture Graph | Energetic | Install + live playground link |
| AI App | Pipeline Flowchart | Energetic | Hardware gate + env isolation |
| Knowledge Base | Concept map / Flowchart | Academic | Learning-path TOC |
| Infrastructure | Topology Graph | Professional | Lite → Standalone → Cluster ladder |
| Monorepo | Package Graph | Professional | Single workspace command |

---

## 1. Library

A published package consumed by other code. No runtime of its own.

**Detection:** `publishConfig`, `files` field, `[project]` in `pyproject.toml` with no
entrypoint, no `dev`/`start` script, no Dockerfile.

### Section set

| Order | Section | Level | Notes |
|---|---|---|---|
| 1 | Hero | required | Lead with install command as a CTA |
| 2 | Features | required | 3–6, framed as capabilities not adjectives |
| 3 | Quick Start | required | Install + minimal usage in one block |
| 4 | Usage | required | 2–4 real examples from tests or examples/ |
| 5 | API | required | Public surface only |
| 6 | Compatibility | required if declared | Runtime/OS/browser matrix |
| 7 | Configuration | optional | Only if options exist |
| 8 | Architecture | recommended | Class diagram for OOP-heavy packages |
| 9 | Tech Stack | optional | Skip for T1 |
| 10 | Contributing | tier-gated | — |
| 11 | License | required | One line |

**Forbidden:** Deployment, Configuration (when no options exist), Adopters.

---

## 2. Application

A deployable service or full-stack product.

**Detection:** `dev`/`start` scripts, Dockerfile, docker-compose, no `publishConfig`.

### Section set

| Order | Section | Level | Notes |
|---|---|---|---|
| 1 | Hero | required | Lead with the outcome, not the stack |
| 2 | Features | required | Max 6, benefit-led |
| 3 | Demo / Preview | recommended | Screenshot or GIF when assets exist |
| 4 | Quick Start | required | Docker first, then manual |
| 5 | Configuration | required if `.env.example` exists | Group by file |
| 6 | Architecture | required | Architecture or sequence diagram |
| 7 | API | required if routes exist | Grouped by resource |
| 8 | Project Structure | recommended | Depth ≤ 3 |
| 9 | Tech Stack | recommended | Grouped by layer |
| 10 | Deployment | required if Docker/CI exists | Real commands only |
| 11 | Roadmap | tier-gated | T2+ |
| 12 | FAQ | tier-gated | T3 |
| 13 | Contributing | tier-gated | — |
| 14 | License | required | — |

---

## 3. CLI Tool

Installed and invoked from a terminal.

**Detection:** `bin` field, `cmd/` directory, `[[bin]]` in Cargo.toml, single entrypoint.

### Section set

| Order | Section | Level | Notes |
|---|---|---|---|
| 1 | Hero | required | Lead with the invocation |
| 2 | Features | required | Short list |
| 3 | Installation | required | Every package manager, separate blocks |
| 4 | Usage | required | Real invocation with real output |
| 5 | Commands | required | Table: command · description · example |
| 6 | Configuration | required if config file exists | Config file path + keys |
| 7 | Workflow Diagram | recommended | Flowchart of the main path |
| 8 | Compatibility | optional | OS matrix |
| 9 | Contributing | tier-gated | — |
| 10 | License | required | — |

**Forbidden:** API, Deployment, Architecture Graph (unless the tool embeds a remote
service).

### Commands table shape

```
| Command | Description | Example |
|---|---|---|
| `init` | Scaffold a config file | `tool init --template minimal` |
| `run` | Execute the pipeline | `tool run ./input.json` |
```

---

## 4. UI Library

A component library with visual output.

**Detection:** component exports, Storybook, theme token files, peer dependency on a
framework, no server code.

### Section set

| Order | Section | Level | Notes |
|---|---|---|---|
| 1 | Hero | required | Lead with the playground link |
| 2 | Preview | required when assets exist | Screenshot or GIF row |
| 3 | Features | required | — |
| 4 | Installation | required | Peer deps called out explicitly |
| 5 | Usage | required | One component, minimal props |
| 6 | Theming | recommended | Token names, not values |
| 7 | Components | recommended | Table: component · purpose |
| 8 | Compatibility | required if declared | Framework + browser versions |
| 9 | Accessibility | recommended | Conformance level if implemented |
| 10 | Contributing | tier-gated | Include the local dev server port |
| 11 | License | required | — |

**Forbidden:** Deployment, Configuration (env-based).

---

## 5. AI App

An application whose behaviour depends on models or inference frameworks.

**Detection:** model provider SDKs, RAG/agent/embedding dependencies, prompt files,
inference server config, vector store dependency.

### Section set

| Order | Section | Level | Notes |
|---|---|---|---|
| 1 | Hero | required | State what it does for the user |
| 2 | Capabilities | required | Separate model-backed capability from plain code |
| 3 | Demo | recommended | Interaction recording |
| 4 | Quick Start | required | Hardware gate first, then 4 lines |
| 5 | Model Configuration | required | Provider table, not a dump of keys |
| 6 | Environment Isolation | required | Separate envs for app and inference |
| 7 | Pipeline Diagram | required | Data flow: input → embed → retrieve → generate |
| 8 | Configuration | required if config exists | — |
| 9 | Capability Matrix | recommended | Which model tier unlocks which feature |
| 10 | Limitations | recommended | Honest scope boundaries |
| 11 | Contributing | tier-gated | — |
| 12 | License | required | — |

### Why this profile is different

Model capability varies wildly by parameter count. Never write "supports agents" without
qualifying which model class can actually satisfy it. Use a capability matrix:

```
| Mode | Interaction | Behaviour | Suitable models |
|---|---|---|---|
| Autonomous | Agent + multiple tools | Model plans and calls tools itself | Frontier models |
| Guided | Agent + one tool | Model parses arguments only | Mid-size models |
| Manual | No agent | User supplies all arguments | Small or non-tool models |
```

This table prevents users from filing bugs against behaviour their model cannot support.

---

## 6. Knowledge Base

A documentation, curriculum or reference corpus rather than executable software.

**Detection:** >20 Markdown files, no build system, no manifest, long-form single README,
`SUMMARY.md` / `mkdocs.yml`.

### Section set

| Order | Section | Level | Notes |
|---|---|---|---|
| 1 | Hero | required | State the audience and outcome |
| 2 | Navigation Funnel | required | Two-tier TOC (see below) |
| 3 | Motivation / Why | required | Who this is for |
| 4 | Curriculum / Topics | required | Grouped topic index |
| 5 | Topic Cards | required | One standardized card per topic |
| 6 | Worked Examples | recommended | Real case studies |
| 7 | Appendix / Cheatsheet | recommended | Reference tables |
| 8 | Translations | tier-gated | Per-language index |
| 9 | Contributing | required | Translation + content workflow |
| 10 | License | required | — |

**Forbidden:** Quick Start, API, Deployment, Tech Stack.

### Two-tier TOC funnel

A knowledge base longer than 800 lines needs two navigation layers:

1. **Journey layer** — the order a reader should progress through
2. **Index layer** — a flat, searchable list of every topic with anchors

### Standardized topic card

Every topic uses the same four-part shape so readers can skim:

```
## Topic name

<architecture or flow diagram>

One paragraph defining the concept and its mechanism.

### Modes / Variants
- **Mode A** — when to use it
- **Mode B** — when to use it

### Trade-offs
- What the approach costs you: complexity, latency, consistency, money

### Further reading
- <authoritative source>
```

The trade-offs subsection is mandatory. A topic card without a trade-off discussion is
incomplete — the discipline is the value of the format.

---

## 7. Infrastructure

Backend systems, databases, brokers, platforms, runtimes.

**Detection:** K8s manifests, Helm charts, `.proto` files, multi-SDK folders, server
components with coordinator/storage separation, operator code.

### Section set

| Order | Section | Level | Notes |
|---|---|---|---|
| 1 | Hero | required | Lead with the problem class it solves |
| 2 | What it does | required | 3–4 bolded capabilities with one-line bodies |
| 3 | Architecture | required | Topology diagram + design notes |
| 4 | Deployment Ladder | required | Lite → standalone → clustered |
| 5 | Quick Start | required | Shortest path to a running instance |
| 6 | Configuration | required | Key parameters, not every flag |
| 7 | SDK Matrix | required when clients exist | Language · package · status |
| 8 | Ecosystem | recommended | Integrations, adapters, tools |
| 9 | Scenario Matrix | recommended | Scenario → primitives used |
| 10 | Performance / Benchmarks | optional | Only with a reproducible source |
| 11 | Citation | optional | BibTeX when the project is cited academically |
| 12 | Contributing | tier-gated | — |
| 13 | License | required | Include the governance body if any |

### Deployment ladder pattern

Never open with a Helm chart. Escalate difficulty:

```
1. Embedded / zero-install   — single dependency, in-process
2. Container, single node    — one command to a working instance
3. Cluster / production      — orchestrator manifests, HA notes
4. Build from source         — contributor path only
```

### SDK matrix shape

```
| Language | Package | Status |
|---|---|---|
| Python | `pymilvus` | Stable |
| Go | `client/v3` | Stable |
| Java | `milvus-sdk-java` | Stable |
| Node.js | `milvus-sdk-node` | Beta |
```

---

## 8. Monorepo

Multiple packages or apps in one repository.

**Detection:** `workspaces` field, `packages/` + `apps/` directories, `pnpm-workspace.yaml`,
`lerna.json`, `nx.json`, `turbo.json`.

### Section set

| Order | Section | Level | Notes |
|---|---|---|---|
| 1 | Hero | required | — |
| 2 | Packages | required | Table of every package with purpose and status |
| 3 | Getting Started | required | Single install command for the whole tree |
| 4 | Common Scripts | required | Table of root scripts |
| 5 | Package Structure | required | Tree, depth ≤ 3 |
| 6 | Package Graph | recommended | Which packages depend on which |
| 7 | Development Workflow | recommended | How to work in one package |
| 8 | Releasing | tier-gated | How versions are cut |
| 9 | Contributing | tier-gated | — |
| 10 | License | required | Note per-package license variance |

### Packages table shape

```
| Package | Purpose | Version |
|---|---|---|
| `@scope/core` | Runtime primitives | 1.4.0 |
| `@scope/react` | React bindings | 1.4.0 |
| `@scope/cli` | Command-line interface | 1.2.1 |
```

---

## Selecting Between Overlapping Archetypes

| Ambiguity | Resolution |
|---|---|
| Library that also ships a CLI | Primary = Library, secondary = CLI Tool; add a Commands section |
| Application with an embedded model | AI App wins when model behaviour is the product; Application wins when the model is incidental |
| Infrastructure with SDKs | Infrastructure wins; the SDK folder becomes the SDK Matrix |
| Monorepo of libraries | Monorepo wins for the root README; each package gets its own Library README |
| UI Library inside a Monorepo | Monorepo at root, UI Library in the package folder |

Record the secondary archetype in the scan summary. It only influences emphasis — never
structure.
