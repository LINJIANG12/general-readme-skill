# Accessibility

Rules that gate G6 enforces. A README that cannot be parsed by a screen reader, or that
carries meaning only in colour, excludes readers.

---

## Table of Contents

- [Why This Matters Here](#why-this-matters-here)
- [Alt Text](#alt-text)
- [Tables](#tables)
- [Links](#links)
- [Emoji and Icons](#emoji-and-icons)
- [Colour](#colour)
- [Heading Structure](#heading-structure)
- [HTML Specifics](#html-specifics)
- [Right-to-Left Languages](#right-to-left-languages)
- [Pre-Delivery Checklist](#pre-delivery-checklist)

---

## Why This Matters Here

README files are read in many contexts: screen readers, terminal Markdown viewers,
`curl` output, LLM ingestion, and rendered web. Anything that encodes meaning in a visual
channel alone is lost in most of them.

Rules in this file are not stylistic preferences — they are gate G6 checks.

---

## Alt Text

### Informative images

Every image that carries meaning needs descriptive alt text.

| Image | Good alt | Bad alt |
|---|---|---|
| Project logo in the Hero | `Vector database for similarity search` or the project name | `logo`, `banner`, `image` |
| Architecture screenshot | `Agent builder with a tool-selection panel open` | `screenshot` |
| Star history chart | `Star history for project-x, rising from 0 to 42k over three years` | `star history` |
| Product demo GIF | `Creating a workflow by dragging a node onto the canvas` | `demo` |
| Adopter logo | `Acme Corp` | `logo1` |
| Sponsor logo | `Sponsor: Acme` | `sponsor` |

### Decorative images

A purely decorative flourish takes empty alt text, deliberately:

```html
<img src="divider.svg" alt="" />
```

Never omit the `alt` attribute entirely — an absent attribute makes a screen reader
announce the file name.

### Badge alt text

Badges are informative when they carry a version, status or licence.

```html
<img alt="npm version 2.4.1" src="https://img.shields.io/npm/v/package" />
<img alt="Build passing" src="https://img.shields.io/github/actions/workflow/status/..." />
```

Writing a full alt for every badge is verbose in raw Markdown. Two acceptable positions:

| Approach | Form | When |
|---|---|---|
| Descriptive alt | `![npm version](url)` | Preferred — shields.io supplies a default if omitted, but write it explicitly when the value matters |
| Reference form | `[![npm version][badge-npm]][link-npm]` | When using the link pool; the alt is the first set of brackets |

### Animated media

A GIF or video must have alt text describing the **action**, not the files:

- Good: `Dragging a node onto the workflow canvas and connecting it to a model node`
- Bad: `demo.gif`

When the animation conveys a long sequence, also state what it demonstrates in prose —
alt text should be short.

---

## Tables

1. **Every table has a header row.** A table without one fails gate G6.
2. **No empty header cells.** Use a meaningful label, or drop the column.
3. **Alignment markers are fine** (`:---:`) and do not affect accessibility.
4. **Do not use a table purely for layout** — except the card-row pattern in
   `hero-and-html.md`, which has a documented justification. A layout table must have
   meaningful cell content, not decorative placeholders.
5. **One idea per cell.** Dense multi-line cells are hard to follow with a screen reader.
6. **Header text should be a noun phrase**, not a verb phrase — `Variable`, not
   `What you set here`.

### Bad

```
| | | |
|---|---|---|
| a | b | c |
```

### Good

```
| Variable | Description | Default |
|---|---|---|
| `PORT` | HTTP listen port | `3000` |
```

---

## Links

1. **Descriptive link text.** Never `click here`, `here`, `this link`, or a bare URL.
   - Good: `See the [migration guide](link)`
   - Bad: `For the migration guide, [click here](link)`
2. **Multiple links with the same text must differ** — a screen-reader user navigating by
   link text cannot distinguish three links all labelled "docs".
3. **A bare URL must be the actual destination**, not a shortener.
4. **Do not use the URL as link text** unless the URL itself is information.
5. **Icon-only links need `aria-label` or adjacent text.**

```html
<!-- Good -->
<a href="https://discord.gg/x" aria-label="Join the Discord community">
  <img src="discord.svg" alt="" />
</a>

<!-- Bad — a screen reader announces the file name or nothing -->
<a href="https://discord.gg/x"><img src="discord.svg" /></a>
```

---

## Emoji and Icons

1. **No emoji in prose.** The house style in `writing-style.md` bans emoji in headings, lists,
   tables and section intros. Do not introduce one to "lighten" a passage.
2. **Badge logos are images, not emoji.** Shields.io badges and brand logos are unaffected by
   the emoji rule, but each still needs a text alt or a readable label.
3. **Never let a symbol carry meaning alone.** Any surviving icon must sit beside words that
   say the same thing.
   - Good: `![Scoped tokens](…)` next to `**Scoped tokens**` — the badge decorates, the words
     carry the meaning
   - Bad: a table whose header is `🔒`
4. **Avoid symbol chains as separators.** A run of glyphs like `✅✅❌✅` carries meaning only
   visually.
5. **A screen reader reads emoji names aloud.** An emoji on every list item makes the list
   tedious — one more reason to keep them out of prose entirely.

---

## Colour

1. **Never the only carrier of meaning.** A red badge meaning "failing" must also say
   "failing".
2. **Badge colour is decoration**, not semantics. `![Build failing](red-badge)` is fine;
   a red-grey colour pair distinguishing "supported" from "unsupported" without labels is
   not.
3. **Do not rely on coloured text** — Markdown has no colour support anyway, and any HTML
   colour usage fails gate G4.
4. **Contrast in custom SVG**: text on a coloured fill must use white or near-black. The
   diagram palette in `diagram-templates.md` already pairs white text with dark fills.
5. **Dual-theme media is mandatory** for charts with baked backgrounds — a light-background
   chart on a dark GitHub theme is both unreadable and, for low-vision readers, a contrast
   failure.

---

## Heading Structure

1. **No skipped levels.** `##` → `####` without an intervening `###` breaks outline
   navigation. (The Hero `<h1>` is the sole permitted HTML heading.)
2. **One `<h1>` per document** — the Hero title. Body sections start at `##`.
3. **Headings describe content, not position.** `## Configuration`, not `## Next Section`.
4. **No empty headings.** A heading with no content underneath is removed.
5. **Anchor-generating headings must be unique.** Two `## Usage` sections produce
   ambiguous anchors and break the back-to-top links.
6. **Do not style a heading with bold text.** `**Configuration**` is not a heading and will
   not appear in the outline or receive an anchor.

---

## HTML Specifics

| Element | Requirement |
|---|---|
| `<img>` | Non-empty or deliberately empty `alt` |
| `<a>` wrapping only an image | Add `aria-label` or ensure the image `alt` describes the destination |
| `<table>` used for cards | Populate every cell with real content |
| `<details>` | Requires `<summary>`; summary describes the content |
| `<picture>` | The fallback `<img>` carries the alt text |
| `<div align="center">` | Layout only — never wrap body prose, which should stay left-aligned |

Semantic HTML is preferred over presentational HTML, but GitHub sanitises most attributes.
Where a semantic element is unavailable, achieve accessibility through alt text and
adjacent prose.

---

## Right-to-Left Languages

Applies when generating `README.ar.md`, `README.he.md`, `README.fa.md`, or similar.

1. **Code blocks and commands stay left-to-right.** Never mirror a code fence.
2. **Mixed-direction lines** (an English identifier inside RTL prose) can render
   incorrectly. Wrap such runs in `<bdi>` when the ambiguity is real:
   ```html
   <bdi>README.md</bdi>
   ```
3. **Tables** in RTL locales: keep the structural order the same as other locales so the
   files stay diffable, unless the project's convention differs.
4. **Punctuation** follows the target language's convention. Do not carry English commas
   into Arabic prose.
5. **URLs and file paths remain unchanged.**
6. **The language switcher stays centred** — alignment is a layout choice, not a
   direction-dependent one.

---

## Pre-Delivery Checklist

Gate G6 verifies these. Run before Phase 4.

- [ ] Every `<img>` and `![]()` has descriptive alt text, or a deliberate `alt=""`
- [ ] Badge alt text states the value where the value matters
- [ ] Every table has a header row with no empty cells
- [ ] No meaning carried by colour alone
- [ ] No heading level skipped
- [ ] Headings unique and descriptive
- [ ] No bare "click here" / "here" link text
- [ ] Icon-only links have `aria-label` or adjacent text
- [ ] Emoji never the sole label for a feature
- [ ] Emoji used consistently or not at all within a section
- [ ] Chart images use the dual-theme pattern
- [ ] `<details>` blocks all have `<summary>`
- [ ] RTL considerations applied if an RTL locale is generated
