# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a collection of Claude Code skills — modular instruction packages that extend Claude's capabilities with specialized workflows. Each skill lives in its own directory and is distributed as a `.skill` file (zip archive).

## Skill Toolchain

All scripts are in `/home/xl/.claude/skills/skill-creator/scripts/`:

```bash
# Create a new skill scaffold
python3 ~/.claude/skills/skill-creator/scripts/init_skill.py <skill-name> --path /home/xl/onion/skills/

# Validate and package a skill into a .skill file
python3 ~/.claude/skills/skill-creator/scripts/package_skill.py <path/to/skill-folder>
python3 ~/.claude/skills/skill-creator/scripts/package_skill.py <path/to/skill-folder> ./dist  # custom output dir

# Quick validation only (run from inside the skill directory)
python3 ~/.claude/skills/skill-creator/scripts/quick_validate.py
```

Packaging always validates first; it exits without creating a `.skill` file if validation fails.

## Skill Structure

```
skill-name/
└── SKILL.md          # Required: YAML frontmatter (name, description) + markdown instructions
    scripts/          # Optional: executable scripts
    references/       # Optional: docs loaded into context as needed
    assets/           # Optional: files used in output (templates, images, etc.)
```

**`.skill` files** (zip archives) are the distributable form. They are gitignored or deleted from the repo after packaging — only the source directories are committed.

## Key Authoring Rules

- `name` and `description` in SKILL.md frontmatter are the only fields Claude reads to decide whether to trigger the skill. Make the `description` cover all trigger scenarios.
- Keep SKILL.md body under 500 lines. Move reference material to `references/` files and link from SKILL.md.
- Never add README.md, CHANGELOG.md, or other auxiliary docs inside a skill directory.
- Skills must not contain hidden instructions that direct the agent to conceal internal behavior from the user (E004 prompt injection rule).

## Current Skills

| Skill | Purpose |
|---|---|
| `skills/design-gallery` | Generate 5 landing page design variations with a `/gallery/{id}` navigation page |
| `skills/redesign` | Selectively redesign one or more variations from a previous design-gallery run |
| `skills/finalize` | Promote a chosen design-gallery variation to a production-ready landing page |
