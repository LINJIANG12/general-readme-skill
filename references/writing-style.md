# Writing Style

There is one house style. Every generated README uses it. It is not configurable.

Read this before Phase 2 and again before running gate G3.

---

## Table of Contents

- [The Voice](#the-voice)
- [Sentence Rules](#sentence-rules)
- [Section Intros](#section-intros)
- [Feature and List Format](#feature-and-list-format)
- [Numbers Over Adjectives](#numbers-over-adjectives)
- [Emoji and Punctuation](#emoji-and-punctuation)
- [Banned Phrases](#banned-phrases)
- [Preferred Vocabulary](#preferred-vocabulary)

---

## The Voice

**Neutral, thorough, structured.** Write like a senior engineer documenting a system for
their own team — someone who will have to read this again in six months and needs it to be
accurate.

- Clear over clever.
- Complete sentences with a subject and a verb.
- Define a term on first use if it is domain-specific.
- Parallel structure in lists: either every item starts with a verb, or every item starts
  with a noun. Never mix within one list.
- No marketing register. The reader is evaluating, not being sold to.

### Do

- `The server validates incoming requests against the JSON schema before processing.`
- `Prerequisites: Node.js 18+, PostgreSQL 14+`
- `Latency was measured at 12 ms at p99 on a 1M-record corpus.`
- `Administrators must configure TLS_CERT before exposing the service.`

### Don't

- `Super fast validation! 🚀`
- `Just install Node and you're good to go.`
- `In the ever-evolving landscape of modern software…`
- `This is a powerful and robust framework that leverages cutting-edge technology.`

---

## Sentence Rules

1. **Vary sentence length.** A run of uniform sentences reads as machine-generated. Mix
   one-liners with two-clause explanations.
2. **One idea per sentence.** If a sentence has more than two commas, split it.
3. **Active voice by default.** Passive is acceptable where the actor is irrelevant:
   `The index is rebuilt nightly.`
4. **Specific over general.** `Handles 10k req/s` beats `high performance`. `JWT with
   RS256` beats `secure authentication`.
5. **No restating the heading.** A `## Configuration` section followed by `This section
   describes the configuration` has its first sentence deleted.
6. **No hedging on facts.** Do not write `might support` when the manifest proves support.
   Reserve hedging for genuinely inferred statements (`appears to`, `primarily`).
7. **No absolute claims without evidence.** Not `the fastest`, `100% secure`, `never fails`.
8. **Second person is acceptable in instructions**, third person in reference prose.

---

## Section Intros

Optional, and at most one sentence.

- Use one when the section needs framing the heading cannot provide.
- Omit when the heading is self-explanatory — which is most of the time.
- Never use an intro that only announces the section exists.

| Verdict | Text |
|---|---|
| Good | `Everything needed to run the service locally.` |
| Good | `(omitted)` |
| Bad | `The following section describes the configuration options of this project.` |
| Bad | `This section will guide you through the installation process.` |

---

## Feature and List Format

Features are a table in every README, with a bolded name and one clause of substance.

```markdown
| Feature | Description |
|---|---|
| Real-time sync | WebSocket updates pushed to every connected client |
| Role-based access | Permissions resolved per workspace membership |
| Typed errors | Failures carry a status code and the parsed response body |
```

Rules:

1. **Maximum 6 rows.** With 20 candidate features, choose the 6 a reader would notice.
2. **Never pad.** Two real features beat six padded ones.
3. **Lead with the outcome**, not the mechanism.
   - Good: `Streams 10k events per second`
   - Bad: `Uses a lock-free ring buffer`
4. **No feature the scan did not evidence.**
5. **Do not restate the Hero description.**
6. **No "and much more".**

For lists outside the Features table (steps, options, limitations), use `-` bullets, keep
them flat, and apply the parallel-structure rule.

---

## Numbers Over Adjectives

Whenever a measurable value exists in the source, use the value.

| Instead of | Write |
|---|---|
| `blazingly fast` | `12 ms p99 on a 1M-record corpus` |
| `highly scalable` | `scales horizontally to N nodes` |
| `comprehensive test coverage` | `94% line coverage` |
| `supports many databases` | `supports PostgreSQL 14+, MySQL 8+, SQLite 3.35+` |
| `lightweight` | `4.2 MB gzipped` |
| `battle-tested` | `running in production since 2021` (only with a source) |

A number without a source is fabrication. Cite the file it came from.

---

## Emoji and Punctuation

1. **No emoji anywhere in prose.** Not in headings, lists, tables or section intros.
   Badge logos are images, not emoji, and are unaffected.
2. **No emoji as a bullet marker.** Use `-`.
3. **No exclamation marks** in any description.
4. **No decorative punctuation** — no `>>>`, no chains of `—`.
5. **Use the target language's punctuation.** Chinese uses full-width punctuation
   （，。：）；English uses half-width.
6. **Code spans and identifiers keep their original form** regardless of surrounding
   language — backticks, mixed case, underscores.

---

## Banned Phrases

Banned everywhere, with no exceptions:

> powerful · robust · versatile · leverages · seamlessly · cutting-edge · comprehensive ·
> state-of-the-art · ever-evolving landscape · game-changing · revolutionary ·
> next-generation · best-in-class · enterprise-grade · blazingly fast · world-class ·
> turnkey · synergy · effortless · unleash · supercharge · battle-tested · production-ready
> (unless citing actual production usage with a source) · one-stop · out of the box
> (as a boast; acceptable when stating a factual default) · simply · just · easy ·
> straightforward · obviously · of course · as you can see · note that · it's worth
> mentioning · awesome · cool · amazing · love · hate · super · we believe

Also banned:

- Emoji in prose
- Exclamation marks
- Unourced comparisons (`faster than X`)
- Unsourced compliance or security claims (`audited`, `secure`, `GDPR compliant`)

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
| allows you to | lets you |

---

## Applying the Style to Chinese Output

The voice is language-independent. When the primary language is Chinese:

1. **Keep the same register** — 客观、结构化、完整句。不要因为换成中文就变得口语化或营销化。
2. **Technical terms stay in English** where Chinese developers use the English form:
   `API`、`REST`、`Docker`、`commit`、`pull request`、`webhook`。不要生造译名。
3. **First use of a term may pair both forms**: `依赖注入（dependency injection）`.
4. **No Chinese-specific filler** — 禁止「强大的」「优雅的」「极致的」「开箱即用」这类空泛形容，
   等同于英文的 banned list。
5. **Use full-width punctuation**，but never inside a code span or a path.
6. **Sentence length**: Chinese tolerates longer clauses than English. Split anyway when
   a sentence carries more than one idea.
