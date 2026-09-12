# Installation — Claude Code

## Quick Setup

Copy the skill files to your project:

```bash
mkdir -p .claude/skills/general-readme
cp SKILL.md .claude/skills/general-readme/
cp -r references/ .claude/skills/general-readme/
```

## Global Installation

To make the skill available across all your projects:

```bash
mkdir -p ~/.claude/skills/general-readme
cp SKILL.md ~/.claude/skills/general-readme/
cp -r references/ ~/.claude/skills/general-readme/
```

## Usage

Type `/readme` or say "generate readme" in any Claude Code session.

## How It Works

Claude Code automatically loads skills from `.claude/skills/`. The skill triggers when you type `/readme` or say something that matches the trigger phrases in the skill description. It resolves only the primary language and detects the entry mode, then proceeds with the fixed structure and the house style.
