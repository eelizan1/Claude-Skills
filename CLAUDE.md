# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repository is a collection of custom Claude Code skills — reusable slash commands that extend Claude Code's behavior. Skills allow you to encode repeatable workflows (code review, PR descriptions, security audits, etc.) as prompts that Claude executes on demand.

## Repository Structure

```
.
├── CLAUDE.md                        # This file
└── .claude/
    ├── commands/                    # Deployed skills (active slash commands)
    │   └── <skill-name>.md          # Becomes /<skill-name> command
    └── skills/                      # Skills in development
        └── <skill-name>/
            └── SKILL.md             # Skill prompt definition
```

## How Skills Work

Skills are Markdown files containing the prompt Claude executes when the command is invoked.

- The **filename** (without `.md`) becomes the slash command name: `review.md` → `/review`
- Use `$ARGUMENTS` anywhere in the file to forward text the user types after the command name: `/review src/api.ts` passes `src/api.ts` as `$ARGUMENTS`
- Skills can use any tools available to Claude Code (file reads, bash, web search, etc.)

## Skill Lifecycle

1. **Develop** — draft the skill prompt in `.claude/skills/<name>/SKILL.md`
2. **Test** — invoke it manually or via the Skill tool to verify behavior
3. **Deploy** — copy or move to `.claude/commands/<name>.md` to activate the slash command

## Scope

| Location | Scope |
|---|---|
| `.claude/commands/` (this repo) | This project only |
| `~/.claude/commands/` | Global — all projects |

To make a skill available everywhere, add it to `~/.claude/commands/`.

## Adding a New Skill

1. Create `.claude/skills/<skill-name>/SKILL.md` with the prompt
2. Test the skill by running it via the Skill tool or copying to commands/
3. Deploy to `.claude/commands/<skill-name>.md` when ready
