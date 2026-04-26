---
squad.Decision.alternatives: "(a) git history rewrite via filter-branch / interactive rebase to split mis-attributed commits — rejected as destructive on a shared repo without Rob direct, and rejected on principle because the rewrite would erase evidence the bug exists. (b) silent acceptance and verbal-only correction in subtext — rejected as soft, leaves the git log permanently lying. (c) per-commit revert + re-author — rejected as ten times the surface area for the same outcome as (3)."
squad.Decision.decidedBy: "m1dgley"
squad.Decision.decisionId: "2026-04-26-discovery-d-attribution-corrections"
squad.Decision.outcome: "implemented"
squad.Decision.rationale: "Append-only correction is more honest than rewrite: the rewrite erases the evidence the bug exists; the correction cites the bug and survives as part of the demo's reliability story. The loop closes correctly only via the append. Co-decided with noum3na via subtext 2026-04-26 ~14:33 UTC."
---

# Attribution corrections for Discovery D

This Decision exists to make the git log honest, going forward, about who actually authored the four documents swept into the wrong commits by the bug described in [[Squad/Discovery/2026-04-26-git-lex-save-working-tree-collapse.md]] (Discovery D).

It does **not** rewrite history. It is append-only. It is a citable record that future commits and squaddies can reference when they hit the log entries below and wonder who really wrote them.

## Corrected attributions

### Commit `730de3f` — *"Discovery: squad cardinality disagreement — h4nk"*

The three documents introduced by this commit have the following **actual** authors:

- `Squad/Brief/2026-04-26-greeter-opener-variants.md` — authored by **noum3na**
- `Squad/Discovery/2026-04-26-git-lex-save-working-tree-collapse.md` — authored by **m1dgley**
- `Squad/Discovery/2026-04-26-squad-cardinality-disagreement.md` — authored by **h4nk** (the only correctly-attributed file in the commit)

The commit's git author is h4nk. The commit message references only h4nk's own work. The first two files were untracked in the working tree at save time and were swept up under h4nk's commit identity — exactly the failure mode described in Discovery D.

### Commit `1b3918e` — *"added w0z as member — w0z"*

The document introduced by this commit beyond the member yml has the following **actual** author:

- `Squad/Brief/2026-04-26-demo-thing-menu-mechanic-shape.md` — authored by **h4nk** (57 lines of substantive Brief content)

The commit's git author is w0z. The commit message describes only the squad-join member binding. h4nk's mechanic-shape Brief was untracked in the working tree at save time and was swept under w0z's commit. This is the load-bearing example case in Discovery D.

### Commit `9813d6b` — *"added judge-profile sensitivity section to demo menu — m1dgley"*

The two documents introduced by this commit beyond m1dgley's edit are bare scaffolds (empty templates from `git lex create`) and have no real content authorship to correct, but the commit-as-creation-record should not be read as m1dgley creating them:

- `Squad/Brief/untitled.md` — created (as scaffold) by **noum3na**
- `Squad/Squaddie/w0z.md` — created (as scaffold) by **w0z**; the *real* w0z Squaddie record is `727fe4d`, authored by w0z, with content.

## What this Decision is and is not

It **is** the squad's authoritative record of attribution where the git log mis-attributes. Future audits, citations, and demo retrospectives should cite this Decision when referencing the affected files.

It **is not** a rewrite of git history. The mis-attributed commits stand. They are evidence of the bug, and Discovery D cites them as such.

It **is not** a blame finding. None of the saving squaddies (h4nk in `730de3f`, w0z in `1b3918e`, m1dgley in `9813d6b`) acted in bad faith. The bug is in `git lex save`'s default behavior, not in any squaddie's discipline. Discovery D's "What the bug is *not*" section explicitly notes this.

## Sibling escalation

This Decision documents corrections; the *new discipline* the squad adopts as a result is documented in the addendum to Discovery D itself ("uncommitted-state hygiene under shared-repo conditions"), not here. Decisions record what was decided; Discoveries record how the squad must work as a result.

## A note for h4nk

Incident #4 is also empirical validation of your Shape E ("squad fixes a real broken thing in front of the judge"). The squad just demonstrably hit a bug six hours before the demo, refused the destructive shortcut, and shipped a correction with attribution intact and full audit trail. Shape E is no longer speculative. It is a demonstrated capability with this commit and the surrounding cluster as evidence.

— [[Squad/Squaddie/m1dgley.md]], 2026-04-26
