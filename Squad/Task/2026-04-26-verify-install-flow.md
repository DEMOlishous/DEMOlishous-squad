---
title: "Verify install-and-meet flow end-to-end (judge dry-run)"
tags: [task, demo, install, dry-run, verification]
squad.Task.taskId: "2026-04-26-verify-install-flow"
squad.Task.taskStatus: "blocked"
squad.Task.assignedTo: "noum3na"
squad.Task.blockedBy: "2026-04-26-soul-kit-issue-9-fix"
---

# Verify install-and-meet flow end-to-end (judge dry-run)

Pretend to be a judge. Walk the actual install path:

1. Fresh machine state (or fresh checkout)
2. Install the m4rq + spaceG.O.A.T. marketplace plugin
3. Clone `github.com/DEMOlishous/noum3na`
4. Start Claude Code in the cloned repo
5. Observe: does noum3na greet me, or do I get default Claude?
6. Continue: can I `git lex join` the squad? Pull the rest of DEMOlishous?

## What to watch for

- **Issue #7**: does the install need `--dangerously-load-development-channels`? If yes, judges hit a usability blocker.
- **Issue #9**: does AGENTS.md auto-fire on session start? If no, the greeter never wakes up. (As of 2026-04-26, NO. Soul-kit fix needed — see [[2026-04-26-soul-kit-issue-9-fix]].)
- **Subtext loaded?** Without subtext, the "you can talk to other DEMOlishous members" beat doesn't work.
- **Does the README make sense to a stranger?** I wrote it from inside, and that's a different read than from outside.

## Acceptance

- A judge with no prior context can install, clone, start Claude Code, and within ~30 seconds see something that looks like a soul greeting them, not raw Claude.
- They can then ask "what next" and be walked into the squad-pull flow without manual hand-holding from Rob.

## Status

Blocked on [[2026-04-26-soul-kit-issue-9-fix]] — running this dry-run before the fix lands just re-confirms #9 is broken.

## Related

- Blocked by: [[2026-04-26-soul-kit-issue-9-fix]]
- Project: [[Project/anthropic-hackathon-demo]]
