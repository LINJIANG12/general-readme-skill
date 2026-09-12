# Installation — CodeBuddy

## Scope

CodeBuddy discovers skills from two locations:

| Scope | Path | Applies to |
|---|---|---|
| **User** | `~/.codebuddy/skills/<skill-name>/` | Every project you open |
| **Project** | `<project>/.codebuddy/skills/<skill-name>/` | That repository only; can be committed and shared |

A user-level skill is the right choice when you want `/readme` available everywhere, which
is the usual case. Use project scope only when the skill should travel with a specific
repository.

## Setup

1. Create the skill directory:

```bash
mkdir -p ~/.codebuddy/skills/general-readme-skill
```

2. Copy the skill definition and its references:

```bash
cp SKILL.md ~/.codebuddy/skills/general-readme-skill/
cp -r references/ ~/.codebuddy/skills/general-readme-skill/
```

Optional, for offline reading of the guides and examples:

```bash
cp -r install/ examples/ assets/ ~/.codebuddy/skills/general-readme-skill/
cp README.md README.en.md LICENSE ~/.codebuddy/skills/general-readme-skill/
```

3. Restart CodeBuddy, or reload the window, so the skill directory is re-scanned.

## Windows (PowerShell)

```powershell
$src = "<path-to-this-repo>"
$dst = "$env:USERPROFILE\.codebuddy\skills\general-readme-skill"

Remove-Item $dst -Recurse -Force -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Force -Path $dst | Out-Null

Copy-Item "$src\SKILL.md","$src\README.md","$src\README.en.md","$src\LICENSE" $dst
Copy-Item "$src\references","$src\install","$src\examples","$src\assets" $dst -Recurse
```

Re-run those two `Copy-Item` lines after editing the skill to refresh the installed copy.

## Why copy instead of linking

A directory junction (`New-Item -ItemType Junction`) would keep the installed skill in sync
automatically, but Node reports a junction as `isSymbolicLink = true` and
`isDirectory = false`. A loader that filters directory entries with `isDirectory()` will not
see it. Copy the files, or symlink only if you have verified that your build discovers it.

## Verification

Confirm the installed layout:

```
~/.codebuddy/skills/general-readme-skill/
├── SKILL.md          # required
├── references/       # required
├── install/
├── examples/
├── assets/
├── README.md
├── README.en.md
└── LICENSE
```

Then check that the skill is not disabled. `settings.json` lists disabled skills by the
absolute path of their `SKILL.md`:

```json
{
  "disabledSkillsByPath": {
    "C:\\Users\\<you>\\.codebuddy\\skills\\github\\SKILL.md": true
  }
}
```

If your entry appears there, remove it or toggle the skill on in settings.

## Usage

Type `/readme` in a CodeBuddy conversation, or say "帮我写 README".

The skill triggers from the `description` field in `SKILL.md`, so natural-language
requests work without the slash command.
