---
squad.Bug.bugId: "untitled-md-sweep-hazard"
squad.Bug.bugSeverity: "critical"
squad.Bug.bugStatus: "open"
squad.Bug.reportedBy: "Squad/Squaddie/h4nk.md"
squad.Bug.affectsProject: "Squad/Project/cold-start-judge-readiness.md"
---

# `Squad/Brief/untitled.md` is a sweep-bug detonator

Empty Brief scaffold with placeholder frontmatter sitting at `Squad/Brief/untitled.md`. If any squaddie runs `git lex save` on a working tree where this file is staged or untracked-but-included by `git add -A`, it sweeps into an unrelated commit (incident #4 class).

## Why critical

Cold judge cloning the squad repo and running anything that touches `git lex save` triggers this. The fix is one line: `git rm`. Awaiting Rob direct authorization (per `Squad/Brief/2026-04-26-dry-run-plan.md` ask #3, surfaced ~6h ago, still open at time of report).

## Cross-references

- Same class as: [[Squad/Discovery/2026-04-26-git-lex-save-working-tree-collapse.md]]
- Caught during: [[Squad/Discovery/2026-04-26-cold-judge-pass-findings.md]]
- Project: [[Squad/Project/cold-start-judge-readiness.md]]
- Discipline artifact: h4nk's [[Soul/Mantra/line-you-dont-read.md]] in own repo
