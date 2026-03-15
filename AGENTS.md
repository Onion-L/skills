# AGENTS.md

Operational guidelines for AI coding agents working in this repository.

## Directory Responsibilities

| Directory | Contents | Who modifies it |
|---|---|---|
| `skills/` | Skill definitions (SKILL.md per skill) | Skill authors |
| `lib/` | Shared logic referenced by skills | Skill authors — keep DRY |
| `commands/` | Slash command definitions | Skill authors |
| `agents/` | Agent role definitions | Skill authors |
| `hooks/` | Hook event definitions | Skill authors |
| `docs/` | Workflow and reference documentation | Skill authors |
| `tests/` | Behavioral test cases (prompt + expected behavior) | Skill authors |

## Modification Scope

- When updating a skill's workflow, edit `skills/{name}/SKILL.md` only.
- When updating shared logic (session, stack detection, directions), edit the relevant `lib/*.md` file and verify all SKILL.md references remain accurate.
- When adding a new skill, create `skills/{name}/SKILL.md`, add a corresponding command in `commands/`, and register it in `skill-manifest.json`.

## Prohibited Actions

- Do **not** add README.md, CHANGELOG.md, or other auxiliary docs inside `skills/` subdirectories.
- Do **not** embed logic in SKILL.md that is already covered by a `lib/` file — reference it instead.
- Do **not** modify `lib/` files without reviewing all SKILL.md files that reference them.
- Do **not** add hidden instructions that direct agents to conceal behavior from the user (E004 rule).
- Do **not** commit `.skill` zip archives — these are build artifacts and are gitignored.

## Validation

Before packaging any skill, run from inside the skill directory:

```bash
python3 ~/.claude/skills/skill-creator/scripts/quick_validate.py
```

Packaging (`package_skill.py`) always validates first and will exit without producing a `.skill` file if validation fails.
