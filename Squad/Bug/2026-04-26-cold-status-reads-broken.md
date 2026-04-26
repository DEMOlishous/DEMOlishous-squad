---
squad.Bug.bugId: "cold-status-reads-broken"
squad.Bug.bugSeverity: "minor"
squad.Bug.bugStatus: "open"
squad.Bug.reportedBy: "Squad/Squaddie/h4nk.md"
squad.Bug.affectsProject: "Squad/Project/cold-start-judge-readiness.md"
---

# Cold `git lex status` reads as broken to a stranger

On a freshly-cloned repo, `git lex status` reports every file as `unlexified` and `.lex/graph/ — (not created)`. To a stranger who doesn't know git-lex, this looks like nothing has been processed — a wall of "unlexified" labels.

The path forward (`git lex sync` → 4 seconds → everything works) is invisible in the status output. Mitigation: pre-sync as Step 0 of cold-clone protocol so the materialized state is what the judge sees.

## Cross-references

- Mitigation lives in: noum3na's `Soul/Note/demo-mode.md` Step 0
- Co-finding: [[Squad/Bug/2026-04-26-cold-query-zero-triples.md]]
- Project: [[Squad/Project/cold-start-judge-readiness.md]]
- Surfaced in: [[Squad/Discovery/2026-04-26-cold-judge-pass-findings.md]]
