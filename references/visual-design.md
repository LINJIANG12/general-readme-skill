# Visual Design

`writing-style.md` governs what the words say. This file governs how the page looks. It is
part of the house style and is not configurable.

Read it before composing, and run its checklist as part of gate G4.

---

## Table of Contents

- [Why Generated Docs Look Templated](#why-generated-docs-look-templated)
- [The Five Levers](#the-five-levers)
- [Contrast](#contrast)
- [Accent](#accent)
- [Rhythm](#rhythm)
- [Density](#density)
- [Attention Budget](#attention-budget)
- [Ownership](#ownership)
- [Checklist](#checklist)

---

## Why Generated Docs Look Templated

A generated README usually fails visually for one reason: **every section has the same
shape.** Heading, table, rule. Heading, table, rule. Nothing tells the eye where to rest, so
nothing reads as important.

| Cause | Symptom |
|---|---|
| One form for everything | A table in every section, including where prose or a list reads better |
| Every colour equally loud | A seven-hue diagram; a badge for everything; bold in every other line |
| No negative space | `---` between every section, headings touching tables, no lead-in line |

The fix is not decoration. It is **restraint plus variation**: one accent against many
neutrals, and a different form in each adjacent section.

---

## The Five Levers

| Lever | One-line rule |
|---|---|
| **Contrast** | Every text-on-colour pair is a verified pair. Never assume — compute |
| **Accent** | One accent hue per document, and at most three roles per diagram |
| **Rhythm** | Adjacent sections never open with the same form |
| **Density** | Caps on paragraphs, lists and tables. Depth material goes into `<details>` |
| **Focal point** | One thing per screen-height earns attention. Spend it deliberately |

---

## Contrast

Colour is the one visual property that can be *measured*, so it is not a matter of taste.
Every text-on-colour pair in the document must clear these thresholds:

| Text | Minimum ratio | Standard |
|---|---|---|
| Body-size text in a diagram node, HTML block or table | **4.5:1** | WCAG 2.1 AA |
| Large text (≥18.66px bold, or ≥24px) | 3:1 | WCAG 2.1 AA |
| Borders, arrows, and any non-text shape boundary, against the page | 3:1 | WCAG 2.1 AA |
| Target for anything the skill generates | **7:1** | WCAG 2.1 AAA |

### How to check

Relative luminance, per WCAG 2.1:

```
c  = channel / 255
lin = c / 12.92                     if c <= 0.04045
lin = ((c + 0.055) / 1.055) ^ 2.4   otherwise
L  = 0.2126·R + 0.7152·G + 0.0722·B
ratio = (L_lighter + 0.05) / (L_darker + 0.05)
```

### Rules

1. **Never pair white text with a mid-saturation fill.** A 500-level brand colour behind
   white text lands between 2:1 and 4.2:1 — it fails AA for any label the reader must read.
   This is the most common defect in generated diagrams.
2. **Use a verified pair or nothing.** The palette in `diagram-templates.md` is pre-computed
   to satisfy the 7:1 target. Do not substitute a hue of your own.
3. **Colour never carries meaning alone.** A red node must also say what it means
   (`accessibility.md` → *Colour*).
4. **Do not state a contrast claim you have not computed.** If a reference asserts a pair is
   safe, verify it before repeating the assertion.

---

## Accent

1. **One accent hue per document.** The Hero's badge colours are the exception — they come
   from the badge matrix, not from taste.
2. **At most three roles per diagram**, plus Neutral. A diagram with seven equally loud fills
   reads as a colour chart, not an architecture.
3. **At most one focal element per diagram** — the single node the section is about, drawn
   solid. Everything else is a tint.
4. **Emphasis is a budget.** At most one bold run per paragraph, one bold column per table,
   and never negative for an entire sentence.
5. **No decorative colour.** There is no "accent for pretty" — if a colour does not
   distinguish a role the reader needs, delete it and use Neutral.

---

## Rhythm

The reader's eye needs variety to navigate. A document where every section has one shape is
unreadable however correct each section is.

1. **Adjacent sections must not be built on the same block type.** Two neighbouring sections
   cannot both turn on a table, or both on a diagram, a code block or an image. Prose is never
   the "built on" type — it is the connective tissue, so two prose-led sections are fine.
   A section built on a table is followed by one built on prose, a list, code, an image or a
   diagram.
2. **At most one table per section**, except in reference sections (`API`, `Commands`,
   `Configuration`, `Tech Stack`) where a table is the content.
3. **A table or list gets a lead-in line** when its columns are not self-evident. One
   sentence, then the block.
4. **Default to no horizontal rule.** Whitespace already separates sections on GitHub; a rule
   between every section is noise. At most one `---`, placed where the document changes
   register — for example before the licence.
5. **Vary block length.** Three short sections and one long one reads better than four equal
   ones.
6. **Do not repeat a footer device.** A "back to top" link on every section is noise; one at
   the end is enough.

---

## Density

Caps exist because most README reading happens on a phone.

| Element | Cap |
|---|---|
| Paragraph | 3 lines, or roughly 240 CJK / 280 Latin characters |
| Sentence | One idea. Split at ~40 CJK / ~30 Latin words |
| List | 3–7 items; 8+ means split it or collapse it |
| Table columns | 4 (5 only for a reference table, and it must still be readable at 375px) |
| Table cell | ~40 CJK / ~60 Latin characters |
| Code block | 12 lines, unless reproducing a real file |
| Bold run | 1 per paragraph |
| Section before depth material | 3 blocks, then a `<details>` |

### Rules

1. **Depth goes into `<details>`.** A section's first screen is for the reader who is deciding;
   the reference detail is for the reader who has decided.
2. **A two-column table whose second column is a sentence is a list.** Use the list.
3. **Do not bold the label and then also bold the value.** One of the two.
4. **Trim, do not compress.** If a cell needs 80 characters, the table is the wrong form.
5. **One term per concept, everywhere.** Never alternate `技能` with `工具`, or `扫描` with
   `Scan`, within one document.

---

## Attention Budget

Per screen-height, roughly one element may ask for attention. Three at once means none of them
gets it.

1. **Alerts are the accent, not the default.** At most one alert per three sections, and only
   for a genuine trap. Never `[!NOTE]` as decoration. Pick the type that matches the stakes
   and follow the alert rules in `hero-and-html.md`.
2. **A diagram earns its place** only when the structure is genuinely non-linear or the
   relationship is hard to say in a sentence. A five-step list does not need a flowchart.
3. **One image per idea.** Two adjacent screenshots need captions explaining the difference,
   or one of them should go.
4. **Set image width explicitly** when the source is wider than the column, so the reader is
   not made to scroll a screenshot sideways.
5. **Media with a baked background needs a dark/light pair** (`accessibility.md` → *Colour*).

---

## Ownership

Read the owning reference rather than restating it:

| Region | Owner |
|---|---|
| Hero, HTML blocks, alerts, collapsibles, link pool | `hero-and-html.md` |
| Badge groups, caps and style | `badge-styles.md`, `badges.md` |
| Diagram palette values, diagram templates | `diagram-templates.md` |
| Contrast thresholds, accent, rhythm, density, budget | **this file** |
| Alt text, table headers, RTL, dark/light media | `accessibility.md` |
| Form choice per section (table vs list vs prose) | `writing-style.md` → *The Right Form* |

---

## Checklist

Run as part of gate G4.

- [ ] No white text on a mid-saturation fill anywhere
- [ ] Every colour pair comes from the verified palette
- [ ] At most three roles and one focal node per diagram
- [ ] No two adjacent sections open with the same form
- [ ] At most one table per non-reference section
- [ ] `---` used sparingly, not between every section
- [ ] Paragraph, list, table-column and code-block caps respected
- [ ] Table columns ≤ 4 and readable at 375px
- [ ] Alerts ≤ 1 per 3 sections, correct type, content on the next line
- [ ] One bold run per paragraph
- [ ] Images sized explicitly; baked-background media has a dark/light pair
- [ ] One term per concept across the whole document
- [ ] No repeated "back to top" footer on every section
