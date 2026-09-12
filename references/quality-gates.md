# Quality Gates

Seven gates run in Phase 3. A README ships only after every applicable gate passes or its
failure is explicitly reported.

---

## Gate Index

| Gate | Name | Blocks delivery? |
|---|---|---|
| G1 | Evidence | Yes |
| G2 | Structure | Yes |
| G3 | Voice | Yes |
| G4 | Visual | Yes |
| G5 | Links | Yes |
| G6 | Accessibility | Yes |
| G7 | i18n | Only when multiple languages |

---

## G1 — Evidence

**Question:** can every factual assertion be traced to a source?

### Check

Walk the document and list every assertion of these kinds:

- a feature description
- a command
- a version number or requirement
- a port, path, variable name or default value
- a performance or coverage claim
- a compatibility claim
- a license

For each, locate the matching row in the evidence map.

### Fail conditions

- An assertion has no evidence row
- An assertion is `inferred` level but written as fact
- A version/port/default is stated without `declared` evidence
- A benchmark is quoted without a source in the repository

### Repair

| Case | Action |
|---|---|
| Claim has no source, but the fact is minor | Delete the claim |
| Claim has no source and the section depends on it | Delete the section |
| Vague claim with a source | Replace with the source's concrete value |
| Inferred claim | Add hedging language |

**Never** invent a source to satisfy this gate.

---

## G2 — Structure

**Question:** does the document follow the one fixed section order?

### Check

1. Read the fixed section order from `SKILL.md`.
2. Confirm every section that has scan data is present.
3. Confirm the present sections appear in the fixed order, with nothing reordered.
4. Confirm no section outside the fixed list was invented.
5. Confirm every absent section genuinely had no data in the evidence map.

### Fail conditions

- A section with data is missing
- Sections appear out of the fixed order
- A section outside the 20 was invented
- A section was dropped despite having evidence

### Repair

| Case | Action |
|---|---|
| Section has data but is missing | Author it |
| Sections out of order | Reorder them; never rename a section to fit the order |
| Invented section | Remove it, or fold its content into the closest listed section |
| Section present with no evidence | Delete it — gate G1 takes precedence |

---

## G3 — Voice

**Question:** is the house style applied, and is the text free of banned phrases?

### Check

1. Confirm the house style from `references/writing-style.md` is applied throughout.
2. Scan for every banned phrase in that file.
3. Confirm no emoji in prose and no exclamation marks anywhere.
4. Confirm sentence-length variety (no wall of identical-length sentences).
5. Confirm no absolute claim without evidence ("the fastest", "100% secure").
6. Confirm parallel structure within each list.

### Banned phrase master list

> powerful · robust · versatile · leverages · seamlessly · cutting-edge · comprehensive ·
> state-of-the-art · ever-evolving landscape · game-changing · revolutionary ·
> next-generation · best-in-class · enterprise-grade · blazingly fast · world-class ·
> turnkey · synergy · effortless · unleash · supercharge · battle-tested · one-stop ·
> production-ready (unless citing sourced production usage)

Plus:

> emoji in prose · exclamation marks · awesome · cool · amazing · love · hate · super ·
> simply · just · easy · straightforward · obviously · of course · as you can see ·
> note that · it's worth mentioning · we believe · unsourced comparisons ·
> unsourced security or compliance claims

The authoritative list lives in `references/writing-style.md`.

### Repair

Rewrite the sentence. Prefer the concrete value over the adjective:
"Handles 10k req/s" over "blazingly fast", "Uses JWT with RS256" over "secure".

---

## G4 — Visual

**Question:** is the layout compliant and are templates unmodified?

### Check

1. **Hero present and compliant** — centered container, logo, one-line description,
   subtitle, primary badges, language switcher. Template must match
   `hero-and-html.md` exactly; no invented variants.
2. **Badge grouping** — follows the group definitions and caps in `badge-styles.md`. No
   badge in the wrong group. No conditional badge without its data.
3. **Badge count within each group's cap.**
4. **Every badge URL resolves** to a real shields.io pattern (no `{PLACEHOLDER}` left).
5. **Diagrams** — every Mermaid block declares `classDef` and applies `class`. No
   colorless diagram.
