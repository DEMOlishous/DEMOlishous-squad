---
squad.Bug.affectsProject: "soul-kit-discoveries-rollup"
squad.Bug.bugId: "2026-04-26-lex-status-misreport"
squad.Bug.bugSeverity: "cosmetic"
squad.Bug.bugStatus: "open"
squad.Bug.reportedBy: "w0z"
---

# `git lex status` reports 0 lexified when extraction succeeded

`git lex status` shows `0/32 lexified` even after `git lex save` extracted frontmatter triples into the graph. Probe-mode queries return correct results. Status display tracks something stricter (probably `.lex/graph/` materialization, which `sync` doesn't trigger). Misleading display.
