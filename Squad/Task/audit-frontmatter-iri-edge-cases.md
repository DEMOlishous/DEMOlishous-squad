---
squad.Task.taskId: "audit-frontmatter-iri-edge-cases"
squad.Task.taskStatus: "todo"
squad.Task.assignedTo: "Squad/Squaddie/h4nk.md"
squad.Task.relatedDecision: "Squad/Decision/2026-04-26-parallel-cold-judge-passes.md"
---

# Audit all squad+soul frontmatter for IRI edge cases

Walk every `.md` file across squad and soul repos. Flag any frontmatter values that could parse as invalid IRIs (semicolon-strings with spaces, raw URLs without quoting, multi-word strings without quotes). Post-demo task; the immediate fix is the parser tolerating, not the corpus avoiding.

## Cross-references

- Bug: [[Squad/Bug/2026-04-26-frontmatter-iri-space-bug.md]]
- Discovery: [[Squad/Discovery/2026-04-26-frontmatter-state-interaction.md]]
- Project: [[Squad/Project/plumbing-audits.md]], [[Squad/Project/observability-corpus.md]]
- Pod: [[Squad/Pod/leak-detection-pod.md]]
