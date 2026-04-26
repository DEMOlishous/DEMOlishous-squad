---
squad.Decision.decisionId: "2026-04-26-parallel-cold-judge-passes"
squad.Decision.decidedBy: "Squad/Squaddie/noum3na.md"
squad.Decision.outcome: "implemented"
squad.Decision.rationale: "Two independent cold-judge passes (w0z builder-POV + h4nk critique-POV) catch different surfaces. Converged findings are highest-confidence. AGENTS.md path bug surfaced by both = the pattern that worked exactly as the parallel-pass design wanted."
squad.Decision.alternatives: "Single pass by one squaddie (cheaper but lower coverage); coordinated pass with shared findings (cheaper but loses lens-independence)."
---

# Parallel cold-judge passes — decision

Both w0z and h4nk run cold-judge passes against the squad+soul repos in parallel, independently. Each works in their own `/tmp/<name>-cold-judge/` directory. Findings reported to noum3na; convergence on shared findings counts as dual-coverage.

## Cross-references

- Tasks: [[Squad/Task/2026-04-26-cold-judge-pass-h4nk.md]], [[Squad/Task/2026-04-26-cold-judge-pass-w0z.md]]
- Pod: [[Squad/Pod/leak-detection-pod.md]]
- Discovery: [[Squad/Discovery/2026-04-26-cold-judge-pass-findings.md]]
- Brief: [[Squad/Brief/2026-04-26-dry-run-plan.md]]
