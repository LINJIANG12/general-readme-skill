---
name: general-readme-skill
description: Use when generating, rewriting, upgrading or reviewing a README.md for any project. Triggers on /readme, "generate readme", "write readme", "update readme", "帮我写 README", "更新README", "生成项目文档". Produces evidence-bound, archetype-aware, accessible README files with modern visual layout and optional multi-language output.
version: 2.0
tags: documentation, readme, auto-generate, project-docs, i18n, accessibility
---

# General README Skill

Generate README files that read like they were written by a maintainer who knows the
codebase — because every claim is bound to a real source file.

> **Derivative work.** Version 2.0 is a substantial rewrite of
> [KieranGao/general-readme-skill](https://github.com/KieranGao/general-readme-skill)
> by OxyTheCrack (MIT). The original copyright notice is retained in `LICENSE`. See
> `README.md` → *Origin and Attribution* for the full change list and the research basis.

## Design Principles

1. **Evidence-bound.** Every feature, command, version, path and default must resolve to
   a scanned file. An unbound claim is deleted, never softened.
2. **Archetype-aware.** Structure follows what the project *is*. A CLI tool and a vector
   database do not share a skeleton.
3. **Compose once.** Hero and other HTML regions are authored as HTML directly. There is
   no separate beautification pass.
4. **Single source of truth.** Every template lives in exactly one reference file. Never
   restate a template that already exists elsewhere.
5. **Progressive disclosure.** This file routes; references carry detail. Load only the
   files the current project needs.
6. **Progressive onboarding.** A reader must reach a running system in four lines or fewer.
7. **Accessible and maintainable.** Alt text, table headers, and reversible HTML only.

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
Phase 0  Classify  → archetype + maturity tier + configuration
Phase 1  Scan      → build an evidence map from static files only
Phase 2  Compose   → assemble sections from the library, archetype-driven
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

## Routing Table

Read a reference only when the current task needs it.

| Need | Read |
|---|---|
| Full phase procedures, Upgrade-mode diffing | `references/workflow.md` |
| Detection rules, evidence-map format | `references/project-scan.md` |
| Archetype → section set, defaults, maturity tier rules | `references/profiles.md` |
| Hero / Features / Quick Start / Usage / Config / Deployment recipes | `references/sections-core.md` |
| Architecture / API / Project Structure / Tech Stack recipes | `references/sections-reference.md` |
| Contributing / Community / Sponsors / Roadmap / FAQ / License recipes | `references/sections-growth.md` |
| Hero template, HTML recipes, alerts, link pool, collapsing | `references/hero-and-html.md` |
| Quick Start ladder, PaaS matrix, multi-package-manager blocks | `references/onboarding.md` |
| Sponsors, adopters, contributors, citations, star history | `references/social-proof.md` |
| Self-check checklist before delivery | `references/quality-gates.md` |
| Alt text, contrast, RTL, table headers | `references/accessibility.md` |
| Multi-language naming, switcher bar, localization policy | `references/language-guide.md` |
| Voice, sentence rules, banned phrases | `references/tone-profiles.md` |
| Technology → shields.io badge URL | `references/badges.md` |
| Badge grouping by maturity tier | `references/badge-styles.md` |
| Mermaid / SVG diagram templates | `references/diagram-templates.md` |

**Reference integrity.** Before generation, confirm every reference you intend to read
exists and is readable. If one is missing, either request all remaining files or continue
with the safe defaults and state which reference was unavailable. Never silently proceed
as if a missing reference had been loaded.

---

## Phase 0 — Classify

1. Determine **archetype** (8 options) and **maturity tier** (T1/T2/T3) using
   `references/profiles.md`.
2. Confirm configuration with the user, offering the archetype's defaults as
   pre-selected answers:

| Option | Values | Default |
|---|---|---|
| Tone | Energetic / Minimal / Professional / Playful / Academic / Enterprise | archetype default |
| Badge style | flat / flat-square / for-the-badge | flat |
| Primary language | any ISO 639-1 | English |
| Secondary languages | zero or more | none |
| Growth sections | on / off | tier default |

3. If the user supplies no answers, proceed with the archetype defaults and say so.
   Do not block on questions.

## Phase 1 — Scan

Build an **evidence map**: an explicit `claim → source` list. Without it, Phase 2 has
nothing to bind to and the anti-fabrication principle is unenforceable.

Rules, detector precedence, and the evidence-map format live in
`references/project-scan.md`.

## Phase 2 — Compose

1. Read `references/profiles.md` for the section set of the detected archetype.
2. Read the matching section recipes and the visual references you will use.
3. Author sections in the profile's declared order. Skip a section only when the scan
   produced no data for it — never emit `N/A`, `Coming soon`, or placeholder prose.
4. Author Hero and other HTML regions directly as HTML per
   `references/hero-and-html.md`. Do not write Markdown first and convert later.
5. Prefer the reference-style link pool for all URLs (see `hero-and-html.md`).
6. Mask secrets, keys, tokens and private hostnames as you write.

Precedence when constraints conflict:

1. Privacy protection
2. Preserve manual content (Upgrade mode)
3. Evidence binding — no unbound claim
4. Section order for the archetype
5. Visual/voice preferences

## Phase 3 — Verify

Run all seven gates from `references/quality-gates.md`. Any gate that fails is repaired;
if a claim cannot be repaired it is deleted rather than weakened.

| Gate | Checks |
|---|---|
| G1 Evidence | Every assertion traces to a source |
| G2 Structure | Archetype-required sections present and ordered |
| G3 Voice | No banned phrases, one consistent tone |
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
- **No filler.** Banned: placeholder sections, "coming soon", emoji-free-but-empty prose.
- **No template drift.** If a template exists in a reference, copy it verbatim.
- **No destructive edits.** In Upgrade mode `<!-- MANUAL-START -->` …
  `<!-- MANUAL-END -->` blocks and untagged top-level sections survive untouched.

## Reference Catalog

| File | Purpose |
|---|---|
| `workflow.md` | Phase procedures and Upgrade-mode diffing |
| `project-scan.md` | Detection rules, evidence-map format |
| `profiles.md` | 8 archetypes, maturity tiers, defaults |
| `sections-core.md` | Identity and onboarding section recipes |
| `sections-reference.md` | Architecture, API, structure, stack recipes |
| `sections-growth.md` | Community, sponsors, roadmap, FAQ, license recipes |
| `hero-and-html.md` | Hero template and HTML recipe library |
| `onboarding.md` | Quick Start ladder, deploy matrices |
| `social-proof.md` | Sponsors, adopters, contributors, citations |
| `quality-gates.md` | Seven delivery gates |
| `accessibility.md` | Alt text, contrast, RTL |
| `language-guide.md` | Naming, switcher, localization policy |
| `tone-profiles.md` | Six voices and the tone × archetype matrix |
| `badges.md` | Technology → badge URL mapping |
| `badge-styles.md` | Badge grouping by tier |
| `diagram-templates.md` | Mermaid and SVG templates |
