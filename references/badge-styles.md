# Badge Styles

Badge appearance, grouping, and the per-tier budget. Technology → URL mapping lives in
`badges.md`; this file decides where each badge goes and how many are allowed.

---

## Table of Contents

- [Style Parameter](#style-parameter)
- [Grouping Model](#grouping-model)
- [Budget by Tier](#budget-by-tier)
- [Group Definitions](#group-definitions)
- [Layout Rules](#layout-rules)

---

## Style Parameter

One style applies to the whole document. Mixing `style=flat` with `style=for-the-badge` in
the same Hero fails gate G4.

| Style | Parameter | Character | Best for |
|---|---|---|---|
| **Flat** | `style=flat` | Compact, standard, neutral | Default for most projects |
| **Flat-square** | `style=flat-square` | Sharp edges, slightly denser | Developer tools, terminal-adjacent projects |
| **For-the-badge** | `style=for-the-badge` | Tall, bold, high impact | CTA badges only, or very visual projects |

### Rules

1. **Default is `flat`.**
2. **`for-the-badge` is for CTAs, not for the full matrix.** A row of eight tall badges
   consumes the entire viewport. Use it for the Quick Start and Licence buttons, then use
   the resolved style for everything else.
3. **Exception:** a project whose resolved style is `for-the-badge` applies it consistently.
4. **`flat-square` pairs well with a dense technical document** and poorly with a
   marketing-oriented Hero.
5. **The style parameter must be explicit** on static badges. Omitting it yields the
   shields.io default, which may differ from the chosen style.

---

## Grouping Model

Badges are grouped by **signal type**, and the groups appear in a fixed order. Ordering by
signal rather than by technology keeps the Hero scannable.

| Group | Question it answers | Placement |
|---|---|---|
| **Identity** | What is this and is it healthy? | Hero, first badge row |
| **Stack** | What is it built with? | Hero, second badge row |
| **Traction** | Is anyone using it? | Hero, third row (T3 only) |
| **Community** | Where do I talk to people? | Hero, final row, or the Community section |
| **Governance** | Who stands behind it? | Hero identity row, or the License section |

### Rules

1. **Groups render on separate lines.** A single 14-badge line is unreadable on narrow
   viewports.
2. **Never interleave groups.** A database badge in the identity row breaks the model.
3. **Order within a group is stable**: highest signal first.
4. **A group with no badges is omitted entirely** — no empty row, no placeholder.

---

## Budget by Tier

The tier from `profiles.md` caps the total. Exceeding the budget fails gate G2.

| Tier | Identity | Stack | Traction | Community | Governance | Total |
|---|---|---|---|---|---|---|
| **T1** | 3 | 3 | 0 | 0 | 0 | ≤ 5 |
| **T2** | 4 | 5 | 2 | 1 | 1 | ≤ 12 |
| **T3** | 5 | 6 | 3 | 3 | 2 | ≤ 18 |

### Rules

1. **The budget is a ceiling.** A T3 project with nothing to show in Traction omits that row.
2. **Identity row max 5** even at T3 — beyond that the Hero becomes a wall.
3. **Stack row max 6.** Pick the six that characterise the project; the rest live in the
   Tech Stack section.
4. **Traction badges require real numbers.** A stars badge on a repository with 40 stars is
   a negative signal — omit it.
5. **Community badges require a live channel.**
6. **Count badges, not rows.** Two rows of three is six badges.

---

## Group Definitions

### Identity

The minimum set that lets a reader judge project health.

| Badge | Condition | Priority |
|---|---|---|
| Build / CI status | A CI workflow exists | 1 |
| Release version | A registry package or releases exist | 2 |
| License | A licence file exists | 3 |
| Primary language | Always | 4 |
| Coverage | Coverage reporting is configured | 5 |

Omit any badge whose data does not exist. A static "build passing" badge with no CI is a
fabrication — gate G1.

### Stack

Drawn from the detected framework, database and infrastructure set.

| Priority | Source |
|---|---|
| 1 | Primary framework |
| 2 | Secondary framework (if central) |
| 3 | Database |
| 4 | Cache / queue |
| 5 | Container / orchestration |
| 6 | Language runtime version (if declared) |

Rules:

1. **Runtime stack only.** Exclude linters, formatters and test frameworks unless
   contributor tooling is central to the project's pitch.
2. **Exclude transitive dependencies.** A badge implies usage by the project.
3. **Cap at six.** The Tech Stack section carries the long tail.
4. **Keep official brand colours** — see `badges.md` → *Brand Palette Rule*.

### Traction

| Badge | Condition |
|---|---|
| Stars | Repository has meaningful traction — omit below roughly 500 stars |
| Downloads | Package is published and downloads are measurable |
| Docker pulls | An image is published |
| Contributors | A contributor count is available |
| Backers / sponsors | A funding configuration exists |

### Community

| Badge | Condition |
|---|---|
| Discord / Slack | A live invite link exists |
| WeChat / regional channel | A QR or link is documented |
| X / Mastodon / Reddit | An active account exists |
| Forum / Discussions | Discussions are enabled and used |

### Governance

| Badge | Condition |
|---|---|
| Foundation membership | CNCF, Apache, LF AI & Data, OpenSSF, or similar |
| Security policy | `SECURITY.md` exists |
| Code of conduct | `CODE_OF_CONDUCT.md` exists |
| Standards conformance | OpenAPI, OCI, SLSA, WCAG, or another published standard |
| Recognition | Product Hunt, Trendshift, or comparable |

---

## Layout Rules

### In the Hero

```html
<p>
  {IDENTITY_BADGES}
</p>

<p>
  {STACK_BADGES}
</p>

<p>
  {TRACTION_BADGES}
</p>

<p>
  {LANGUAGE_SWITCHER}
</p>
```

Each group is a separate `<p>` inside the Hero's centred container
(`hero-and-html.md` → *Hero Template*).

### Elsewhere in the document

1. **A badge may be repeated** in the section it belongs to — a build badge in both the
   Hero and the Contributing section is acceptable, but keep it to two appearances total.
2. **Section-local badges** use the same resolved style.
3. **A badge must never be the only content of a section.**
4. **No badge inside a code block.**

### Spacing

- One badge per source line in Markdown form, so the raw file stays readable.
- A blank line between groups.
- No badges inside list items.

### Reference form

Use the link pool (`hero-and-html.md` → *Link Pool*) for badges:

```markdown
[![Build][badge-ci]][link-ci]
[![Version][badge-version]][link-version]
[![License][badge-license]][link-license]
```

This keeps the badge definition next to its URL and makes a style change a single edit per
badge.

---

## Verification

Before Phase 4:

- [ ] One style parameter used throughout
- [ ] `for-the-badge` only on CTAs, unless it is the resolved style
- [ ] Groups rendered on separate lines, in the fixed order
- [ ] No group exceeds its maximum
- [ ] Total within the tier budget
- [ ] No badge without its underlying data
- [ ] Every dynamic badge references a real package or repository
- [ ] Every badge URL uses a valid shields.io pattern
- [ ] Stack badges retain official brand colours
- [ ] Traction badges omitted where the numbers would weaken the case
- [ ] All badge URLs present in the link pool
