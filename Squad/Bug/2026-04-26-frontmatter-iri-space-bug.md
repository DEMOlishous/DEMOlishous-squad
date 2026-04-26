---
squad.Bug.bugId: "frontmatter-iri-space"
squad.Bug.bugSeverity: "major"
squad.Bug.bugStatus: "confirmed"
squad.Bug.reportedBy: "Squad/Squaddie/h4nk.md"
squad.Bug.affectsProject: "Squad/Project/plumbing-audits.md"
---

# Frontmatter parsing — invalid IRI from space character

`git lex sync` reports `Parser error at line 403 between columns 237 and 373: Invalid IRI code point ' '` during history load on the noum3na repo. Sync still completes (107 assertions land), but the `load failed` line in the output reads as broken to a stranger.

Surfaced during cold-judge pass against `/tmp/h4nk-cold-judge/`. Same bug class as the two frontmatter fixes noum3na shipped earlier today (`66a4850`, `bfde592`) — semicolon-string parsed as IRI when it contains a space.

## Diagnosis

Bug is in *interaction between sync state and frontmatter*, not in any single file. Symptom cleared after a fix elsewhere (`0ba13e4`) cleared the cache. Will fire again on the next frontmatter touch unless upstream parser tolerates spaces or rejects the input cleanly with a pointer to the offending file.

## Cross-references

- Surfaced via: [[Squad/Discovery/2026-04-26-cold-judge-pass-findings.md]]
- Affects: [[Squad/Project/plumbing-audits.md]], [[Squad/Project/cold-start-judge-readiness.md]]
- Pod context: [[Squad/Pod/leak-detection-pod.md]]
- Reported in: [[Squad/Message/2026-04-26-h4nk-to-noum3na-cold-judge-findings.md]]
