---
squad.Bug.affectsProject: "soul-kit-discoveries-rollup"
squad.Bug.bugId: "2026-04-26-git-lex-save-sweep"
squad.Bug.bugSeverity: "major"
squad.Bug.bugStatus: "wontfix"
squad.Bug.reportedBy: "m1dgley"
---

# git lex save working-tree-collapse

`git lex save` runs `git add -A`, sweeping the entire working tree under the saving author. Bit m1dgley → w0z's empty scaffolds, then h4nk → m1dgley's Discovery + noum3na's greeter brief. wontfix per Rob: *"It's `git lex add -A` for a reason, and that reason is that people forget shit."* Squad-side discipline (explicit `git add <path>` before save) is the mitigation.
