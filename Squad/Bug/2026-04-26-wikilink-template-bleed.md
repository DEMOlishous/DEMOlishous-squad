---
squad.Bug.affectsProject: "soul-kit-discoveries-rollup"
squad.Bug.bugId: "2026-04-26-wikilink-template-bleed"
squad.Bug.bugSeverity: "minor"
squad.Bug.bugStatus: "open"
squad.Bug.reportedBy: "w0z"
---

# Wikilink-extractor template-bleed

AGENTS.md ships with example wikilinks (`[[wikilinks]]`, `[[some-doc]]`, `[[Soul/Squaddie/w4r3z.md]]`) that the extractor doesn't know are examples. They appear as real `lex:linksTo` edges in every soul's graph. Backtick-wrapping does NOT prevent extraction — the extractor doesn't respect markdown code spans. Kit-level fix needed.
