---
name: general-readme-skill
description: Use when generating, rewriting, upgrading or reviewing a README.md for any project. Triggers on /readme, "generate readme", "write readme", "update readme", "帮我写 README", "更新README", "生成项目文档". Produces evidence-bound, accessible README files in one consistent house style, with optional multi-language output.
version: 3.0
tags: documentation, readme, auto-generate, project-docs, i18n, accessibility
---

# General README Skill

Generate README files that read like a maintainer who knows the codebase wrote them,
because every claim is bound to a real source file.

**One structure. One voice. Every project.** There is a single fixed section order and a
single writing style. A CLI tool and a vector database get the same skeleton — they simply
differ in which sections have data behind them.

## Design Principles

1. **Evidence-bound.** Every feature, command, version, path and default must resolve to a
   scanned file. An unbound claim is deleted, never softened.
2. **One structure.** A single fixed section order applies to every project. No profiles, no
   variants, no per-type templates. Sections with no data are skipped; the rest never move.
3. **One voice.** A single house writing style. No tone selection.
4. **Compose once.** Hero and other HTML regions are authored as HTML directly. There is no
   separate beautification pass.
5. **Single source of truth.** Every template lives in exactly one reference file. Never
   restate a template that already exists elsewhere.
6. **Progressive disclosure.** This file routes; references carry detail. Load only the
   files the current task needs.
7. **Progressive onboarding.** A reader reaches a running system in four lines or fewer.
8. **Accessible and maintainable.** Alt text, table headers, and reversible HTML only.
9. **Sparing with tables.** A table is used only when the content is genuinely tabular. A
   name plus one clause is a bullet, not a table; a short overview stays one paragraph.

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
Phase 2  Compose   → fill the fixed section order, skipping sections with no data
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

## The Structure

This is the only README structure the skill produces. Sections appear in exactly this
order. **A section is skipped entirely when the scan produced no data for it** — never
`N/A`, never `Coming soon`, never a placeholder.

The **Hero** always sits first, followed by an optional **Table of Contents**; neither is
counted among the 20. A jumpable table of contents belongs there when the document has
more than about five sections (`references/hero-and-html.md` → *Table of Contents*). It is
a navigation aid, not one of the sections.

**Overview is prose, not an inventory.** It answers, in a few short paragraphs, what the
project is and why it exists — no table, no bullet list. It is the reader's orientation and
it carries the *why*; **How It Works** carries the concrete mechanics. The directory tree
belongs in Project Structure, not here.

| # | Section | Include when |
|---|---|---|
| 1 | **Overview** | There is a story to tell about what the project is and why it exists |
| 2 | **Features** | At least one user-visible, high-impact differentiator |
| 3 | **Demo / Preview** | Image, video or example output exists in the repo |
| 4 | **Quick Start** | A runnable entry point exists |
| 5 | **How It Works** | A flow, workflow or architecture can be derived from the source |
| 6 | **Usage** | A public API, interface or exported surface exists |
| 7 | **Requirements** | Runtime, platform or dependency requirements exist |
| 8 | **Configuration** | Config files detected (`.env.example`, `*.config.*`, `*.yaml`, `*.toml`) |
| 9 | **Project Structure** | More than one top-level source directory |
| 10 | **API** | Routes, schemas or exported service definitions detected |
| 11 | **Commands** | A CLI entrypoint exists (`bin`, `cmd/`, `[[bin]]`, `[project.scripts]`) |
| 12 | **Tech Stack** | Dependencies declared in a manifest |
| 13 | **Deployment** | Dockerfile, compose file, CI config or platform manifests detected |
| 14 | **Roadmap** | A roadmap file, milestone config or documented plan exists |
| 15 | **FAQ** | An FAQ document exists, or recurring questions are documented |
| 16 | **Contributing & Community** | `CONTRIBUTING.md`, issue templates, or community links exist |
| 17 | **Sponsors & Adopters** | A funding config or documented adopters exist |
| 18 | **Security** | `SECURITY.md` exists, or the project handles auth, network or user data |
| 19 | **Citation** | `CITATION.cff` exists, or the project has a published paper |
| 20 | **License** | A licence file exists |

Final section otherwise:

> If no licence file exists, omit section 20 and close with one line instead:
> `No LICENSE file detected. Add a LICENSE to clarify project licensing.`

A typical project produces 10–14 of the 20 sections. Producing 20 is not the goal;
producing the right ones in the right order is.

Section recipes: `references/sections-core.md`, `sections-reference.md`, `sections-growth.md`.

---

## Routing Table

Read a reference only when the current task needs it.

| Need | Read |
|---|---|
| Full phase procedures, Upgrade-mode diffing | `references/workflow.md` |
| Detection rules, evidence-map format | `references/project-scan.md` |
| Overview / Hero / Features / Demo / Quick Start / Usage / Config / Deployment recipes | `references/sections-core.md` |
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
core files in full, then sample the rest on demand. Documenting a project does not require
reading all of it — stop once the sections have enough evidence behind them.

Rules, detector precedence, the discovery-pass model, and the evidence-map format live in
`references/project-scan.md`. The scan also reports which of the 20 sections have data.

## Phase 2 — Compose

1. Read the section list above. For each section, take the scan's verdict on whether data
   exists; skip the ones that do not.
2. Read the matching section recipes and the visual references you will use.
3. Author the surviving sections in the fixed order. Never reorder them.
4. Author Hero and other HTML regions directly as HTML per `references/hero-and-html.md`.
   Do not write Markdown first and convert later.
5. Place a jumpable table of contents between the Hero and the first section when the
   document has more than about five sections (`hero-and-html.md` → *Table of Contents*).
6. Write in the house style from `references/writing-style.md`.
7. Prefer the reference-style link pool for all URLs (see `hero-and-html.md`).
8. Mask secrets, keys, tokens and private hostnames as you write.

Precedence when constraints conflict:

1. Privacy protection
2. Preserve manual content (Upgrade mode)
3. Evidence binding — no unbound claim
4. The fixed section order
5. Visual preferences

## Phase 3 — Verify

Run all seven gates from `references/quality-gates.md`. Any gate that fails is repaired;
if a claim cannot be repaired it is deleted rather than weakened.

| Gate | Checks |
|---|---|
| G1 Evidence | Every assertion traces to a source |
| G2 Structure | Surviving sections appear in the fixed order, none reordered |
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
5. Report the change summary (Create mode: sections written; Upgrade mode: added /
   regenerated / preserved).

If the scan produced no usable data, stop and reply exactly:
`No valid project content detected, cannot generate README.`

---

## Non-Negotiables

- **No fabrication.** No invented feature, command, flag, version, path or benchmark.
- **No filler.** Banned: placeholder sections, "coming soon", empty prose.
- **No reordering.** The section order is fixed. Sections are skipped, never moved.
- **No extra sections.** Do not invent a section outside the 20 listed.
- **No template drift.** If a template exists in a reference, copy it verbatim.
- **No destructive edits.** In Upgrade mode `<!-- MANUAL-START -->` …
  `<!-- MANUAL-END -->` blocks and untagged top-level sections survive untouched.

## Reference Catalog

| File | Purpose |
|---|---|
| `workflow.md` | Phase procedures and Upgrade-mode diffing |
| `project-scan.md` | Detection rules, evidence-map format |
| `sections-core.md` | Overview, Hero, Features, Demo, Quick Start, Usage, Configuration, Deployment, Limitations |
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
