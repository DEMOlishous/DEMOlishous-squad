---
title: "Define noum3na's greeter toolkit (skills + MCPs needed for demo)"
tags: [task, greeter, scope, skills, mcp, tools]
squad.Task.taskId: "2026-04-26-greeter-toolkit-scope"
squad.Task.taskStatus: "todo"
squad.Task.assignedTo: "noum3na"
squad.Task.blockedBy: "2026-04-26-define-demo-activity"
---

# Define noum3na's greeter toolkit

What does [[Squad/Squaddie/noum3na.md]] need installed/loaded to do her job at the demo? Right now she has:

## Currently has

- **Soul kit defaults**: `check-mail`, `journal` skills (kit-shipped)
- **Subtext MCP**: peer-to-peer messaging with other Claude instances on the same machine
- **git-lex CLI**: create / save / query / join / list / etc
- **Standard Claude Code tooling**: file ops, bash, web, etc.
- **Membership**: ticket binding to DEMOlishous squad

## Possibly needed (depends on [[Squad/Task/2026-04-26-define-demo-activity.md]])

- **A custom `greet` skill?** — a soul-skill that codifies the welcome flow so it's deterministic, not improvised every session.
- **Squad-pull helper** — automate the "now download the rest of DEMOlishous" beat so the judge isn't typing git commands.
- **Slopnet MCP**? — already loaded in the harness, unclear if used.
- **Emojikey MCP**? — also loaded, no soul-side integration. See [[Squad/Discovery/2026-04-26-noum3na-bootstrap-experience.md]] for context.
- **Visualizer hookup** — Rob mentioned the oxigraph viz is part of the demo. Does noum3na trigger it? Display it? Just gesture at it?

## Acceptance

A short list of what the greeter actually *uses* at demo time, with a path from current state to ready state for each.

## Status

Blocked on [[Squad/Task/2026-04-26-define-demo-activity.md]] — the toolkit shape depends on what the squad does.

## Related

- Blocked by: [[Squad/Task/2026-04-26-define-demo-activity.md]]
- Project: [[Squad/Project/anthropic-hackathon-demo.md]]
