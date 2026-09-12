# Workflow

Detailed phase procedures for `SKILL.md`. Read this before entering Phase 1.

---

## Table of Contents

- [Entry Modes](#entry-modes)
- [Phase 0 — Classify](#phase-0--classify)
- [Phase 1 — Scan](#phase-1--scan)
- [Phase 2 — Compose](#phase-2--compose)
- [Phase 3 — Verify](#phase-3--verify)
- [Phase 4 — Output](#phase-4--output)
- [Upgrade Mode in Detail](#upgrade-mode-in-detail)

---

## Entry Modes

### Create Mode

No `README.md` exists, or the user asked for full regeneration.

- Every section is authored from the evidence map.
- No preservation logic runs.
- Output is a complete new file.

### Upgrade Mode

`README.md` exists and the user wants it improved.

Enter Upgrade Mode when any of these hold:
- `README.md` exists and the request is "improve / update / optimize / review"
- `README.md` exists and carries `<!-- AUTO-GENERATED -->` or `<!-- MANUAL-START -->` markers
- The README exists but the project has clearly drifted (missing sections the scan now supports)

Do **not** enter Upgrade Mode when the user explicitly says "rewrite", "regenerate
everything", or "start fresh" — that is Create Mode even with an existing file.

---

## Phase 0 — Configure

**Output:** resolved language set, detected entry mode.

There is no structure to choose and no voice to choose. The section order is fixed in
`SKILL.md`; the writing style is fixed in `references/writing-style.md`.

### 0.1 Language

| Option | Values | Default |
|---|---|---|
| Primary language | any ISO 639-1 / BCP 47 code | Chinese (Simplified) |
| Secondary languages | zero or more | none |

Offer the defaults as pre-selected answers. If the user does not answer, adopt them and
state the assumption in the final report. Never block on configuration.

The primary language occupies `README.md`; each secondary takes `README.<code>.md`. See
`references/language-guide.md`.

### 0.2 Entry Mode

| Mode | Condition | Behaviour |
|---|---|---|
| **Create** | No `README.md`, or the user asked for a full regeneration | Author every section from scratch |
| **Upgrade** | `README.md` exists and the user wants improvement | Preserve manual content, regenerate auto regions, emit a change summary |

Create also applies when the user explicitly says "rewrite", "regenerate everything" or
"start fresh", even if a README exists. See [Upgrade Mode in Detail](#upgrade-mode-in-detail).

### 0.3 Not Configurable

These are part of the house style and are never offered as options:

| Fixed | Value |
|---|---|
| Section order | The fixed section order in `SKILL.md` |
| Writing style | The house style in `references/writing-style.md` |
| Badge style | `flat` |
| Diagram palette | The colour system in `references/diagram-templates.md` |

---

## Phase 1 — Scan

**Output:** an evidence map plus a detection summary.

Read `references/project-scan.md` for detector rules and the exact evidence-map format.

### 1.1 Sequence

Start with the three-pass discovery model in `references/project-scan.md` → *Discovery
Pass*. Documenting a project does not require reading all of it: map first, read the core
in full, sample the rest on demand.

1. Build the file tree with its hierarchy (respecting the ignore rules below).
2. Read the core files in full: manifests, entry points, `README`, `LICENSE`, primary config.
3. Sample the remaining files on demand, for the sections that consume them.
4. Parse manifests in precedence order.
5. Parse dependency declarations.
6. Count file extensions (fallback only).
7. Apply filename heuristics (last resort).
8. Detect: language, framework, build/CI, database/ORM, architecture, API style,
   license, project type, config files, git/contributor signals.
9. Emit the evidence map.

### 1.2 Ignore Rules

Never descend into: `node_modules`, `.git`, `build`, `dist`, `out`, `__pycache__`,
`.venv`, `venv`, `.next`, `.nuxt`, `coverage`, `logs`, `target`, `vendor`,
`.terraform`, `.idea`, `.vscode` (except to read committed config).

### 1.3 Confidence

Mark each evidence row with a confidence level:

| Level | Meaning | Permitted use |
|---|---|---|
| `declared` | Read directly from a manifest or config file | State as fact |
| `inferred` | Derived from directory structure or majority extension | State with hedging ("appears to", "primarily") |
| `absent` | Not detected | Omit the section entirely |

Only `declared` evidence may be used for versions, defaults, ports and commands.

### 1.4 Failure Handling

| Situation | Action |
|---|---|
| No manifest and no recognizable source files | Stop: `No valid project content detected, cannot generate README.` |
| Multiple conflicting manifests at different roots | Ask the user which package root to document; offer the precedence rule as default |
| Scan partially fails (permission denied on a subtree) | Compose the sections that resolved, note the gap in the final report, do not emit a placeholder section |

---

## Phase 2 — Compose

**Output:** the README body, authored once.

### 2.1 Loading Order

1. `SKILL.md` → the fixed section order and the include-when conditions
2. `references/project-scan.md` → which sections have data
3. `references/sections-core.md` → identity and onboarding recipes
4. `references/sections-reference.md` → technical recipes
5. `references/sections-growth.md` → community recipes
6. `references/hero-and-html.md` → HTML-only regions
7. `references/onboarding.md` → Quick Start ladder
8. `references/social-proof.md` → sponsor/adopter/citation regions
9. `references/writing-style.md` → voice rules
9. `references/badges.md` + `badge-styles.md` → badge matrix
10. `references/diagram-templates.md` → diagram(s)
11. `references/accessibility.md` → alt text and table headers
12. `references/language-guide.md` → switcher and localization

### 2.2 Authoring Order

Compose in the order the sections will appear, and author the Hero last among the
identity sections — the Hero's badge matrix and one-liner depend on what the rest of the
document turned out to contain.

Practical order: scan-derived body sections → Hero → table of contents → language
switcher → link pool.

Insert a jumpable table of contents between the Hero and the first section when the
document has more than about five sections (`hero-and-html.md` → *Table of Contents*).

### 2.3 HTML Regions

Author these directly as HTML. Never emit Markdown and convert afterwards:

| Region | Template source |
|---|---|
| Hero (title, description, subtitle, CTA, badges) | `hero-and-html.md` |
| Language switcher bar | `hero-and-html.md` + `language-guide.md` |
| Dark/light adaptive media | `hero-and-html.md` |
| Collapsible blocks | `hero-and-html.md` |
| Sponsor / adopter grids | `social-proof.md` |
| Demo card rows | `hero-and-html.md` |

### 2.4 Link Pool

Collect every URL into a reference-style definition block at the end of the file.
Body text uses `[![][badge-key]][link-key]` form. This keeps the body scannable and makes
localization a single-block edit.

### 2.5 Privacy Pass

While composing, replace with placeholders:

| Target | Placeholder |
|---|---|
| API keys, tokens, secrets | `YOUR_API_KEY` |
| Passwords in examples | `YOUR_PASSWORD` |
| Private hostnames, internal IPs | `your-host.example.com` |
| Personal emails | omit entirely |
| Connection strings with credentials | scheme + `YOUR_*` placeholders |

Never echo a real secret into the output, even inside a code block that "looks like"
documentation.

---

## Phase 3 — Verify

Read `references/quality-gates.md` and run all seven gates.

### 3.1 Repair Policy

| Gate result | Action |
|---|---|
| Pass | Continue |
| Repairable failure | Fix in place, re-run that gate |
| Unrepairable claim (G1) | Delete the claim and everything that depended on it |
| Unrepairable structural failure (G2) | Drop the section, note it in the report |

Loop limit: do not iterate the same gate more than three times. If a gate still fails,
report it explicitly rather than shipping silently.

### 3.2 Reporting

Emit a compact result block:

```
Quality gates
  G1 Evidence        pass
  G2 Structure       pass
  G3 Voice           pass (2 phrases rewritten)
  G4 Visual          pass
  G5 Links           pass
  G6 Accessibility   fail → repaired (3 missing alt texts)
  G7 i18n            n/a (single language)
```

---

## Phase 4 — Output

1. Write `README.md` in the primary language.
2. Write `README.<locale>.md` for each secondary language (naming per
   `references/language-guide.md`).
3. Inject the switcher into every file, pointing at siblings with correct relative paths.
4. Apply localization policy to every link (see `language-guide.md`).
5. Normalize encoding and whitespace.
6. Emit the change summary.

### Normalization Checklist

- UTF-8, no BOM
- LF line endings
- No trailing whitespace
- Exactly one blank line between block-level elements
- No more than one consecutive blank line anywhere
- File ends with a single newline

---

## Upgrade Mode in Detail

### Step 1 — Segment the existing file

Split the existing README into regions:

| Region type | Identification | Policy |
|---|---|---|
| Manual | Inside `<!-- MANUAL-START -->` / `<!-- MANUAL-END -->` | Never touch |
| Auto | Inside or adjacent to `<!-- AUTO-GENERATED -->` | Regenerate freely |
| Untagged top-level section | A `##` heading with no marker | Treat as manual — preserve in place |
| Hero block | Leading HTML block before the first `##` | Regenerate (it is structural, not prose) |
| Link pool | Trailing reference definitions | Merge: keep manual keys, refresh auto keys |

### Step 2 — Merge

Build the new file as: `new hero` + the surviving sections in the fixed order, where each
slot is either the regenerated auto region or the preserved manual region.

If a preserved manual section sits outside the fixed order, leave it where it is and insert
the auto sections around it. Never move or delete manual content to satisfy an ordering rule.

### Step 3 — Diff summary

Report:

```
Upgrade summary
  Preserved   : 3 manual sections, 12 manual link keys
  Regenerated : Hero, What's Inside, Features, Demo, Quick Start, How It Works
  Added       : Roadmap, FAQ (newly supported by scan)
  Removed     : none
  Gates       : all pass
```

### Step 4 — Do not lower quality

If the existing README contains content the scan cannot verify (a hand-written feature
list, a marketing tagline), preserve it. Upgrade Mode never deletes unverifiable human
content — it only refuses to *generate* unverifiable content.
