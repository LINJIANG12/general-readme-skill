# Tone Profiles

Six voices. Phase 0 resolves one archetype, which pre-selects a default tone; the user may
override. Exactly one tone applies across the whole document — mixing fails gate G3.

---

## Table of Contents

- [Tone × Archetype Matrix](#tone--archetype-matrix)
- [A — Energetic](#a--energetic)
- [B — Minimal](#b--minimal)
- [C — Professional](#c--professional)
- [D — Playful](#d--playful)
- [E — Academic](#e--academic)
- [F — Enterprise](#f--enterprise)
- [Universal Rules](#universal-rules)
- [Banned Phrase Master List](#banned-phrase-master-list)
- [Preferred Vocabulary](#preferred-vocabulary)

---

## Tone × Archetype Matrix

The archetype's default is used when the user supplies no preference.

| Archetype | Default tone | Acceptable alternatives |
|---|---|---|
| Library | Minimal | Professional |
| Application | Professional | Energetic |
| CLI Tool | Minimal | Playful |
| UI Library | Energetic | Playful, Professional |
| AI App | Energetic | Professional |
| Knowledge Base | Academic | Professional |
| Infrastructure | Professional | Enterprise |
| Monorepo | Professional | Minimal |

### Switching tone mid-document

Not permitted. If the user asks for Energetic features but Professional tables, resolve to
one: use Energetic throughout and convert the tables to emoji lists, or use Professional
throughout and drop the emoji.

---

## A — Energetic

Reference style: FastAPI, shadcn/ui.

### Voice

Direct, confident, mildly opinionated. Excited about what the project does without
overselling it. Contractions welcome.

### Rules

- Short sentences. More than two commas → split.
- Lead with the benefit, not the feature.
- Active voice: `Handles 10k req/s`, not `10k req/s can be handled`.
- Emoji permitted in feature lists, one per item, prefixed to a bolded label.
- Section intros: one sentence maximum, optional.

### Do

- `Get up and running in 30 seconds.`
- `Type-safe end to end — no `any` anywhere.`
- `Drops into any Express app. Zero config.`
- `- ⚡ **Instant reload** — Config changes apply without a restart`

### Don't

- `This is a powerful and robust framework that leverages cutting-edge technology.`
- `It seamlessly integrates with your existing workflow.`
- `In the ever-evolving landscape of web development…`
- Emoji on every line of a long list

---

## B — Minimal

Reference style: Tailwind CSS, esbuild.

### Voice

Confident, quiet. Let the code speak. If a section can be shorter, shorten it. Every word
earns its place.

### Rules

- One-line descriptions. No paragraphs unless unavoidable.
- No section intros. The heading is the intro.
- No explanatory prose around code blocks.
- No emoji. No bold. No em dashes in lists.

### Do

- `Type-safe API with full inference.`
- `npm install package`
- `- Real-time sync over WebSocket`
- `- Role-based access per workspace`

### Don't

- `To get started, simply run the following command to install the package:`
- `This section will guide you through the installation process.`
- Any sentence restating what the code already shows.
- Decorative emoji

---

## C — Professional

Reference style: Kubernetes, Node.js, Django.

### Voice

Neutral, thorough, structured. A senior engineer documenting for their team. Clear over
clever. Complete sentences, not fragments.

### Rules

- Complete sentences with subject and verb.
- Define domain terms on first use.
- Parallel structure in lists — all items start with a verb, or all with a noun.
- No emoji in prose (badge logos are fine).
- Section intros: one neutral sentence, optional.

### Do

- `The server validates incoming requests against the JSON schema before processing.`
- `Prerequisites: Node.js 18+, PostgreSQL 14+`
- `| Type Safety | Full TypeScript inference with zero configuration |`

### Don't

- `Super fast validation! 🚀`
- `Just install Node and you're good to go.`
- Exclamation marks in descriptions

---

## D — Playful

Reference style: community tooling with personality — good for CLI tools and developer
utilities where the audience appreciates it.

### Voice

Warm and human, lightly witty. Never at the expense of clarity. The humour is in the
phrasing, not in added content — nothing is sacrificed for a joke.

### Rules

- Emoji permitted and encouraged, but only where the tone profile allows decoration.
- Occasional second person, but instructions stay imperative.
- One light touch per section, maximum. A joke in every paragraph is exhausting.
- Never jokey in: prerequisites, commands, security, licence, limitations.
- Never self-deprecating about reliability or security.

### Do

- `Install it once, forget it exists. That's the goal.`
- `## Installation` / `One command. That's the whole section.`
- `- 🧹 **Tidy output** — No 400-line stack traces in your terminal`
- `We recommend the Docker route. It's less likely to surprise you.`

### Don't

- `This tool is basically magic ✨🧙‍♂️🚀` — no substance
- Humour inside a command block or a warning
- `Don't worry, we definitely tested it!` — undermines trust
- Puns in section headings that obscure the content

---

## E — Academic

Reference style: research software, canonical algorithm implementations, curated
curricula.

### Voice

Precise, attributed, restrained. Claims carry sources. The document is a reference, not a
pitch.

### Rules

- Every performance or comparative claim carries a citation or a measurement source.
- Use the field's terminology consistently, and define it on first use.
- Footnote-style attributions where a claim originates elsewhere.
- No emoji. No exclamation marks.
- Prefer the passive voice where the actor is irrelevant: `The index is rebuilt nightly.`
- Include a Citation section when the project has a paper (see `social-proof.md`).

### Do

- `Latency was measured at 12 ms at p99 on a 1M-vector corpus (see benchmarks).`
- `The approach follows the two-phase commit protocol described by Gray & Lamport (1978).`
- `## Reproducing the results` with the exact commands and dataset versions
- `### Trade-offs` in every concept explanation

### Don't

- `Blazingly fast compared to other solutions.`
- `Everyone is using this.`
- An unsourced comparison against a named competitor
- Marketing adjectives of any kind

---

## F — Enterprise

Reference style: compliance-oriented platform documentation for internal or regulated
adoption.

### Voice

Formal, procedural, unambiguous. Written for a reader who must have the document approved
by a security or compliance reviewer.

### Rules

- No contractions. No emoji. No idioms.
- State requirements and obligations with `must`, `should`, `may` per RFC 2119 semantics.
- Explicit about what the software does not do (see Limitations).
- Security, licence and data-handling statements up front, not buried.
- Every version, dependency and supported platform is stated precisely.
- Change-history and support policy referenced where they exist.

### Do

- `Administrators must configure `TLS_CERT` before exposing the service.`
- `Supported platforms: RHEL 8 and 9, Ubuntu 22.04 LTS, Windows Server 2022.`
- `Report vulnerabilities through the process in [SECURITY.md](SECURITY.md). Do not open a public issue.`
- `## Data handling` — what is stored, where, and for how long

### Don't

- `Just point it at your database and you're done!`
- Vague support statements such as `works with most databases`
- Security claims without evidence
- Omitting the Limitations section

---

## Universal Rules

Apply to all six tones.

1. **No filler.** Every sentence carries information.
2. **Vary sentence length.** A run of uniform sentences reads as machine-generated.
3. **Be specific.** `Handles 10k req/s` beats `high performance`. `JWT with RS256` beats
   `secure authentication`.
4. **No absolute claims without evidence.** Not `the fastest`, `100% secure`, `never fails`.
5. **No hedging on facts.** Do not write `might support` when the manifest proves support.
6. **No marketing register.** The reader wants to evaluate, not be sold to.
7. **Second person is acceptable in instructions; third person in reference prose.**
8. **No restating the heading.** `## Configuration` followed by `This section describes
   the configuration` is deleted.
9. **No exclamation marks in Enterprise, Professional, Minimal, Academic.**
10. **No emoji in Enterprise, Professional, Minimal, Academic.**

---

## Banned Phrase Master List

### Banned in all tones

> powerful · robust · versatile · leverages · seamlessly · cutting-edge · comprehensive ·
> state-of-the-art · ever-evolving landscape · game-changing · revolutionary ·
> next-generation · best-in-class · enterprise-grade · blazingly fast · world-class ·
> turnkey · synergy · effortless · unleash · supercharge

### Additionally banned in Minimal

> simply · just · easy · straightforward · obviously · of course · as you can see ·
> note that · it's worth mentioning · in order to (use "to")

### Additionally banned in Professional

> emoji in prose · exclamation marks · awesome · cool · amazing · love · hate · super

### Additionally banned in Enterprise

> everything in the Professional list · contractions · idioms · "and more" ·
> "blazing" · "we believe" · unsourced compliance claims

### Additionally banned in Academic

> everything in the Professional list · anecdotal claims · unsourced comparisons ·
> "obviously" · "it is well known that"

### Additionally banned in Playful

> Jokes inside prerequisites, commands, security, licence, or limitations ·
> self-deprecation about reliability or security · emoji chains

---

## Preferred Vocabulary

| Avoid | Prefer |
|---|---|
| utilize, leverage | use |
| implement | add, build |
| integrate | connect, add support for |
| facilitate | let, allow |
| architect (verb) | design |
| streamlined | simple |
| high-performance | fast, with the measured number |
| seamlessly integrates with | works with |
| set up | configure |
| check | validate |
| create | initialize (for state), add (for files) |
| log in | authenticate |
| a number of | several, or the actual count |
| in order to | to |
| prior to | before |
| in the event that | if |
| at this point in time | now |

### Numbers over adjectives

Whenever a measurable value is available in the source, use it.

| Instead of | Write |
|---|---|
| `blazingly fast` | `12 ms p99 on a 1M corpus` |
| `highly scalable` | `horizontally scalable to N nodes` |
| `comprehensive test coverage` | `94% line coverage` |
| `supports many databases` | `supports PostgreSQL 14+, MySQL 8+, SQLite 3.35+` |
| `lightweight` | `4.2 MB gzipped` |
