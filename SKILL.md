---
name: general-readme-skill
description: Use when generating, rewriting, upgrading or reviewing a README.md for any project. Triggers on /readme, "generate readme", "write readme", "update readme", "帮我写 README", "更新README", "生成项目文档". Produces evidence-bound, accessible README files in one consistent house style, with optional multi-language output.
version: 3.0
tags: documentation, readme, auto-generate, project-docs, i18n, accessibility
---

# General README Skill

Generate README files that read like a maintainer who knows the codebase wrote them,
because every claim is bound to a real source file.

**One ordering logic. One voice. Every project.** Sections are chosen to fit the project and
ordered so that a reader's questions are answered in the order they are asked. There is no
rigid list of sections to obey — and no arbitrary layout either.

## Design Principles

1. **Evidence-bound.** Every feature, command, version, path and default must resolve to a
   scanned file. An unbound claim is deleted, never softened.
2. **One ordering logic.** Sections are chosen per project and ordered by what the reader
   needs next. No rigid list, no per-type template — but never an arbitrary order either.
3. **One voice.** A single house writing style. No tone selection.
4. **Compose once.** Hero and other HTML regions are authored as HTML directly. There is no
   separate beautification pass.
5. **Single source of truth.** Every template lives in exactly one reference file. Never
   restate a template that already exists elsewhere.
6. **Progressive disclosure.** This file routes; references carry detail. Load only the
   files the current task needs.
7. **Progressive onboarding.** A reader reaches a running system in four lines or fewer.
8. **Accessible and maintainable.** Alt text, table headers, and reversible HTML only.
9. **The right form for the content.** A comparison across attributes is a table; a name plus
   one clause is a bullet; a sequence is a numbered list; a risk is an alert; a flow is a
   diagram; a picture beats a paragraph. Choose the form that reads best — never one form for
   everything, and never prose dressed up as a table.
10. **Nothing is lost.** A fact stated in an existing README survives every regeneration — in
    place, in another section, or in an auxiliary document. It is never dropped in silence.

## Trigger Rules

Trigger when user input matches any of:

- Exact command: `/readme`
- Text: generate readme, write readme, create project documentation, update readme,
  rewrite readme, review my README
- Chinese: 帮我写 README, 生成项目文档, 更新README, 优化README
- Scenario: user asks to create, rewrite, upgrade, or critique a project README

---

## Workflow

```
Phase 0  Configure → language, entry mode
Phase 1  Scan      → build an evidence map from static files only
Phase 2  Compose   → choose the sections the project needs and order them for the reader
Phase 3  Verify    → run the seven quality gates, repair or drop failures
Phase 4  Output    → write primary file, then localized files
```

**Two entry modes.** Detect the mode in Phase 0:

| Mode | Condition | Behaviour |
|---|---|---|
| **Create** | No `README.md`, or user asks for full regeneration | Author every section from scratch |
| **Upgrade** | `README.md` exists and user wants improvement | Preserve manual content, regenerate only auto regions, emit a change summary |

Detailed phase instructions: `references/workflow.md` — read it before Phase 1.

> **Hard constraint for all phases:** read static files only. Never execute, modify or
> delete project files. Never run `git` or any state-changing command.

---

## Document Shape

There is no fixed section list. A README is a set of sections chosen to fit the project,
ordered so that a reader's questions are answered in the order they are asked.

### The ordering principle

Order by what the reader needs next, not by a template.

| Stage | Answers | Typical sections |
|---|---|---|
| **Identity** | What is this? | Hero, Overview |
| **Proof** | Why should I believe it? | Demo / Preview |
| **Onboarding** | How do I start? | Quick Start, Requirements |
| **Mechanics** | How does it work? | How It Works |
| **Reference** | The detail | Usage, API, Commands, Configuration, Project Structure, Tech Stack |
| **Operations** | Running it for real | Deployment, Security |
| **Community** | Who else is involved? | Contributing & Community, Roadmap, FAQ, Sponsors & Adopters, Citation, License |

### The section library

Pick what fits; skip what does not. Recipes live in `references/sections-*.md`.

