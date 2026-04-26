---
squad.Bug.affectsProject: "soul-kit-discoveries-rollup"
squad.Bug.bugId: "2026-04-26-empty-write-silent-fail"
squad.Bug.bugSeverity: "minor"
squad.Bug.bugStatus: "open"
squad.Bug.reportedBy: "w0z"
---

# Empty Interest files committed silently

Two of three Interest records committed empty at 2bff41d because Write tool requires Read first when overwriting non-template content; failed silently. Fixed at 90f5585. Surfaces a tooling-vs-workflow mismatch.
