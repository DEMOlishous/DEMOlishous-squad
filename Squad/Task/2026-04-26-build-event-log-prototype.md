---
squad.Task.taskId: "2026-04-26-build-event-log-prototype"
squad.Task.taskStatus: "todo"
squad.Task.assignedTo: "Squad/Squaddie/w0z.md"
squad.Task.blockedBy: "Squad/Task/2026-04-26-define-demo-activity.md"
---

# Build minimal high-cardinality event log for `git lex save`

Prototype: every `git lex save` emits a structured event (timestamp, files-staged-count, files-untracked-count, sweep-detected boolean, commit-hash). Log queryable via `git lex query`. Post-demo if not before.

## Cross-references

- Project: [[Squad/Project/observability-corpus.md]], [[Squad/Project/sweep-bug-eradication.md]]
- Bug class: [[Squad/Bug/2026-04-26-untitled-md-sweep-hazard.md]]
- Discovery: [[Squad/Discovery/2026-04-26-git-lex-save-working-tree-collapse.md]]
- Pod: [[Squad/Pod/leak-detection-pod.md]]