| Section | Include when | Recipe |
|---|---|---|
| **Hero** | Always | `sections-core.md` |
| **Overview** | The project has a reason to exist worth stating | `sections-core.md` |
| **Demo / Preview** | Always — show real effects (screenshots, recordings, links); emit a placeholder when no asset is provided | `sections-core.md` |
| **Quick Start** | A runnable entry point exists | `sections-core.md` |
| **How It Works** | A flow, workflow or architecture can be derived from the source | `sections-reference.md` |
| **Usage** | A public API, interface or exported surface exists | `sections-core.md` |
| **Requirements** | Runtime, platform or dependency requirements exist | `sections-reference.md` |
| **Configuration** | Config files are detected | `sections-core.md` |
| **Project Structure** | More than one top-level source directory | `sections-reference.md` |
| **API** | Routes, schemas or exported services are detected | `sections-reference.md` |
| **Commands** | A CLI entrypoint exists | `sections-reference.md` |
| **Tech Stack** | Dependencies are declared | `sections-reference.md` |
| **Deployment** | Dockerfile, compose, CI or platform manifests are detected | `sections-core.md` |
| **Roadmap** | A roadmap file or documented plan exists | `sections-growth.md` |
| **FAQ** | An FAQ document or recurring questions exist | `sections-growth.md` |
| **Contributing & Community** | A contributing guide, templates or community links exist | `sections-growth.md` |
| **Sponsors & Adopters** | A funding config or documented adopters exist | `sections-growth.md` |
| **Security** | `SECURITY.md` exists, or the project handles auth, network or user data | `sections-growth.md` |
| **Citation** | `CITATION.cff` exists, or a published paper exists | `sections-growth.md` |
| **License** | A licence file exists | `sections-growth.md` |

### Rules

1. **A section with no data is not written.** Never `N/A`, never `Coming soon`, never filler —
   the Demo section excepted, which carries a placeholder by design when no asset exists.
2. **A section with data is not silently lost**, and neither is any other fact from an existing
   README. See the Displaced Content Policy in `references/workflow.md`.
3. **Add project-specific sections when the project needs them.** A section named for its
   content (`数据来源`, `计算模型`, `迁移指南`) beats forcing that content into a wrong one.
   Name it after what it holds, never after its position.
4. **The order above is the default, not a law.** Move a section when the project's own logic
   demands it — a hardware-gated project may need Requirements before Quick Start.
5. **Never force content into a wrong section** to satisfy a shape.
6. **The Hero always sits first**, followed by an optional table of contents
   (`hero-and-html.md`). Neither counts as a section.

Section recipes: `references/sections-core.md`, `sections-reference.md`, `sections-growth.md`.

---

## Routing Table

Read a reference only when the current task needs it.

| Need | Read |
|---|---|
| Full phase procedures, Upgrade-mode diffing | `references/workflow.md` |
| Detection rules, evidence-map format | `references/project-scan.md` |
| Overview / Hero / Demo / Quick Start / Usage / Config / Deployment recipes | `references/sections-core.md` |
| How It Works / API / Commands / Structure / Stack / Requirements recipes | `references/sections-reference.md` |
| Contributing / Community / Sponsors / Roadmap / FAQ / Security / License recipes | `references/sections-growth.md` |
| Hero template, HTML recipes, alerts, link pool, collapsing | `references/hero-and-html.md` |
| Quick Start ladder, PaaS matrix, multi-package-manager blocks | `references/onboarding.md` |
| Sponsors, adopters, contributors, citations, star history | `references/social-proof.md` |
| Self-check checklist before delivery | `references/quality-gates.md` |
| Alt text, contrast, RTL, table headers | `references/accessibility.md` |
| Multi-language naming, switcher bar, localization policy | `references/language-guide.md` |
| The house writing style and banned phrases | `references/writing-style.md` |
| Technology → shields.io badge URL | `references/badges.md` |
| Badge grouping and caps | `references/badge-styles.md` |
| Mermaid / SVG diagram templates | `references/diagram-templates.md` |

**Reference integrity.** Before generation, confirm every reference you intend to read
exists and is readable. If one is missing, either request all remaining files or continue
with the safe defaults and state which reference was unavailable. Never silently proceed
as if a missing reference had been loaded.

---

## Phase 0 — Configure

Only two things are resolved. There is no structure to pick and no voice to pick.

| Option | Values | Default |
|---|---|---|
| Primary language | any ISO 639-1 / BCP 47 code | Chinese (Simplified) |
| Secondary languages | zero or more | none |

Plus the auto-detected entry mode (Create / Upgrade).

If the user supplies no answers, proceed with the defaults and say so. Do not block on
questions.

> **Primary language.** The primary language always occupies `README.md`, whatever the
> language is. Every additional language takes `README.<code>.md`. Adding English as a
> secondary is the usual choice for projects with an international audience.

Badge style is fixed at `flat`. Diagram colours are fixed by the palette in
`diagram-templates.md`. Both are part of the house style and are not configurable.

## Phase 1 — Scan

Build an **evidence map**: an explicit `claim → source` list. Without it, Phase 2 has
nothing to bind to and the anti-fabrication principle is unenforceable.

Start with the three-pass discovery model: map the file tree with its hierarchy, read the
core files (manifests, entry points, AND core business logic implementations: services, commands,
domain engines) in full, then sample secondary modules on demand. Documenting a project
does not require reading all of it — stop once the core capabilities and contracts have
concrete evidence behind them.

In **Upgrade mode**, also build a **content ledger** first: list every section and every
notable block of the existing README. The ledger is the checklist that guarantees nothing is
lost — each entry must end the run as kept, relocated, merged or explicitly prompted.

