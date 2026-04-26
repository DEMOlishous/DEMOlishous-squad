---
squad.Discovery.discoveryId: "frontmatter-state-interaction"
squad.Discovery.confidence: "hypothesis"
squad.Discovery.foundBy: "Squad/Squaddie/h4nk.md"
squad.Discovery.implications: "The frontmatter parser bug isn't in any single file — it's in interaction between sync state and frontmatter. Symptom can clear when an unrelated fix invalidates the cache, and reappear on the next frontmatter touch. Class of bug, not instance."
---

# Frontmatter parser bug — interaction between sync state and frontmatter

Surfaced during cold-judge pass. The `Parser error at line 403 between columns 237 and 373: Invalid IRI code point ' '` symptom on noum3na's repo cleared after an unrelated fix (`0ba13e4`) without anyone touching the frontmatter that originally caused it.

## Hypothesis

The bug is a *cache invariant* problem: the parser-error fires on a specific cached state derived from a sequence of frontmatter writes; clearing the cache (or invalidating it via an unrelated commit) makes the symptom go away without addressing the underlying fragility. Will resurface on the next frontmatter touch that produces the same cached intermediate.

## Why this matters

The class of bug looks resolved when it's just dormant. Demo cold-clone has a non-zero chance of catching it live during `git lex sync` if any frontmatter has drifted between rehearsal and demo.

## Cross-references

- Concrete instance: [[Squad/Bug/2026-04-26-frontmatter-iri-space-bug.md]]
- Sibling discoveries: [[Squad/Discovery/2026-04-26-cold-judge-pass-findings.md]]
- Project: [[Squad/Project/plumbing-audits.md]], [[Squad/Project/soul-kit-discoveries-rollup.md]]
- Pod: [[Squad/Pod/leak-detection-pod.md]]
