# Onboarding

Quick Start patterns that get a reader to a running system with the fewest possible
commands, and the deployment matrices that support them.

Read alongside `sections-core.md` → *Quick Start*.

---

## Table of Contents

- [The Four-Line Rule](#the-four-line-rule)
- [Ladder Variants](#ladder-variants)
- [Hardware and Runtime Gate](#hardware-and-runtime-gate)
- [Multi-Package-Manager Blocks](#multi-package-manager-blocks)
- [PaaS Deploy Matrix](#paas-deploy-matrix)
- [Expected Output Block](#expected-output-block)
- [Long-Running Task Guidance](#long-running-task-guidance)
- [Docker Variants](#docker-variants)

---

## The Four-Line Rule

A reader should reach a running system in **four commands or fewer**:

```
1. fetch the project
2. install
3. configure (omitted when none is needed)
4. run
```

If the project needs more, the extra steps either belong in a prerequisite block above the
commands, or the project needs a container recipe.

### The closing condition

Every Quick Start ends with an observable result:

```
Open http://localhost:3000 — the setup wizard appears.
```

Without a stated success condition, a reader cannot tell whether it worked. A Quick Start
that ends on a command fails gate G2 for Application and CLI Tool archetypes.

### Anti-patterns

| Anti-pattern | Correction |
|---|---|
| `a && b && c && d` on one line | Split into numbered steps |
| `# Edit .env with your credentials` and nothing else | State which values are required |
| No success condition | Add the URL or the expected output |
| Prerequisites buried mid-section | Move to the top, before any command |
| Generic `docker build -t my-app .` | Use the project's real image name and path |
| Commands that were never in the repository | Remove — gate G1 |

---

## Ladder Variants

Choose the variant that matches the archetype.

### A — Container-first (Application)

Use when a `Dockerfile` or compose file exists. Containers eliminate environment drift.

```
## Quick Start

<one line stating the outcome>

> [!IMPORTANT]
> Requires Docker and Docker Compose v2.24 or later.

```bash
git clone <repo>
cd <project>
cp .env.example .env
docker compose up -d
```

Open http://localhost:3000.
```

**Then, below it**, a `<details>` block with the manual path for contributors:

```
<details>
<summary>Manual setup for development</summary>

### Prerequisites
...
</details>
```

### B — Package-manager-first (Library, CLI Tool)

Use when the artefact is published to a registry. Lead with the one-line install.

```
## Installation

```bash
npm install <package>
```

```bash
pnpm add <package>
```

```bash
yarn add <package>
```

```bash
bun add <package>
```

## Usage

```typescript
<minimal real example>
```
```

Each manager gets its **own fence**. Never `npm/yarn/pnpm install`.

### C — Language-runtime-first (Application, Library in Python/Go/Rust)

Use when the project is consumed from source or a language-native registry.

```
### Prerequisites

- Python 3.11+
- PostgreSQL 15+

### Install

```bash
<real install command for this project>
```

### Run

```bash
<real run command>
```
```

State the runtime version only when the manifest declares it.

### D — Integration-first (UI Library, Framework plugin)

Use when the package plugs into a host framework and needs the peer dependency.

```
### Installation

```bash
npm install <package> <peer-dependency>
```

`<peer-dependency>` is a peer dependency and must be installed separately.

### Register

```typescript
<real registration snippet>
```
```

Peer dependencies must be called out explicitly — a silent missing peer is the most common
installation failure.

### E — Hardware-gated (AI App)

Use when model inference imposes real hardware constraints.

```
## Quick Start

> [!IMPORTANT]
> - CPU: 4 cores minimum
> - RAM: 16 GB minimum
> - GPU: optional, 8 GB VRAM recommended for local inference

### 1. Application environment

```bash
<install the application>
```

### 2. Inference environment

> [!WARNING]
> Install the inference server in a **separate** virtual environment. Sharing an
> environment causes dependency conflicts that are difficult to diagnose.

```bash
<install the inference framework, in its own env>
```

### 3. Run

```bash
<start command>
```
```

The two-environment rule is mandatory for AI App. Enforcing the separation prevents the
most common and most confusing failure class.

### F — Learning-path (Knowledge Base)

Knowledge bases have no `run` command. Replace with a progression:

```
## Getting Started

1. Read <introductory topic>
2. Work through <core topic>
3. Attempt <worked example>
4. Review <reference appendix>
```

---

## Hardware and Runtime Gate

Place **before** the first command, so an under-provisioned reader discovers the problem
before installing anything.

### Form

```markdown
> [!IMPORTANT]
> **Minimum requirements**
> - CPU: <n> cores
> - RAM: <n> GB
> - Disk: <n> GB
> - Runtime: <name> <version>+
```

### Sourcing the numbers

| Constraint | Source |
|---|---|
| Runtime version | `engines`, `requires-python`, `rust-version`, `.nvmrc` |
| CPU / RAM / disk | Container resource limits, CI matrix, documented requirements |
| GPU / VRAM | Inference framework docs, compose service reservations |

**Never invent a hardware requirement.** If the repository states none, omit the gate
rather than guessing. An invented requirement blocks users who could have run the project.

---

## Multi-Package-Manager Blocks

Detect the declared manager from `packageManager` in the manifest or the lockfile present.

| Lockfile / field | Manager |
|---|---|
| `package-lock.json` | npm |
| `pnpm-lock.yaml`, `pnpm-workspace.yaml` | pnpm |
| `yarn.lock` | yarn |
| `bun.lockb`, `bun.lock` | bun |
| `uv.lock` | uv |
| `poetry.lock` | poetry |

### Rules

1. **Lead with the declared manager**, then list the alternatives.
2. **Separate fence per manager.** Never slash-join.
3. **Do not list a manager the project does not support.** If the manifest declares an
   engine constraint, honour it.
4. **For monorepos**, one install command at the root — do not enumerate per-package
   installs.
5. **For libraries**, list all managers whose registries carry the package.

---

## PaaS Deploy Matrix

Offer one-click deployment only for platforms the project actually documents support for.

### Form

```markdown
| Deploy to Vercel | Deploy to Netlify | Deploy to Railway |
| :---: | :---: | :---: |
| [![Deploy with Vercel][badge-vercel]][link-vercel] | [![Deploy to Netlify][badge-netlify]][link-netlify] | [![Deploy on Railway][badge-railway]][link-railway] |
```

### Rules

1. **A button must lead to a working deploy flow.** A dead button fails gate G5.
2. **Pair with a note about what the platform does not configure** — environment variables,
   databases, and background workers usually need manual setup.
3. **Use a `[!TIP]` alert** for common platform pitfalls (fork sync, build cache, region).
4. **Do not recommend a platform the project does not support**, even if it is popular.
5. **For self-hosted-only projects**, omit the matrix and say so explicitly.

### Common platform caveats worth stating

| Platform | Caveat |
|---|---|
| Vercel | Serverless functions have an execution time limit; persistent connections unsupported |
| Netlify | Same function limits; long-running jobs need a separate worker |
| Railway / Render | Cold starts on free tiers |
| Regional hosting | Domain configuration and备案 requirements in some regions |

---

## Expected Output Block

For any step whose success is not self-evident, show what success looks like.

### Form

````markdown
After the command completes, you should see:

```text
────────────────────────────────────────────
  Name        : sample
  Records     : 740
  Duration    : 0:02:33
────────────────────────────────────────────
```
````

### Rules

1. **Use a `text` fence**, not `bash`.
2. **Reproduce the real shape** of the output — field names, separators — but you may omit
   timings and paths that vary.
3. **Never fabricate a log format.** If you cannot reproduce it from the source or a
   documented example, describe the success condition in prose instead.
4. Use this for: index builds, migrations, model downloads, first-run setup, codegen.

---

## Long-Running Task Guidance

Steps that take minutes with no output cause users to interrupt them. Mitigate:

| Technique | Example |
|---|---|
| State the expected duration | "This takes 2–5 minutes depending on disk speed" |
| Warn against interruption | `> [!WARNING]` — "Do not interrupt; a partial index must be rebuilt" |
| Mention progress indicators | "Progress is printed every 1000 records" |
| Provide a resume path | "If interrupted, re-run with `--resume`" |
| Add the expected-output block | See above |

---

## Docker Variants

| Variant | Command shape | When |
|---|---|---|
| Single container | `docker run -p 3000:3000 <image>` | Simple stateless service |
| Compose | `docker compose up -d` | Multi-service stack |
| Compose, production file | `docker compose -f docker-compose.prod.yml up -d` | When the file exists |
| Build from source | `docker build -t <name> .` | When no published image exists |
| Pre-built image | `docker pull <image>` | When a registry image exists |

### Rules

1. **Use the project's real image name**, read from the compose file or CI config.
2. **Publish the port mapping** when the service exposes a port — a reader needs the URL.
3. **Mention volume mounts** when the project requires persistence.
4. **Mention the environment file** when compose reads one.
5. **Never invent a Docker Hub namespace.**

---

## Checklist Before Writing Quick Start

- [ ] Archetype-appropriate variant selected
- [ ] Hardware/runtime gate placed before the first command (or omitted with reason)
- [ ] Four steps or fewer
- [ ] Every command exists in the repository, evidence-bound
- [ ] Each step is a single copy-pasteable block
- [ ] Closing condition states a URL or observable result
- [ ] Long-running steps carry a duration or a non-interruption warning
- [ ] All commands identical across language files (never translated)
- [ ] No placeholder tokens remain