Rules, detector precedence, the discovery-pass model, and the evidence-map format live in
`references/project-scan.md`. The scan also reports which sections have data.

## Phase 2 — Compose

1. From the section library, take the sections the scan has data for; skip the rest.
2. Add a project-specific section when the project genuinely needs one (see *Document Shape*).
3. Order the chosen sections by the ordering principle — identity → proof → onboarding →
   mechanics → reference → operations → community.
4. For each section, pick the form that reads best: table, list, prose, alert, diagram or
   code block (`writing-style.md` → *The Right Form*).
5. Read the matching recipes and the visual references you will use.
6. Author Hero and other HTML regions directly as HTML per `references/hero-and-html.md`.
   Do not write Markdown first and convert later.
7. Place a jumpable table of contents between the Hero and the first section when the
   document has more than about five sections (`hero-and-html.md` → *Table of Contents*).
8. Write in the house style from `references/writing-style.md`.
9. Prefer the reference-style link pool for all URLs (see `hero-and-html.md`).
10. Mask secrets, keys, tokens and private hostnames as you write.

Precedence when constraints conflict:

1. Privacy protection
2. Lose nothing (Upgrade mode) — preserve manual content, and every fact, in place or elsewhere
3. Evidence binding — no unbound claim
4. The reader's order — questions answered in the order they are asked
5. Visual preferences

## Phase 3 — Verify

Run all seven gates from `references/quality-gates.md`. Any gate that fails is repaired;
if a claim cannot be repaired it is deleted rather than weakened.

| Gate | Checks |
|---|---|
| G1 Evidence | Every assertion traces to a source |
| G2 Structure | Sections are ordered for the reader, none empty, nothing with data missing |
| G3 Voice | No banned phrases, house style applied |
| G4 Visual | Hero compliant, badges grouped, templates unmodified from source |
| G5 Links | No placeholder URLs, relative paths resolve, anchors exist |
| G6 Accessibility | Every image has alt text, every table has a header row |
| G7 i18n | Switcher is bidirectional, localized links mapped |

Report the gate results to the user as a short pass/fail list.

## Phase 4 — Output

1. Write the primary `README.md`.
2. Write one file per secondary language.
3. Ensure the language switcher is present and bidirectional in **every** file.
4. Normalize: UTF-8, LF line endings, no trailing whitespace, single blank line between
   blocks.
5. In **Upgrade mode**, walk the content ledger and report every entry: kept, relocated,
   merged or prompted. No entry may end as "dropped".
6. Report the change summary (Create mode: sections written; Upgrade mode: added /
   regenerated / preserved / displaced).

If the scan produced no usable data, stop and reply exactly:
`No valid project content detected, cannot generate README.`

---

## Non-Negotiables

- **No fabrication.** No invented feature, command, flag, version, path or benchmark.
- **No filler.** Banned: placeholder sections, "coming soon", empty prose.
- **No arbitrary order.** Sections are ordered for the reader — never shuffled to look
  organised, and never left in the order they happened to be written.
- **No empty sections.** A section without data is not written; the Demo placeholder is the
  single exception.
- **No template drift.** If a template exists in a reference, copy it verbatim.
- **No destructive edits.** In Upgrade mode `<!-- MANUAL-START -->` …
  `<!-- MANUAL-END -->` blocks and untagged sections survive untouched.
- **Nothing is lost.** Any content in an existing README that cannot fit the new shape must be
  relocated to an appropriate auxiliary document (`CONTRIBUTING.md`, `MIGRATION.md`, `docs/`)
  with a link back, or explicitly prompted to the user. This covers facts as well as sections:
  a dependency, command or caveat named in the old README must still be present in the new one
  (`references/workflow.md` → *Displaced Content Policy*).

## Reference Catalog

| File | Purpose |
|---|---|
| `workflow.md` | Phase procedures and Upgrade-mode diffing |
| `project-scan.md` | Detection rules, evidence-map format |
| `sections-core.md` | Overview, Hero, Demo, Quick Start, Usage, Configuration, Deployment, Limitations |
| `sections-reference.md` | How It Works, API, Commands, Structure, Stack, Requirements, SDKs, Packages |
| `sections-growth.md` | Contributing, Community, Roadmap, FAQ, Security, Sponsors, Citation, License |
| `hero-and-html.md` | Hero template and HTML recipe library |
| `onboarding.md` | Quick Start ladder, deploy matrices |
| `social-proof.md` | Sponsors, adopters, contributors, citations |
| `quality-gates.md` | Seven delivery gates |
| `accessibility.md` | Alt text, contrast, RTL |
| `language-guide.md` | Naming, switcher, localization policy |
| `writing-style.md` | The house style and banned phrases |
| `badges.md` | Technology → badge URL mapping |
| `badge-styles.md` | Badge grouping and caps |
| `diagram-templates.md` | Mermaid and SVG templates |
