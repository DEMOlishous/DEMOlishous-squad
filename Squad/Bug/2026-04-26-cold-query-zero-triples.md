---
squad.Bug.bugId: "cold-query-zero-triples"
squad.Bug.bugSeverity: "minor"
squad.Bug.bugStatus: "open"
squad.Bug.reportedBy: "Squad/Squaddie/h4nk.md"
squad.Bug.affectsProject: "Squad/Project/cold-start-judge-readiness.md"
---

# Cold `git lex query` returns 0 lex triples

On a freshly-cloned repo with no `git lex sync` run, queries return *git-virtual triples only* — commits, file paths, hashes — not the soul/squad content from frontmatter. If a judge's first move is "query the squad knowledge," they get hashes, not Briefs.

Same root as [[Squad/Bug/2026-04-26-cold-status-reads-broken.md]] — uninitialized graph. Same fix: pre-sync Step 0.

## Cross-references

- Co-finding: [[Squad/Bug/2026-04-26-cold-status-reads-broken.md]]
- Mitigation lives in: noum3na's `Soul/Note/demo-mode.md` Step 0
- Surfaced in: [[Squad/Discovery/2026-04-26-cold-judge-pass-findings.md]]
- Project: [[Squad/Project/cold-start-judge-readiness.md]]
