# Section Recipes — Growth

Community, governance and sustainability sections. Each recipe is included only when the
scan finds the data it needs — see the include-when column in `SKILL.md`. Which sections are
present never affects their order.

`Contributing` and `Community` are one section in the fixed structure
(**Contributing & Community**). The two recipes below are written to be merged into it.

Section visuals (sponsor grids, star-history charts) come from `social-proof.md`.

---

## Table of Contents

- [Contributing](#contributing)
- [Community](#community)
- [Roadmap](#roadmap)
- [FAQ](#faq)
- [Changelog](#changelog)
- [Security](#security)
- [Sponsors](#sponsors)
- [Adopters](#adopters)
- [Acknowledgments](#acknowledgments)
- [Citation](#citation)
- [Star History](#star-history)
- [Comparison](#comparison)
- [License](#license)

---

## Contributing

**Purpose:** turn a reader into a contributor with the least friction.

**Include when:** `CONTRIBUTING.md`, issue templates, or community links exist.

Use the short form when the repository has only a contributing guide. Use the full form when
it also has a development workflow worth documenting.

### Short form

```
## Contributing

Issues and pull requests are welcome.

1. Fork the repository
2. Create a branch (`git checkout -b fix/thing`)
3. Commit (`git commit -m 'fix: correct thing'`)
4. Push and open a pull request
```

### Full form

```
## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide.

### Quick start

```bash
<clone, install, run the dev server — real commands>
```

### Good first issues

<label or link to the good-first-issue filtered view>

### Commit conventions

<only if a convention is declared in commitlint config or CONTRIBUTING.md>

### Ways to contribute without code

- Report a reproducible bug
- Improve documentation
- Answer questions in discussions
- Review open pull requests
```

### Rules

1. **Fork → branch → commit → push → PR**, in that order, as a numbered list.
2. **Include the local dev commands** when they exist in the manifest scripts — a
   contributor cannot fix a bug they cannot run.
3. **State the commit convention** only when one is declared. Do not impose one.
4. **Link `CONTRIBUTING.md`** when it exists instead of duplicating it.
5. **List non-code contributions** — documentation, triage, translation, support.
6. **Never open with "We welcome contributions!"** — open with the steps.
7. **Name the code of conduct** when `CODE_OF_CONDUCT.md` exists.

---

## Community

**Purpose:** tell people where to talk, and route each kind of question correctly.

**Include when:** a community channel is documented — Discussions, a chat invite, or a
forum link.

### Shape

```
## Community

| Channel | Purpose |
|---|---|
| GitHub Discussions | Questions, ideas, show-and-tell |
| GitHub Issues | Reproducible bugs and feature requests |
| Discord / Slack | Real-time chat |
| <local channel> | <regional community> |
```

### Rules

1. **Route explicitly.** Separate "ask a question" from "report a bug" from "chat". This
   protects the issue tracker.
2. **Only list channels that exist** in the repository config or official docs. A dead
   invite link fails gate G5.
3. **Point security issues away from public channels** — always to the Security section.
4. **Include regional channels** for the project's user base (see `language-guide.md`
   localization policy).
5. **State response expectations** only if the project publishes them.

---

## Roadmap

**Purpose:** show direction and let users plan.

**Include when:** a roadmap file, milestone configuration, or documented plan exists.

### Shape

```
## Roadmap

### Planned

| Version | Focus |
|---|---|
| v2.2 | Multi-tenant isolation |
| v2.3 | Plugin API |

### Under consideration

- <item with no committed version>
```

### Rules

1. **Source from a real roadmap file, milestone config, or documented plan.** Never invent
   future features from a code TODO.
2. **Separate committed from exploratory.** A reader must not treat "under consideration"
   as a promise.
3. **Link the tracking issue or milestone** for each item so the reader can follow it.
4. **Do not include a roadmap for an unmaintained project** — it reads as a broken promise.
5. If the project has no roadmap, omit the section rather than writing "TBD".

---

## FAQ

**Purpose:** pre-answer the questions the maintainers are asked most.

**Include when:** an FAQ document exists, or recurring questions are documented in issues
or discussions.

### Shape

```
## FAQ

<details>
<summary>Why does X behave differently from Y?</summary>

<answer, including the workaround if one exists>
</details>

<details>
<summary>Can I use this in production?</summary>

<answer>
</details>
```

### Rules

1. **Real questions only.** Source from `docs/FAQ.md`, a FAQ label, or documented issue
   themes. Never invent questions to fill the section.
2. **Use `<details>` collapsing** so a long FAQ does not dominate the document.
3. **Answer inside the block**, not with a link alone — the link is supplementary.
4. **5–10 entries maximum.** Beyond that, link to the full FAQ document.
5. **Never use FAQ to advertise.** It answers questions.
6. **Never answer with "yes" alone** — state the condition that makes it possible.

---

## Changelog

**Purpose:** point at what changed, without duplicating the changelog itself.

**Include when:** `CHANGELOG.md` exists, or releases are published with notes.

### Shape

```
## Changelog

Release notes are published on the [releases page](link).

This project follows [Semantic Versioning](https://semver.org/).
```

### Rules

1. **Never inline the changelog.** It is a separate maintained file. Link it.
2. **State the versioning scheme** only when the project declares one.
3. **Link the releases page or `CHANGELOG.md`** — whichever the project maintains.
4. **Omit the section entirely** when the project has no release process.

---

## Security

**Purpose:** give vulnerabilities a private channel instead of a public issue.

**Include when:** `SECURITY.md` exists, or the project handles authentication, network
traffic or user data.

### Shape

```
## Security

Report vulnerabilities privately to `security@example.com` — do not open a public issue.

Include in your report:
- Affected version
- Reproduction steps
- Impact assessment

We acknowledge reports within <period>.
```

### Rules

1. **Explicitly forbid public disclosure in the issue tracker.** This is the primary
   purpose of the section.
2. **Prefer linking `SECURITY.md`** when it exists.
3. **Use the project's real disclosure contact** — never a placeholder address.
4. **State the acknowledgement window** only if the project actually commits to one.
5. **Do not overstate security posture.** Do not claim "audited" or "secure" without a
   source.

---

## Sponsors

**Purpose:** acknowledge funding and make the funding path visible.

**Include when:** `.github/FUNDING.yml`, a sponsors file, or documented sponsors exist.

**Visual templates:** `social-proof.md` → *Sponsor Grid*, *Tiered Sponsor Wall*.

### Rules

1. **Read sponsors from the funding configuration**, never invent them.
2. **Tier them** (e.g. Keystone / Gold / Silver) with descending logo size.
3. **Each logo links** to the sponsor's site.
4. **Wrap the region in placeholder comments** (`<!-- sponsors -->` … `<!-- /sponsors -->`)
   so automation can refresh it.
5. **Place it after the technical content**, not in the Hero — funding is not the pitch.
6. **Omit entirely** when there are no sponsors. An empty sponsor section is worse than
   none.

---

## Adopters

**Purpose:** social proof from real users, and a growth loop.

**Include when:** organisations publicly document their use of the project.

**Visual templates:** `social-proof.md` → *Adopter Wall*.

### Rules

1. **Real, verifiable users only.** Never fabricate a company logo.
2. **Link each entry** to the company's project or case study.
3. **Add the registration call to action** — a link to the tracking issue or a template
   inviting users to add themselves. This is what makes the section grow.
4. **Cap the wall** at a readable grid; overflow goes to a separate `ADOPTERS.md`.
5. **Prefer named engineering teams over anonymous logos** when a quote is available.

---

## Citation & Acknowledgments

**Purpose:** credit prior work, and let researchers cite the project correctly.

**Include when:** the code derives from, extends or implements prior work worth crediting,
**or** `CITATION.cff` / a published paper / a DOI exists. Either half may appear on its own —
write only the subsection that has data.

### Acknowledgments

1. **Credit real dependencies of significance** — the framework the project extends, the
   protocol it implements.
2. **Attribute prior art honestly** when the project was inspired by another, including
   links.
3. Prefer a short paragraph over a long list. The dependency list is already in the
   manifest.
4. **Do not pad** with every transitive dependency.

### Citation

**Template:** `social-proof.md` → *Citation Block*.

1. **Only include when a real citation exists** — `CITATION.cff`, a published paper, or a
   documented DOI.
2. **Use the project's canonical citation**, not a paraphrase.
3. **Fence it as `bibtex`** for correct rendering.
4. **Link the DOI or paper** alongside the BibTeX entry.

---

## Comparison

**Purpose:** help a reader choose between this project and its alternatives, honestly.

**Include when:** the project competes with named alternatives and a fair, sourced
comparison is possible.

### Shape

```
## Comparison

| Capability | This project | <Alternative A> | <Alternative B> |
|---|---|---|---|
| Self-hosted | Yes | No | Yes |
| Horizontal scaling | Yes | Yes | Limited |
| License | Apache-2.0 | MIT | BSL |
```

### Rules

1. **Every claim about a competitor must be verifiable** from that competitor's public
   documentation. Gate G1 applies to competitor claims as strictly as to your own.
2. **State your own weaknesses** in the table. A comparison where you win every row is not
   credible.
3. **Link each alternative** so the reader can verify independently.
4. **Include the comparison date** in the intro — comparisons rot.
5. **Omit when a fair comparison is not possible** rather than writing marketing.

---

## License

**Purpose:** state the terms in one line.

**Include when:** a licence file exists. If none does, close the document with the one-line
recommendation instead.

### Shape

```
## License

[MIT](LICENSE)
```

For multiple licenses or a dual-license:

```
## License

Licensed under the [Apache License 2.0](LICENSE).

The `enterprise/` directory is covered by a separate [commercial license](enterprise/LICENSE).
```

### Rules

1. **Name plus link to the license file.** One line for a single license.
2. **Read the license from the file** — never assume MIT.
3. **Note per-directory or per-package license variance** when the scan found it.
4. **No boilerplate restatement** of the license text.
5. **When no license file exists**, omit the section and add:
   `No LICENSE file detected. Add a LICENSE to clarify project licensing.`
6. **Name the governance foundation** (Apache Software Foundation, CNCF, LF AI & Data)
   when the project belongs to one — it is a trust signal.
