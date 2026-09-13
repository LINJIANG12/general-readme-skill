# Section Recipes — Core

Identity and onboarding sections. These appear in nearly every project.

Templates for HTML regions are **not** reproduced here. Copy them verbatim from
`hero-and-html.md`. Quick Start ladder variants live in `onboarding.md`.

---

## Table of Contents

- [Overview](#overview)
- [Hero](#hero)
- [Features](#features)
- [Demo / Preview](#demo--preview)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [Configuration](#configuration)
- [Deployment](#deployment)
- [Limitations](#limitations)

---

## Overview

**Purpose:** orient the reader — what this project is and why it exists — in flowing prose,
before they reach the reference material. The concrete mechanics belong to **How It Works**.

**Include when:** there is a story to tell about what the project is and why it exists. Most
projects have one. Omit it only for a trivial tool with nothing to explain.

### Shape

```
## Overview

<paragraph 1: what this is, and who it is for>

<paragraph 2: the problem it solves, or why it exists>

<paragraph 3: what the reader gets — the promise, in outcomes>

<paragraph 4: what the reader has to do>
```

### Rules

1. **Prose, in short paragraphs.** No table, no bullet list, no sub-headings. Three to four
   paragraphs of two to four sentences each. A paragraph stays a paragraph — see
   `writing-style.md` → *Tables*.
2. **Answer "what is this and why does it exist".** The *why* is the point. If the section
   only restates what the project does, it has no reason to exist.
3. **Never invent the problem.** Do not open with a claim about what "most tools" or "the
   industry" gets wrong, and do not set up a bad status quo you cannot cite. State what this
   project does. A fabricated backdrop is an unsourced claim and fails gate G1.
4. **Open with what it is.** The first sentence names the thing and its purpose: `A skill
   that lets your AI read a project and write it a README`.
5. **Leave the mechanics to How It Works.** Give the shape and the payoff here; the
   phase-by-phase walk, the diagram and the parameters belong to the next section. The two
   sections must not say the same thing twice.
6. **Concrete over abstract.** Name the real promise — no invented content, no placeholders,
   hand-written parts survive a re-run — not "a better README experience".
7. **Do not repeat the Hero.** The Hero is one line; this is the paragraph behind it.
8. **Do not restate Features.** Features argues why the product is better; Overview says what
   it is and why it exists.
9. **Every claim must trace to a scan row.** Delete a claim rather than invent one.

---

## Hero

**Purpose:** answer "what is this and should I keep reading" in three seconds.

**Template:** `hero-and-html.md` → *Hero Template*. Do not restate or vary the structure.

### Composition rules

| Element | Rule |
|---|---|
| Title | Project name from the manifest `name`, the directory name, or the existing README. No prefix, no suffix. |
| Description | One sentence, 10–25 words. States what it *does*, not what it *is*. |
| Subtitle | Keywords separated by `·` — stack, distinguishing property, supported platforms. |
| CTA badges | At most two. Quick Start and License are the usual pair. |
| Primary badges | Identity group only (build, version, license, language). |
| Platform badges | Only when the project genuinely ships integration for those platforms. |
| Language switcher | Present only when more than one language file is produced. |

### Description examples

| Verdict | Text | Why |
|---|---|---|
| Good | `Fast, type-safe HTTP server for Node.js` | Concrete, states function |
| Good | `Vector database for large-scale similarity search` | Names the domain and the job |
| Good | `Generate professional README files from your codebase` | Subject and verb |
| Bad | `A powerful and robust HTTP server framework` | Banned adjectives, no function |
| Bad | `This project is an HTTP server` | Tautology |
| Bad | `Next-generation AI-powered platform leveraging cutting-edge technology` | All filler |

### Alt text on the logo

The Hero logo is informative — it names the project. Alt text must be the project name,
not `logo` or `banner`.

---

## Features

**Purpose:** the differentiators, in a form a reader can skim in ten seconds.

### Shape

```
- **Real-time sync** — WebSocket updates pushed to every connected client
- **Role-based access** — Permissions resolved per workspace membership
- **Typed errors** — Failures carry a status code and the parsed response body
```

### Rules

1. Maximum 6 items. With 20 features, pick the 6 a buyer would notice.
2. Never pad. Two real features beats six padded ones. A list is the default; a table is
   warranted only when every row carries two or more comparable values — see
   `writing-style.md` → *Tables*.
3. Each entry leads with the outcome, not the mechanism.
   - Good: `Streams 10k events/sec` — Bad: `Uses a lock-free ring buffer`
4. **A feature must be user-visible and high-impact.** Internal machinery — a build
   pipeline, a quality gate, a layer count, a repository layout, a test total — is not a
   feature. State the outcome it produces for the user instead.
5. No feature that the scan did not evidence.
6. Do not restate the description from the Hero.
7. Group only when there are 6+ and natural clusters exist (e.g. Security / Performance /
   Developer experience), otherwise a flat list.

### What counts as a feature

A feature answers "what does this do for me". An implementation detail answers "how is it
built" and belongs in How It Works or Contributing.

| Verdict | Feature | Why |
|---|---|---|
| Good | `Resumes interrupted uploads` | A visible outcome |
| Good | `A wrong command never reaches the README` | States what the user gets |
| Good | `Zero install dependencies` | Removes friction the user would feel |
| Bad | `Seven quality gates` | Internal mechanism — state what it prevents |
| Bad | `A fixed 20-section order` | A design detail — state the reader benefit |
| Bad | `Supports 8 languages` | A count, not a benefit, unless the reader uses those languages |
| Bad | `Monorepo with 6 packages` | Repository layout, not a user outcome |

### Do not

- List every dependency as a feature
- Write "and much more"
- Include a feature the project plans but has not implemented
- Use a phrase from the banned list in `writing-style.md`
- Describe a mechanism when the outcome is what the reader cares about

### Sourcing

Every row must trace to a scan row. If a capability is real but no file evidences it,
delete the row rather than softening it — gate G1.

---

## Demo / Preview

**Purpose:** prove the product works before the reader installs anything.

**Include when:** image or video assets exist in the repository.

### Asset shapes

| Asset | Form |
|---|---|
| Screenshot | Centered `<img>` with width constraint |
| Animated demo | `<img>` or `<video>` — GIF/WebP under ~5 MB |
| Multiple scenarios | Three-column card row (`hero-and-html.md` → *Demo Card Row*) |
| Live playground | Centered CTA badge linking to the playground |

### Rules

1. Never invent a screenshot URL. Only link assets that exist in the repository or an
   official domain the scan evidenced.
2. Alt text describes the content of the image, not its role. `alt="Agent builder showing a
   tool-selection panel"` — not `alt="screenshot"`.
3. For a three-column row, all three cells must have equal width and real content. Two
   real plus one filler fails gate G4.
4. Prefer linking an interactive playground over a static image when one exists — the
   reader can verify behaviour themselves.

---

## Quick Start

**Purpose:** get the reader to a running system with the fewest possible commands.

**Ladder variants:** `onboarding.md` — Docker-first, package-manager-first, language-first,
and hardware-gated variants.

### Mandatory structure

```
## Quick Start

<optional: one line stating the outcome — "Running at http://localhost:3000">

### Prerequisites        ← required when a runtime or service is required
### Install              ← required
### Configure            ← only when configuration is required
### Run                  ← required
```

### Rules

1. **Four steps maximum.** Prerequisites → install → configure → run.
2. **Every step is one copy-pasteable block.** No prose between the reader and the command.
3. **Infrastructure requirements come before the commands**, as a blockquote or alert, so
   a reader on an under-provisioned machine knows before they start.
4. **State the minimum runtime version** only when declared (`engines`, `requires-python`,
   `rust-version`).
5. **Close the loop.** After the run command, state the URL or observable result:
   `Open http://localhost:3000 — you should see the setup wizard.`
6. **No step numbering as prose.** No `Step 1: ...` — use H3 headings.
7. **Docker first when it exists**, with the manual path below it.
8. **Multi-package-manager projects** get separate blocks per manager, never a single
   slash-joined line.

### Failure modes

| Anti-pattern | Fix |
|---|---|
| `npm install && cp .env.example .env && npm run dev` on one line | Split into steps |
| No statement of what success looks like | Add the URL or output line |
| Requires an undocumented database | Add Prerequisites |
| Version requirement buried in prose | Move it to Prerequisites |
| Instructions that were never verified | Only use commands present in the repository |

---

## Usage

**Purpose:** show the API or interface in real use.

### Shape

```
## Usage

### <Scenario name>

```<language>
<real code from the project>
```

<one line on what this produces, if not obvious>
```

### Rules

1. **Real code only.** Source from `examples/`, `tests/`, README snippets already in the
   repo, or exported signatures. Never invent an import path.
2. **Maximum 4 examples.** Pick the four that exercise distinct capabilities.
3. **One concept per example.** A block that demonstrates auth, pagination and error
   handling at once teaches nothing.
4. **Language hint on every fence.** `typescript`, `python`, `go`, `bash`, `yaml`.
5. **Minimal comments.** The code should read on its own. Comment only non-obvious domain
   logic.
6. **H3 label per example** naming the scenario, not the mechanism.
   - Good: `### Streaming a response` — Bad: `### Using the createClient function`
7. **Close the loop for runnable examples** where possible — show the expected output.

### Progressive disclosure

When a basic and an advanced form both matter, show the basic form inline and put the
advanced form inside a `<details>` block (`hero-and-html.md` → *Collapsible Block*).

---

## Configuration

**Purpose:** let the reader run the project with their own settings.

Include only when the scan found configuration files (`.env.example`, `*.config.*`,
`*.yaml`, `*.toml`, `*.ini`).

### Shape

```
## Configuration

### <Config file or group>

| Variable | Description | Default | Required |
|---|---|---|---|
| `DATABASE_URL` | PostgreSQL connection string | — | yes |
| `PORT` | HTTP listen port | `3000` | no |
| `LOG_LEVEL` | `debug` · `info` · `warn` · `error` | `info` | no |
```

### Rules

1. **Group by file** when multiple config files exist.
2. **Mark required vs optional.** A reader must know what they have to supply.
3. **Show defaults as inline code**, and `—` when there is no default.
4. **Enumerate allowed values** for enum-like settings.
5. **Never print a real secret.** Use `YOUR_API_KEY` placeholders.
6. **Do not dump every flag.** Show what a first-time user needs; link to the full
   reference for the rest.
7. **Note precedence** when both env and file configuration exist (which wins).
8. **Warn about insecure defaults** where they exist, using a `> [!WARNING]` alert.

### Optional advanced block

Long or rarely used configuration belongs in a `<details>` block rather than the main
table.

---

## Deployment

**Purpose:** take the project from local to running in production.

Include only when the scan found `Dockerfile`, `docker-compose.yml`, CI config, Helm
charts, or cloud manifests.

### Shape

```
## Deployment

### Docker

```bash
<real docker commands from the project>
```

### Docker Compose

```bash
<real compose command>
```

### Kubernetes

<only when manifests exist — reference the chart path>

### CI/CD

<name the pipeline and reference the config file>
```

### Rules

1. **Use the project's real commands.** Read `Makefile`, `package.json`, compose files —
   never write a generic `docker build -t my-app .`.
2. **Order by likelihood**: Docker → Compose → orchestrator → platform.
3. **Reference the actual file paths** for manifests.
4. **Name the pipeline** when CI exists, and link the workflow file.
5. **Add platform buttons** only for platforms the project actually supports and
   documents. A button that leads nowhere fails gate G5.
6. **Never include credentials** in deployment examples.

---

## Limitations

**Purpose:** state what the project does not do. Honest scope prevents mismatched adoption
and misdirected bug reports.

**Include when:** the code, docs or issues state a real boundary or constraint.

### Shape

```
## Limitations

- <What it cannot do, and the boundary condition>
- <Known constraint, and the workaround if one exists>
```

### Rules

1. Describe a real boundary found in the code or docs — not a humble-brag ("does not
   support infinite scale").
2. Pair each limitation with a workaround or a link when one exists.
3. Never use this section to advertise. It is the one section where admitting a weakness
   builds trust.
4. Do not duplicate the FAQ — Limitations are boundaries, the FAQ is questions.
