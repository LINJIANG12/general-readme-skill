# Hero and HTML Recipes

**This file is the single source of truth for every HTML template.** Other references
point here. Never restate a template elsewhere; never invent a variant.

---

## Table of Contents

- [When to Use HTML](#when-to-use-html)
- [Hero Template](#hero-template)
- [Language Switcher](#language-switcher)
- [Table of Contents](#table-of-contents)
- [Link Pool](#link-pool)
- [Collapsible Block](#collapsible-block)
- [GFM Alerts](#gfm-alerts)
- [Dual-Theme Media](#dual-theme-media)
- [Demo Card Row](#demo-card-row)
- [Capability Card Row](#capability-card-row)
- [Back to Top](#back-to-top)
- [Kept as Markdown](#kept-as-markdown)
- [Upgrading an Existing README](#upgrading-an-existing-readme)

---

## When to Use HTML

| Region | Use HTML | Reason |
|---|---|---|
| Hero | Yes | Requires centering, which Markdown cannot express |
| Language switcher | Yes | Centering and alignment |
| Multi-column card rows | Yes | Requires table or flex layout |
| Sponsor / adopter walls | Yes | Requires grid |
| Collapsible panels | Yes | `<details>` has no Markdown equivalent |
| Alerts | No — use GFM syntax | Native GitHub rendering |
| Tables | No | Markdown tables are easier to maintain |
| Lists | No | Markdown is easier to maintain |
| Code blocks | No | Fenced blocks carry syntax highlighting |
| Mermaid | No | GitHub renders fenced Mermaid natively |
| Headings | No | Markdown headings get anchors and appear in the outline |
| Dividers | No | `---` is sufficient |

**Rule:** use HTML only when Markdown cannot express the intent. HTML that merely
duplicates Markdown capability is rejected at gate G4.

**Accessibility:** HTML regions must still satisfy gate G6 — alt text on every image,
accessible labels on every icon-only link.

---

## Hero Template

Copy verbatim. Replace only the `{PLACEHOLDER}` tokens and the outlined optional blocks.

```html
<div align="center">

<a name="readme-top"></a>

<img src="{LOGO_URL}" alt="{PROJECT_NAME}" height="{LOGO_HEIGHT}" />

<h1>{PROJECT_NAME}</h1>

<p>
  <strong>{ONE_LINE_DESCRIPTION}</strong>
  <br />
  <em>{KEYWORD} · {KEYWORD} · {PLATFORM_SUPPORT}</em>
</p>

<p>
  <a href="#quick-start"><img src="https://img.shields.io/badge/Quick_Start-{COLOR}?style=for-the-badge" alt="Quick Start" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-{LICENSE}-{COLOR}?style=for-the-badge" alt="License: {LICENSE}" /></a>
</p>

<p>
  {IDENTITY_BADGES}
</p>

<p>
  {TECH_BADGES}
</p>

<p>
  {LANGUAGE_SWITCHER}
</p>

</div>
```

### Token reference

| Token | Source | Constraint |
|---|---|---|
| `{LOGO_URL}` | Repository asset or official domain | Must exist — never a placeholder URL |
| `{PROJECT_NAME}` | Manifest `name`, directory name, or existing README | No prefix or suffix |
| `{LOGO_HEIGHT}` | — | `80`–`180`; use `180` only when the image is square |
| `{ONE_LINE_DESCRIPTION}` | Derived from manifest description + scan | 10–25 words |
| `{KEYWORD}` | Stack, property, platform | 3–6 keywords |
| `{COLOR}` | Brand colour, or the house accent `3178C6` | Hex without `#` |
| `{LICENSE}` | SPDX identifier read from the license file | URL-encoded |
| `{IDENTITY_BADGES}` | `badge-styles.md` identity group | Max 5 |
| `{TECH_BADGES}` | `badge-styles.md` stack group | Max 6 |
| `{LANGUAGE_SWITCHER}` | Section below | Omit the whole `<p>` when single-language |

### Rules

1. Wrap the whole Hero in a single `<div align="center">` — not separate `<p align="center">`
   blocks. One container, consistent spacing.
2. Place `<a name="readme-top"></a>` immediately inside the container so back-to-top links
   work.
3. **Title uses `<h1>`, not Markdown `#`** — the header must sit inside the centered
   container. This is the one permitted deviation from "headings stay Markdown".
4. Provide **alt text for the logo** — usually the project name.
5. **At most two CTA badges.** More dilutes each.
6. **Every badge and logo link must resolve.** Placeholder domains are rejected at gate G5.
7. **Omit any block with no content** — never leave an empty `<p>`.

### Badge color selection

| Situation | Approach |
|---|---|
| Project has a brand colour | Derive 3–4 badge colours from the brand palette |
| No brand colour | Use the house accent `3178C6` |
| Never | The shields.io per-badge defaults, which make the Hero look accidental |

Brand-palette badges make the Hero read as one designed artifact instead of a random
assortment. See `badges.md` → *Brand Palette Rule*.

### House accent

The default accent is **`3178C6`**, with CTA buttons at **`2E7D32`**. Use it whenever the
project has no discoverable brand colour. There is one accent for every project — the
structure and palette do not vary by project type.

Every badge carries a white label on its own colour, so each colour must clear **4.5:1 against
white**: `3178C6` is 4.53:1, `2E7D32` is 5.13:1. Bright web colours do not — `4CAF50`, the
green this file used to specify, sits at 2.78:1 and is now rejected at gate G4. Check a
candidate before use (`visual-design.md` → *Contrast*).

---

## Language Switcher

Two forms. Use Form A unless the project ships five or more languages.

### Form A — Text links

Chinese primary, English secondary — the default shape.

```html
<p>
  <strong>简体中文</strong> ·
  <a href="README.en.md">English</a> ·
  <a href="README.ja.md">日本語</a>
</p>
```

### Form B — Capsule badges (5+ languages only)

```html
<p>
  <a href="README.md"><img alt="简体中文" src="https://img.shields.io/badge/简体中文-d9d9d9"></a>
  <a href="README.en.md"><img alt="English" src="https://img.shields.io/badge/English-d9d9d9"></a>
  <a href="README.ja.md"><img alt="日本語" src="https://img.shields.io/badge/日本語-d9d9d9"></a>
</p>
```

### Rules

1. **The current language is plain text, not a link.** In `README.md` the primary language
   (`简体中文`) is not hyperlinked; in a secondary file, that secondary language is not
   hyperlinked.
2. **Label in the native language** — `简体中文`, not "Chinese". Endonyms are readable to
   the people who need them.
3. **Uniform grey** (`d9d9d9`) for capsule badges so the switcher does not compete with
   the Hero's brand colors.
4. **Separator is ` · `** (middot with surrounding spaces).
5. **Bidirectional.** Every file reaches every other file. Naming and localization rules:
   `language-guide.md`.
6. **Omit the block entirely** for a single-language project.

---

## Table of Contents

A jumpable index placed directly under the Hero. It tells the reader what the document
covers before they scroll, and gives every section a one-click target.

### Template

```markdown
## Table of Contents

- [<Section 1>](#<anchor-1>)
- [<Section 2>](#<anchor-2>)
```

### Rules

1. **List the major (`##`) sections only.** Subsections already appear in the reader's
   outline; repeating them makes the index long without adding a target.
2. **Link with real anchors.** An anchor is the heading lowercased with spaces replaced by
   hyphens; non-Latin headings keep their characters (`## 快速开始` → `#快速开始`). Every
   entry must resolve — gate G5.
3. **Place it immediately after the Hero**, before the first content section.
4. **Omit it below about five sections.** A short document's headings are already visible,
   so the index only adds noise.
5. **Collapse it** with the *Collapsible Block* template once it exceeds roughly fifteen
   entries, so the Hero area stays clean.
6. **Do not number the entries** unless the document is procedural.

### Anti-patterns

| Anti-pattern | Fix |
|---|---|
| An index of every `##` and `###` heading | Keep `##` only |
| A hand-typed, unlinked list of headings | Make every entry an anchor link |
| An index on a three-section README | Omit it |
| An entry whose anchor does not resolve | Re-derive the anchor from the actual heading |

---

## Link Pool

Collect every URL at the end of the file. The body then references keys.

### Body form

```markdown
[![Build][badge-ci]][link-ci]
[![Version][badge-npm]][link-npm]

<text using [inline links for prose][link-docs only when repeated]>
```

### Definition block

```html
<!-- LINKS & IMAGES -->

[badge-ci]: https://img.shields.io/github/actions/workflow/status/{owner}/{repo}/ci.yml?style=flat-square
[link-ci]: https://github.com/{owner}/{repo}/actions
[badge-npm]: https://img.shields.io/npm/v/{package}?style=flat-square
[link-npm]: https://www.npmjs.com/package/{package}
```

### Rules

1. **Every badge and image URL goes in the pool.** Prose links may stay inline when they
   appear once.
2. **Key naming**: `badge-<name>` for images, `link-<name>` for destinations.
3. **Place the pool at the file end**, after the license.
4. **Benefits**: the body stays scannable; swapping a URL or a locale is a single edit;
   diffs stay small.
5. In multi-language output, the pool is the **only** block that differs between language
   files (besides prose) — localization edits happen here.

---

## Collapsible Block

```html
<details>
<summary>{SUMMARY_TEXT}</summary>

{CONTENT}

</details>
```

### Rules

1. `<details>` without `<summary>` fails gate G4.
2. **Blank line after `<summary>` and before `</details>`** so inner Markdown renders.
3. Use for: long tables of contents, advanced usage, long configuration, FAQ entries,
   troubleshooting, license compliance scans.
4. **Never collapse primary content.** Features, Quick Start, and Architecture are always
   visible. Collapsing them fails gate G4.
5. **Summary text is descriptive**, not "Click here to expand".

### Where collapsing is encouraged

| Content | Why |
|---|---|
| Table of contents over ~15 lines | Keeps the Hero area clean |
| Advanced or rarely used configuration | First-time users do not need it |
| Troubleshooting / FAQ | Long, consulted selectively |
| Full API surface beyond the core set | Overflow from the API table |
| Compliance and scan reports | Complete but not decision-relevant |

---

## GFM Alerts

Use GitHub's native alert syntax — it renders as styled callouts, no HTML required.

```markdown
> [!NOTE]
> Useful context the reader should know.

> [!TIP]
> An optional improvement or a faster path.

> [!IMPORTANT]
> Something required for the setup to succeed.

> [!WARNING]
> A pitfall that will cause failure or data loss.

> [!CAUTION]
> A security, legal, or irreversible-action concern.
```

### Usage guide

| Alert | Use for | Example trigger |
|---|---|---|
| `[!NOTE]` | Neutral context | "This step is optional when using Docker" |
| `[!TIP]` | Better path | "Add `--watch` for hot reload" |
| `[!IMPORTANT]` | Requirement | "The inference server must run in a separate environment" |
| `[!WARNING]` | Pitfall | "Changing this resets the database" |
| `[!CAUTION]` | Security / legal / irreversible | "This tool must not be used for unauthorized access" |

### Rules

1. **Content on the line after the marker**, all lines prefixed with `>`.
2. **Maximum one alert per step.** Stacked alerts lose their signal.
3. **Place the alert before the command it qualifies**, not after.
4. **`[!CAUTION]` is mandatory** for tools whose misuse is illegal or harmful — remote
   access, network interception, scrapers, anything touching personal data. Place it
   directly below the Hero.
5. Do not use alerts for emphasis. They are for risk and requirement.

### Mandatory caution for sensitive tools

```markdown
> [!CAUTION]
> **Misuse disclaimer.** This software must not be used for unauthorized access,
> surveillance, or any activity that violates applicable law. The maintainers are not
> responsible for misuse.
```

---

## Dual-Theme Media

GitHub renders in light and dark mode. A hardcoded-background image breaks in one of them.

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="{DARK_URL}" />
  <source media="(prefers-color-scheme: light)" srcset="{LIGHT_URL}" />
  <img alt="{DESCRIPTIVE_ALT}" src="{FALLBACK_URL}" />
</picture>
```

### Rules

1. **Always provide `<source>` for both schemes plus a fallback `<img>`.**
2. **Use for**: architecture diagrams with dark backgrounds, star-history charts,
   contributor dashboards, sponsor walls, any chart with a baked background.
3. **Do not use for screenshots** of the product UI unless you have both variants.
4. **Alt text is required** on the fallback `<img>` — gate G6.
5. Common dual-theme sources:
   ```
   star-history:  https://api.star-history.com/svg?repos={owner}/{repo}&type=Date[&theme=dark]
   ```

---

## Demo Card Row

Three equal-width cards, each a visual plus a caption link.

```html
<table>
  <tr>
    <td width="33%" align="center">
      <a href="{LINK_1}"><img src="{IMAGE_1}" alt="{ALT_1}" /></a>
    </td>
    <td width="33%" align="center">
      <a href="{LINK_2}"><img src="{IMAGE_2}" alt="{ALT_2}" /></a>
    </td>
    <td width="33%" align="center">
      <a href="{LINK_3}"><img src="{IMAGE_3}" alt="{ALT_3}" /></a>
    </td>
  </tr>
  <tr>
    <td align="center"><a href="{LINK_1}">{CAPTION_1}</a></td>
    <td align="center"><a href="{LINK_2}">{CAPTION_2}</a></td>
    <td align="center"><a href="{LINK_3}">{CAPTION_3}</a></td>
  </tr>
</table>
```

### Rules

1. **Exactly three cells**, all populated with real assets. Two real plus one filler
   fails gate G4.
2. **Equal width** — `width="33%"` on each `<td>`.
3. **Every image has alt text** and every caption is a working link.
4. Pair with a fourth capability described in prose rather than a four-column row, which
   renders poorly on narrow viewports.
5. Prefer animated GIF/WebP under ~5 MB; larger assets should be linked, not embedded.

---

## Capability Card Row

A two-column grid for a handful of capabilities or highlights, when a plain list would read
as a wall. Use it sparingly — cards add weight, and a list is lighter.

```html
<table>
  <tr>
    <td width="50%" valign="top">
      <h4>{CAPABILITY_1}</h4>
      <p>{ONE_LINE_OUTCOME_1}</p>
    </td>
    <td width="50%" valign="top">
      <h4>{CAPABILITY_2}</h4>
      <p>{ONE_LINE_OUTCOME_2}</p>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h4>{CAPABILITY_3}</h4>
      <p>{ONE_LINE_OUTCOME_3}</p>
    </td>
    <td width="50%" valign="top">
      <h4>{CAPABILITY_4}</h4>
      <p>{ONE_LINE_OUTCOME_4}</p>
    </td>
  </tr>
</table>
```

### Rules

1. **Every cell carries real content** — a name and one clause. An empty cell fails gate G4.
2. **Four to six items.** Beyond six, a list reads better.
3. **Lead with the outcome**, exactly as a feature row would.
4. **Never let an icon carry the meaning alone.** The `<h4>` names the capability.
5. **Do not use it to pad.** Two capabilities are two bullets, not a two-cell grid.
6. **One card row per document.** Repeating the grid turns the page into a wall of boxes.

---

## Back to Top

For documents longer than roughly 200 lines.

```html
<a name="readme-top"></a>
```
placed in the Hero, and at the end of each major section:

```html
<div align="right">

[![Back to top][badge-top]](#readme-top)

</div>
```

with the pool definition:

```html
[badge-top]: https://img.shields.io/badge/-BACK_TO_TOP-151515?style=flat-square
```

### Rules

1. Place after **every major (`##`) section** in long documents, not after subsections.
2. Omit for short documents — the anchor adds noise without benefit.
3. The anchor target must exist exactly once (in the Hero).

---

## Kept as Markdown

These must **not** be converted to HTML. Converting them fails gate G4.

| Element | Why Markdown wins |
|---|---|
| Tables | Maintainable; renders reliably; supports alignment syntax |
| Lists | Maintainable; supports nesting and task lists |
| Code blocks | Syntax highlighting is lost in HTML |
| Mermaid | GitHub renders fenced Mermaid with a native viewer |
| Inline code | Sufficient styling; `<code>` adds nothing |
| Headings (except hero title) | Markdown headings get anchors and build the outline |
| Dividers | `---` is idiomatic and renders identically |
| Anchors | Markdown anchor syntax is stable across renderers |
| Blockquotes | GitHub styling is sufficient; GFM alerts are preferable for callouts |

---

## Upgrading an Existing README

When a README already contains HTML, apply these rules rather than rewriting wholesale.

### Detection order

1. **Marker check.** If `<!-- BEAUTIFIED -->` or a v2 marker is present, the file was
   produced by this skill — apply Upgrade Mode from `workflow.md` instead of raw
   conversion.
2. **Raw HTML scan.** Find any `<div align>`, `<p align>`, `<h1 align>` blocks.
3. **Classify** each block as Hero, switcher, card row, or stray HTML.

### Conversion rules

| Found | Action |
|---|---|
| Markdown Hero (`# Title`, `> desc`, badges) | Replace with the Hero Template |
| `<div align="right">` switcher | Replace with the canonical switcher (left of Hero, centered) |
| Scattered `<p align="center">` blocks | Merge into a single centered container |
| Inline badge URLs | Move into the link pool |
| HTML tables used as layout | Keep only for real card grids; convert content tables back to Markdown |
| HTML used for emphasis or colour | Remove; use bold or the alert syntax |
| `<div align="center">` wrapping body prose | Remove; body text is left-aligned |

### Preservation

- Never touch content inside `<!-- MANUAL-START -->` … `<!-- MANUAL-END -->`.
- Never move or delete manual sections to satisfy ordering.
- When converting a manual HTML block, preserve the text exactly — only the wrapper
  changes.

### Reporting

Emit a short list: blocks converted, blocks preserved, blocks removed and why.
