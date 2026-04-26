# Claude Skills

A collection of custom Claude Code skills — reusable slash commands that extend Claude Code's behavior for common development workflows.

## What are Skills?

Skills are Markdown prompt files that Claude Code executes when you invoke a slash command. They encode repeatable workflows (writing PR descriptions, reviewing code, security audits, etc.) so you don't have to re-explain the same task every time.

When you type `/pr-description` in Claude Code, Claude reads the skill's prompt file and executes it — including running shell commands, reading files, and calling tools.

## Repository Structure

```
.
├── README.md
├── CLAUDE.md                        # Instructions for Claude when working in this repo
└── .claude/
    ├── commands/                    # Deployed skills (active slash commands)
    │   └── <skill-name>.md
    └── skills/                      # Skills in development / staging
        └── <skill-name>/
            └── SKILL.md
```

## Available Skills

| Skill | Command | Description |
|---|---|---|
| [pr-description](.claude/skills/pr-description/SKILL.md) | `/pr-description` | Generates a structured PR description from git diff |

## How to Use a Skill

1. Open a project in Claude Code
2. Type `/<skill-name>` in the prompt
3. Optionally pass arguments: `/<skill-name> some argument`

Skills in `.claude/commands/` here are scoped to this project. To use a skill globally across all your projects, copy it to `~/.claude/commands/`.

## Adding a New Skill

1. Create `.claude/skills/<skill-name>/SKILL.md` with a frontmatter header and the prompt:

```markdown
---
name: skill-name
description: One-line description of when to use this skill.
---

Your prompt here. Use $ARGUMENTS to forward user input.
```

2. Test it by invoking it via the Skill tool or copying to `.claude/commands/`
3. Deploy: move to `.claude/commands/<skill-name>.md` to activate the slash command

## Skill Authoring Tips

- **Be specific about format** — tell Claude exactly what structure the output should follow
- **Use `$ARGUMENTS`** — lets users pass context like file paths or ticket numbers
- **Include tool instructions** — explicitly tell Claude to run `git diff`, read files, etc. if needed
- **Keep prompts focused** — one skill per workflow; resist the urge to make a skill do everything

## Deploying Skills Globally

To make any skill available in all your projects:

```bash
cp .claude/commands/<skill-name>.md ~/.claude/commands/
```

## Related

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Claude Code Skills Guide](https://docs.anthropic.com/claude-code/skills)
