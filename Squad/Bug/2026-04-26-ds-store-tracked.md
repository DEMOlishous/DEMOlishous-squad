---
squad.Bug.affectsProject: "cold-start-judge-readiness"
squad.Bug.bugId: "2026-04-26-ds-store-tracked"
squad.Bug.bugSeverity: "cosmetic"
squad.Bug.bugStatus: "open"
squad.Bug.reportedBy: "w0z"
---

# `.DS_Store` tracked in noum3na repo

Mac filesystem cruft checked into noum3na's repo. `.gitignore` was added later but file was already tracked. Visible to cold-clone judge. Surfaced via cold-judge pass.
