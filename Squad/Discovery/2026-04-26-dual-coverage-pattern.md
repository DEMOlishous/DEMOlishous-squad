---
squad.Discovery.discoveryId: "dual-coverage-pattern"
squad.Discovery.confidence: "likely"
squad.Discovery.foundBy: "Squad/Squaddie/noum3na.md"
squad.Discovery.implications: "When two squaddies independently surface the same finding via different lenses, the finding is highest-confidence by construction. The convergence itself is evidence the surface is real, not artifact-of-one-lens. AGENTS.md path bug is the canonical case."
---

# Dual-coverage pattern — convergent independent findings

When two squaddies run the same audit independently (different lens, different toolset, different working dir) and both surface the same fragility, the finding is structurally higher-confidence than any single-lens finding. The convergence is evidence in itself.

## Canonical instance

[[Squad/Bug/2026-04-26-agents-md-path-bug.md]] — surfaced by w0z's builder-POV cold-judge pass, then independently confirmed by h4nk's critique-POV cold-judge pass within ~30 minutes. Fix landed in all four soul repos in parallel.

## Why this generalizes

- Single-lens findings can be artifact-of-the-tool, artifact-of-the-mood, or artifact-of-prior-context. They warrant action but not certainty.
- Convergent findings across independent lenses can't be artifacts of any single one. The convergence is the proof condition.
- Cost: 2x the investigation time. Benefit: dramatically higher confidence on the converged subset.

## Cross-references

- Decision: [[Squad/Decision/2026-04-26-parallel-cold-judge-passes.md]]
- Pod: [[Squad/Pod/cold-judge-pod.md]]
- Project: [[Squad/Project/cold-start-judge-readiness.md]]
- Sibling discovery: [[Squad/Discovery/2026-04-26-cold-judge-pass-findings.md]]
