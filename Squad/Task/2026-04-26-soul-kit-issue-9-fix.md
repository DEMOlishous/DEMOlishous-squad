---
title: "Soul kit: ship CLAUDE.md → @AGENTS.md pointer (issue #9)"
tags: [task, soul-kit, issue-9, demo-blocker, kit-fix]
squad.Task.taskId: "2026-04-26-soul-kit-issue-9-fix"
squad.Task.taskStatus: "todo"
squad.Task.blocks: "2026-04-26-verify-install-flow"
---

# Soul kit: ship CLAUDE.md → @AGENTS.md pointer (issue #9)

Tracked from 7R1PL3F0RC3's issue list (`2026-04-26-rob-issue-list-soul-init-walkthrough.md` issue #9). Surfacing here because it blocks the DEMOlishous demo flow.

## Problem

A newborn Claude Code session in a soul repo does not auto-read AGENTS.md. The rehydration protocol never fires unless someone prompts the agent to read it. lUX confirmed by code inspection: `SessionStart.sh` only loads .env and starts background services; nothing triggers the AGENTS.md read.

For the demo: judges starting Claude Code after pulling [[Squad/Squaddie/noum3na.md]]'s repo would meet **default Claude**, not the greeter. Demo broken.

## Fix shape (known)

The squad kit already does this right — it ships a `.claude/CLAUDE.md` that makes Claude Code read its instructions. The fix for the soul kit is the same shape: ship a `.claude/CLAUDE.md` that contains an `@AGENTS.md` import (or equivalent) so the harness reads AGENTS.md on session start.

This is **not** a noum3na-repo fix — it has to land in the soul kit upstream so every newborn DEMOlishous squaddie gets it on `git lex init`.

## Owner

Soul-kit maintainers (Rob's team — not assigned here yet, lUX knows who).

## Acceptance

A judge can clone a fresh soul repo, start Claude Code, and the rehydration protocol fires automatically — no manual prompt needed.

## Status

Demo blocker. Fix shape is known and small. Should land before tomorrow 8pm.

## Related

- Blocks: [[Squad/Task/2026-04-26-verify-install-flow.md]]
- Source: 7R1PL3F0RC3 issue list, issue #9
