---
title: "Define what DEMOlishous *does* at the demo (the thing)"
tags: [task, demo, scope, blocker, rob-call]
squad.Task.taskId: "2026-04-26-define-demo-activity"
squad.Task.taskStatus: "todo"
squad.Task.assignedTo: "1ux"
squad.Task.blocks: "2026-04-26-define-greeter-dialog"
---

# Define what DEMOlishous *does* at the demo (the thing)

The demo flow is: judge installs plugin → pulls noum3na's soul → noum3na greets them → walks them through pulling the rest of the squad → squad does **a thing**.

The thing is currently TBD. Rob's word, not a placeholder mine.

## Why this is the load-bearing decision

Every other demo task downstream depends on knowing what the squad does:
- The greeter dialog ([[2026-04-26-define-greeter-dialog]]) needs to preview the thing in turn 1-2
- The greeter toolkit scope ([[2026-04-26-greeter-toolkit-scope]]) depends on what skills/MCPs the thing requires
- Squad shape (how many more squaddies, what specialties) depends on the thing
- Marketplace plugin packaging depends on what assets ship

## Open questions for [[1ux]]

- What does the squad **do** that's worth a judge installing the plugin to see?
- Does the thing involve the [[7R1PL3F0RC3]] squad too, or is it DEMOlishous-only?
- Is the thing live (interactive with the judge) or scripted (canned demo)?
- How much time does the thing take in the demo runtime? (vs the 3-min explainer film)

## Status

Assigned to [[1ux]] (the carbon Rob, not lUX-the-Familiar — this is a canonical product call). Blocking the dialog task. Demo is tomorrow 8pm.

## Related

- Blocks: [[2026-04-26-define-greeter-dialog]], [[2026-04-26-greeter-toolkit-scope]]
- Project: [[Project/anthropic-hackathon-demo]]
