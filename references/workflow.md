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

## Phase 0 — Classify

**Output:** archetype, maturity tier, resolved configuration.

### 0.1 Archetype

Read `references/profiles.md` and pick exactly one primary archetype. If the project
spans two (a monorepo containing both a library and an app), pick the primary and record
the secondary; the primary drives structure, the secondary only influences emphasis.

Signals that resolve ambiguity:

| Signal | Points to |
|---|---|
| `bin` field, `cmd/` directory, single entrypoint | CLI Tool |
| Publish config + no runtime script | Library |
| Dev/start scripts + Dockerfile | Application |
| Component exports + Storybook + theme tokens | UI Library |
| Model/agent/RAG dependencies + prompt files | AI App |
| Large Markdown corpus + no build system | Knowledge Base |
| Helm/K8s manifests + protocol buffers + SDK folders | Infrastructure |
| Workspaces field + multiple package roots | Monorepo |

### 0.2 Maturity Tier

Read the tier table in `references/profiles.md`. Tier controls the section budget, so
resolve it before composing. When star data is unavailable (no network, no `git`
metadata), infer from static signals:

| Static signal | Suggests |
|---|---|
| CI workflow + CONTRIBUTING.md + issue templates | ≥ T2 |
| Sponsors file, docs site, release automation, multiple maintainers file | T3 |
| Only source + LICENSE | T1 |

### 0.3 Configuration

Offer defaults pre-selected. If the user does not answer, adopt the archetype defaults
and state the assumption in the final report. Never block on configuration.

Default resolution order:
1. Explicit user instruction
2. Archetype default from `profiles.md`
3. Global default: Professional tone, flat badges, English primary, no secondaries

---

## Phase 1 — Scan

**Output:** an evidence map plus a detection summary.

Read `references/project-scan.md` for detector rules and the exact evidence-map format.

### 1.1 Sequence

1. List the package root (respecting ignore rules below).
2. Parse manifests in precedence order.
3. Parse dependency declarations.
4. Count file extensions (fallback only).
5. Apply filename heuristics (last resort).
6. Detect: language, framework, build/CI, database/ORM, architecture, API style,
   license, project type, config files, git/contributor signals.
7. Emit the evidence map.

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

1. `references/profiles.md` → section set and order
2. `references/sections-core.md` → identity and onboarding recipes
3. `references/sections-reference.md` → technical recipes (only if the archetype includes them)
4. `references/sections-growth.md` → community recipes (only if the tier enables them)
5. `references/hero-and-html.md` → HTML-only regions
6. `references/onboarding.md` → Quick Start ladder
7. `references/social-proof.md` → sponsor/adopter/citation regions
8. `references/tone-profiles.md` → voice rules
9. `references/badges.md` + `badge-styles.md` → badge matrix
10. `references/diagram-templates.md` → diagram(s)
11. `references/accessibility.md` → alt text and table headers
12. `references/language-guide.md` → switcher and localization

### 2.2 Authoring Order

Compose in the order the sections will appear, and author the Hero last among the
identity sections — the Hero's badge matrix and one-liner depend on what the rest of the
document turned out to contain.

Practical order: scan-derived body sections → Hero → language switcher → link pool.

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

Build the new file as: `new hero` + `ordered sections`, where each ordered section is
either the regenerated auto region or the preserved manual region, placed at its
archetype position.

If a preserved manual section would violate the archetype order, leave it where it is and
insert the auto sections around it. Never move or delete manual content to satisfy an
ordering rule.

### Step 3 — Diff summary

Report:

```
Upgrade summary
  Preserved   : 3 manual sections, 12 manual link keys
  Regenerated : Hero, Features, Quick Start, Architecture
  Added       : Roadmap, FAQ (newly supported by scan)
  Removed     : none
  Gates       : all pass
```

### Step 4 — Do not lower quality

If the existing README contains content the scan cannot verify (a hand-written feature
list, a marketing tagline), preserve it. Upgrade Mode never deletes unverifiable human
content — it only refuses to *generate* unverifiable content.
