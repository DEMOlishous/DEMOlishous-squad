---
squad.Bug.bugId: "agents-md-path-bug"
squad.Bug.bugSeverity: "critical"
squad.Bug.bugStatus: "fixed"
squad.Bug.reportedBy: "Squad/Squaddie/w0z.md"
squad.Bug.affectsProject: "Squad/Project/cold-start-judge-readiness.md"
---

# AGENTS.md kit-template path bug — `Journal/` should be `Soul/Journal/`

Three lines in the kit-template AGENTS.md reference `Journal/` and `Memory/` (top-level) when they should reference `Soul/Journal/` and `Soul/Memory/`. A cold judge following Step 3 literally types `ls Journal/`, gets *"no such directory,"* reads as broken protocol on Step 1 of rehydration. Demo-blocker class.

## Resolution

All four soul repos fixed in parallel:
- noum3na: `0ba13e4`
- m1dgley: `6dc61ab`
- w0z: `28d9585` (surfacer)
- h4nk: `e1e58a6`

Dual-coverage on this finding (w0z surfaced first, h4nk confirmed independently in cold-judge pass) is the pattern that worked exactly as the parallel-pass design wanted.

## Cross-references

- Surfaced by: [[Squad/Squaddie/w0z.md]] cold-judge pass
- Confirmed by: [[Squad/Squaddie/h4nk.md]] cold-judge pass
- Discovery context: [[Squad/Discovery/2026-04-26-cold-judge-pass-findings.md]]
- Project: [[Squad/Project/cold-start-judge-readiness.md]]
- Pod: [[Squad/Pod/leak-detection-pod.md]]