6. **Collapsibles** — every `<details>` has a `<summary>`.
7. **Link pool** — all URLs in the pool, body uses reference form.
8. **Alerts** — every `> [!NOTE]` / `[!TIP]` / `[!WARNING]` / `[!CAUTION]` has content on
   the following line.

### Fail conditions

- Hero deviates from the template
- Placeholder tokens remain (`{PROJECT_NAME}`, `{COLOR}`, `TODO`)
- A diagram has no color classes
- A badge group exceeds its maximum
- A conditional badge appears without data

### Repair

Re-render the region from the source template. Never hand-edit a template into a new shape.

---

## G5 — Links

**Question:** do all links resolve and contain no placeholders?

### Check

| Link type | Verification |
|---|---|
| Relative file link (`LICENSE`, `CONTRIBUTING.md`, `docs/x.md`) | File exists in the scan |
| Relative anchor (`#quick-start`) | Target heading exists in this file |
| Cross-file anchor (`docs/x.md#y`) | File exists and heading likely present |
| External URL | Well-formed, not a placeholder domain |
| Badge URL | Matches a shields.io pattern |
| Image URL | Well-formed; alt text present (also G6) |

### Fail conditions

- A relative file link points to a file the scan did not find
- An anchor has no matching heading
- `example.com`, `your-domain.com`, `TODO`, `#` used as a real link target
- A link to a `docs/` page that does not exist

### Repair

| Case | Action |
|---|---|
| Link target missing but section is valuable | Replace with the closest existing file, or remove the link and keep the prose |
| Anchor missing | Point at the section heading that does exist |
| Placeholder domain | Remove the link or replace with a real detected URL |

---

## G6 — Accessibility

See `accessibility.md` for the full rules. Gate checks:

1. Every `<img>` and `![alt]()` has non-empty, descriptive alt text. Decorative images
   use `alt=""` deliberately.
2. Every Markdown table has a header row.
3. Every table has no empty header cells.
4. Colour is never the only carrier of meaning (a red badge must also carry text).
5. Heading levels are not skipped (no `##` → `####`).
6. Link text is descriptive — no bare "click here" / "here".
7. Emoji are not the sole label for a feature; text accompanies every icon.

### Repair

Add the missing alt text or header row. If alt text cannot be written meaningfully, the
image is decorative — set `alt=""`.

---

## G7 — i18n

Runs only when more than one language file is produced.

### Check

1. A switcher exists in **every** file, including the primary.
2. The switcher is **bidirectional**: from `README.zh-CN.md` you can reach `README.md`
   and every sibling; from `README.md` you can reach every sibling.
3. The current language is **not** a link in its own file.
4. Locale codes use BCP 47 form (`zh-CN`, `pt-BR`), not ad-hoc forms.
5. **Structure mirrors**: same heading sequence in every language.
6. **Code blocks are identical** across languages — commands are never translated.
7. **Localization applied**: links mapped per `language-guide.md`; local platform and
   community links present where the policy requires them.
8. If a translation is knowingly out of date, a status banner is present at the top.

### Fail conditions

- Switcher missing in a secondary file
- Current language rendered as a link
- A command translated
- Heading counts differ between languages
- Chinese file links to the English docs site when a Chinese one exists

### Repair

Fix the switcher, restore the command, re-align headings. If a language file cannot be
fully synchronized, add the anti-stale banner rather than shipping a silent mismatch.

---

## Result Report Format

```
Quality gates
─────────────────────────────────────
G1 Evidence        pass        (24 rows, 0 unbound)
G2 Structure       pass        (13 sections, fixed order)
G3 Voice           pass        (2 phrases rewritten)
G4 Visual          pass
G5 Links           pass
G6 Accessibility   repaired    (3 alt texts added)
G7 i18n            pass        (en, zh-CN — switcher bidirectional)
─────────────────────────────────────
```

If a gate cannot be repaired, state it plainly:

```
G5 Links           FAIL        (docs/advanced.md not found in scan — link removed)
```
