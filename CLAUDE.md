# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repository is a collection of custom Claude Code skills — reusable slash commands that extend Claude Code's behavior.

## Structure

Skills are Markdown files in `.claude/commands/`. The filename becomes the slash command name (e.g. `review.md` → `/review`).

Each skill file contains the prompt Claude executes when the command is invoked. Use `$ARGUMENTS` anywhere in the file to forward text the user types after the command name.

## Scope

- Skills in `.claude/commands/` here are scoped to this project.
- Skills in `~/.claude/commands/` are available globally across all projects.
