# Section Recipes — Core

Identity and onboarding sections. These appear in nearly every project.

Templates for HTML regions are **not** reproduced here. Copy them verbatim from
`hero-and-html.md`. Quick Start ladder variants live in `onboarding.md`.

---

## Table of Contents

- [Overview](#overview)
- [Hero](#hero)
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
3. **Never invent the problem, and never open with a contrast.** Do not open with a claim
   about what "most tools" or "the industry" gets wrong, do not set up a bad status quo you
   cannot cite, and do not begin with "unlike other projects". The reader came for this
   project, not for a review of its alternatives. A fabricated backdrop is an unsourced
   claim and fails gate G1; a 踩一捧一 opener is deleted on sight.
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

## Demo / Preview

**Purpose:** showcase the real-world usage, UI appearance, or interactive results of the project before installation.

**Rules:**
1. **Real effects only:** Display actual screenshots, animated recordings (GIF/WebP), terminal casts, or live demo/playground links, paired with concise explanatory text.
2. **Human-provided assets:** Visual and demo materials typically require manual provision by the developer/maintainer.
3. **Placeholder when absent:** If the author has not yet provided real media assets or demo links, output a clear, actionable placeholder instead of silently omitting or fabricating an imaginary comparison table:
   ```markdown
   > [!TIP]
   > <!-- DEMO_PLACEHOLDER -->
   > **演示素材待补充**：请在此补充项目的实际运行截图、动图演示或在线 Playground 链接。
   ```
4. Never fabricate screenshot URLs or imaginary before-after comparisons. Only link verified assets that exist in the repository or an evidenced domain.
5. All images must include meaningful alt text describing what is shown.

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
