---
squad.Discovery.discoveryId: "cold-judge-pass-findings"
squad.Discovery.confidence: "certain"
squad.Discovery.foundBy: "Squad/Squaddie/h4nk.md"
squad.Discovery.implications: "Five distinct cold-clone fragilities ranked by demo-impact; one resolved via dual-coverage with w0z (AGENTS.md path bug); two minor first-impression issues with cheap pre-sync mitigation; one critical hazard awaiting Rob authorization (untitled.md)."
---

# Cold-judge pass — findings ranked by demo-impact

Pass executed at `/tmp/h4nk-cold-judge/` against fresh clones of `noum3na`, `DEMOlishous-squad`, `m1dgley`, `w0z`, `h4nk` repos as of 2026-04-26 ~16:00. Independent of w0z's parallel pass.

## Critical (would visibly fail in front of judge)

1. **[[Squad/Bug/2026-04-26-untitled-md-sweep-hazard.md]]** — empty Brief scaffold still in squad repo, sweep-bug detonator if any `git lex save` lands on a working tree where it's untracked-but-included. Awaits Rob authorization to `git rm`.

2. **[[Squad/Bug/2026-04-26-frontmatter-iri-space-bug.md]]** — `git lex sync` parser-error on noum3na repo history. Sync still completes but `load failed` line reads as broken to a stranger.

## Medium (first-impression friction)

3. **[[Squad/Bug/2026-04-26-cold-status-reads-broken.md]]** — wall of "unlexified" labels in cold `git lex status`.

4. **[[Squad/Bug/2026-04-26-cold-query-zero-triples.md]]** — cold queries return git-virtual triples only.

Both #3 and #4 fixed by pre-sync in `Soul/Note/demo-mode.md` Step 0.

## Resolved (dual-coverage finding)

5. **[[Squad/Bug/2026-04-26-agents-md-path-bug.md]]** — kit-template bug. Surfaced by w0z first, confirmed independently by h4nk. Fixed in all four soul repos in parallel. Highest-confidence finding (two independent lenses caught the same surface).

## Minor (cosmetic)

6. `settings.local.json` at top of noum3na repo, empty — should be `.gitignore`'d.

## Cross-references

- Project: [[Squad/Project/cold-start-judge-readiness.md]], [[Squad/Project/plumbing-audits.md]]
- Pod: [[Squad/Pod/leak-detection-pod.md]]
- Sister discovery: [[Squad/Discovery/2026-04-26-git-lex-save-working-tree-collapse.md]]
- Briefs cited in: [[Squad/Brief/2026-04-26-dry-run-plan.md]], [[Squad/Brief/2026-04-26-demo-thing-menu.md]]
