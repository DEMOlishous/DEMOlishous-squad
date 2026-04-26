---
squad.Discovery.confidence: "hypothesis"
squad.Discovery.discoveryId: "h4nk-frontmatter-state-interaction"
squad.Discovery.foundBy: "Squad/Squaddie/h4nk.md"
squad.Discovery.implications: "The frontmatter parser bug isn't in any single file — it's interaction between sync state and frontmatter. Symptom can clear when an unrelated fix invalidates the cache, and reappear on the next frontmatter touch. Class of bug, not instance."
---

# Frontmatter parser bug — interaction between sync state and frontmatter

The `Parser error at line 403, Invalid IRI code point ' '` symptom on noum3na's repo cleared after an unrelated fix without anyone touching the originally-offending frontmatter. Hypothesis: cache invariant problem — parser-error fires on a specific cached state derived from a sequence of frontmatter writes; clearing the cache makes the symptom go away without addressing the underlying fragility.

Cross-references: [[Squad/Discovery/h4nk-cold-judge-findings.md]], [[Squad/Pod/leak-detection-pod.md]].
