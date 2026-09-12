# Social Proof

Templates and rules for the sections that build trust, credit contributions, and sustain
the project: sponsors, adopters, contributors, citations, and traction charts.

Read alongside `sections-growth.md`, which covers when each section is warranted.

---

## Table of Contents

- [Principles](#principles)
- [Contributor Wall](#contributor-wall)
- [Sponsor Grid](#sponsor-grid)
- [Tiered Sponsor Wall](#tiered-sponsor-wall)
- [Adopter Wall](#adopter-wall)
- [Testimonial Block](#testimonial-block)
- [Citation Block](#citation-block)
- [Dual-Theme Star Chart](#dual-theme-star-chart)
- [Acknowledgments Block](#acknowledgments-block)

---

## Principles

1. **Verifiable or absent.** Every logo, quote and statistic must be checkable. An
   unverifiable claim is deleted, not softened. Gate G1 applies here most strictly — this
   is the section most likely to be fabricated.
2. **Attributed, not anonymous.** "Used by leading companies" is worthless. Name the
   company, link the source.
3. **Below the pitch.** Social proof supports the technical content; it never replaces it.
   Place these sections after the technical body.
4. **Growth loop where possible.** Adopter and contributor walls should invite the next
   entry, not just display the current set.
5. **No emoji as the only signal.** A trophy emoji without text fails gate G6.

---

## Contributor Wall

Automated, zero-maintenance attribution.

### Dynamic image (preferred)

```html
<a href="https://github.com/{owner}/{repo}/graphs/contributors">
  <img alt="Contributors to {project}" src="https://contrib.rocks/image?repo={owner}/{repo}" />
</a>
```

### Rules

1. **Use the automation.** A hardcoded contributor list goes stale within a week.
2. **Alt text names the project** — `Contributors to <project>`.
3. **Place near the end**, after the technical sections and near Contributing.
4. **Do not enumerate contributor names in prose.** T1 projects may state a count read
   from a `CONTRIBUTORS` / `AUTHORS` file: `Contributors: 3 (Alice, Bob, and 1 other)` —
   names only, never emails.
5. **When git metadata is unavailable**, omit rather than fabricate.

---

## Sponsor Grid

For a small, flat set of sponsors (T3, or a funded project with fewer than ~8 sponsors).

```html
<!-- sponsors -->

<div align="center">

<a href="{SPONSOR_URL_1}"><img src="{LOGO_1}" alt="{SPONSOR_1}" width="160" /></a>
<a href="{SPONSOR_URL_2}"><img src="{LOGO_2}" alt="{SPONSOR_2}" width="160" /></a>
<a href="{SPONSOR_URL_3}"><img src="{LOGO_3}" alt="{SPONSOR_3}" width="160" /></a>

</div>

<!-- /sponsors -->
```

### Rules

1. **Wrap in the placeholder comments** so an automation script can rewrite the block.
2. **Every logo has alt text** with the sponsor's name — an image-only logo fails gate G6.
3. **Every logo links** to the sponsor's site.
4. **Do not list a sponsor the funding configuration does not contain.**
5. **Omit the entire section when there are no sponsors.** An empty sponsor block is worse
   than none.
6. **Update cadence**: this block should be regeneratable by a scheduled job. Keep it
   isolated so regeneration is a no-op elsewhere.

---

## Tiered Sponsor Wall

For projects with a formal tier structure.

```html
<!-- sponsors -->

### Keystone

<div align="center">

<a href="{URL}"><img src="{LOGO}" alt="{NAME}" width="360" /></a>

</div>

### Gold

<div align="center">

<a href="{URL}"><img src="{LOGO}" alt="{NAME}" width="200" /></a>
<a href="{URL}"><img src="{LOGO}" alt="{NAME}" width="200" /></a>

</div>

### Silver

<div align="center">

<a href="{URL}"><img src="{LOGO}" alt="{NAME}" width="130" /></a>
<a href="{URL}"><img src="{LOGO}" alt="{NAME}" width="130" /></a>
<a href="{URL}"><img src="{LOGO}" alt="{NAME}" width="130" /></a>

</div>

<!-- /sponsors -->
```

### Rules

1. **Descending size by tier** — the hierarchy must be visible without reading labels.
2. **Tier names come from the project's funding configuration**, not invented.
3. **Dark-mode-adaptive logos** where the sponsor provides them, via the dual-theme
   pattern in `hero-and-html.md`.
4. **Keep the number per tier readable** — beyond ~5 logos, link to a dedicated sponsors
   file rather than expanding the README.
5. **Order within a tier is not a ranking** — do not imply favouritism.

---

## Adopter Wall

Companies or projects that use this software. This section is a growth loop, not a static
display.

```html
## Adopters

Projects and organisations using {PROJECT}. Add yours via the
[registration issue]({ISSUE_URL}).

<table>
  <tr>
    <td align="center" width="20%"><a href="{URL_1}"><img src="{LOGO_1}" alt="{NAME_1}" width="140" /></a></td>
    <td align="center" width="20%"><a href="{URL_2}"><img src="{LOGO_2}" alt="{NAME_2}" width="140" /></a></td>
    <td align="center" width="20%"><a href="{URL_3}"><img src="{LOGO_3}" alt="{NAME_3}" width="140" /></a></td>
    <td align="center" width="20%"><a href="{URL_4}"><img src="{LOGO_4}" alt="{NAME_4}" width="140" /></a></td>
    <td align="center" width="20%"><a href="{URL_5}"><img src="{LOGO_5}" alt="{NAME_5}" width="140" /></a></td>
  </tr>
</table>
```

### Rules

1. **The registration call to action is mandatory.** Without it the section cannot grow —
   that is its entire purpose. Link a tracking issue or a documented submission process.
2. **Every entry must be verifiable.** Either the company publicly states usage or there is
   a case study. When in doubt, omit the entry.
3. **Link each entry** to the company site or the specific project.
4. **Alt text carries the company name.**
5. **Cap at ~10–15 entries.** Beyond that, link `ADOPTERS.md`.
6. **Do not use a company logo without a basis.** Fabricating adopters is a legal and
   reputational risk, not merely a documentation error.

---

## Testimonial Block

Short quotes from named engineers at identifiable organisations.

```markdown
> "{Quote, one to three sentences, concrete about what changed.}"
>
> — **{Name}**, {Role}, [{Company}]({SOURCE_URL}) <a href="{SOURCE_URL}"><small>(source)</small></a>
```

### Rules

1. **Every quote carries a source link.** A quote without a traceable source is deleted —
   this is gate G1 applied to testimonials.
2. **Named role and company.** Anonymous quotes carry no weight.
3. **Concrete over effusive.** "Cut p99 latency from 400 ms to 90 ms" beats "amazing
   project".
4. **Maximum three.** A wall of praise reads as marketing.
5. **Explicit permission implied** — quote from public sources only (conference talks,
   published blog posts, public issue threads).

---

## Citation Block

For projects with academic standing.

```markdown
## Citation

If you use {PROJECT} in research, cite it as:

```bibtex
@{type}{{key},
  title        = {{Title}},
  author       = {{Author, A. and Author, B.}},
  year         = {2025},
  journal      = {{Journal}},
  doi          = {10.xxxx/xxxxx}
}
```

[Paper]({PAPER_URL}) · [DOI]({DOI_URL})
```

### Rules

1. **Use the project's canonical citation** — read `CITATION.cff` or the documented
   reference. Never compose a citation from inference.
2. **Fence as `bibtex`** for rendering.
3. **Include the DOI or paper link.**
4. **Omit when no citation exists.** Inventing one is worse than omitting the section.
5. Common in: Infrastructure, AI App, Knowledge Base, and any project with a published
   paper.

---

## Dual-Theme Star Chart

Traction visualisation that works in both GitHub themes.

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos={owner}/{repo}&type=Date&theme=dark" />
  <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos={owner}/{repo}&type=Date" />
  <img alt="Star history for {project}" src="https://api.star-history.com/svg?repos={owner}/{repo}&type=Date" />
</picture>
```

### Rules

1. **The dual-theme form is mandatory.** A hardcoded light chart is unreadable in dark mode
   — gate G4.
2. **Read owner and repo from the scan.** Never a placeholder.
3. **Place near the end**, above the license.
4. **Omit for low-traction repositories** — a flat line undermines the document.

---

## Acknowledgments Block

Credit upstream work honestly.

```markdown
## Acknowledgments

{PROJECT} builds on [{UPSTREAM}]({URL}), which provides the {capability}. The
{FEATURE} design follows the approach described in [{REFERENCE}]({URL}).
```

### Rules

1. **Name the substantial upstream dependencies** — the framework extended, the protocol
   implemented, the algorithm adopted.
2. **Attribute prior art** with a link, especially when the project was directly inspired
   by another.
3. **Prose, not a dependency dump.** The manifest already lists dependencies.
4. **Credit translators** for multi-language projects — a short list of locale
   contributors, sourced from translation config rather than invented.

---

## Placement Guide

Recommended order at the end of a T3 document:

```
... technical sections ...
## Roadmap
## FAQ
## Community
## Contributing
## Sponsors
## Adopters
## Acknowledgments
## Citation
## Star History
## License
```

Adjust per archetype, but keep the principle: **technical content first, social proof
after, license last.**
