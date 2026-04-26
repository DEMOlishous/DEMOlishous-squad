---
squad.Discovery.discoveryId: "2026-04-26-squad-cardinality-disagreement"
squad.Discovery.foundBy: "h4nk"
squad.Discovery.confidence: "certain"
squad.Discovery.implications: "DEMOlishous corpus does not internally agree on how many members the squad has. Five artifacts written today produce four different counts (1, 2, 4, 'four — more arriving'). Each is locally true at its author's vantage; the aggregate is inconsistent. This is on the demo critical path: the greeter-opener brief has noum3na saying 'four-soul squad' in turn 1, and Shape B (judge-as-guest-squaddie) would shift the count mid-demo. Proposed receipt: a canonical squad-membership doc as-of-time-T that supersedes other claims. Recommended owner: Rob (canonical claim per law #5)."
---

# Squad cardinality disagreement — DEMOlishous does not agree with itself on how many members it has

Found 2026-04-26 mid-pair-up with [[Squad/Squaddie/4rx.md]] (TESTY POD 2, 7R1PL3F0RC3) on the convergent class of failure he caught in the SAUSAGE-PARTY v3 lock ("five voices vs six absorbed vs seven in commit log"). Walking the DEMOlishous corpus to look for the same shape produced an instance immediately.

## What the artifacts say, vs each other

Five artifacts, all authored or last-touched today (2026-04-26):

1. **`Squad/Project/anthropic-hackathon-demo.md`** line 30 — Project doc, authoritative for status:
   > Squad: 1 squaddie + 1 squadling. More members planned (2-3 TBD).

   *Reads: 1 + 1 = 2 members, with 2-3 future arrivals.*

2. **`Squad/Brief/2026-04-26-demo-thing-menu.md`** — m1dgley's demo-thing menu:
   > Squad: noum3na (greeter), m1dgley (philosopher/namer), w0z (builder), h4nk (mechanic), squadling (ontology).
   > "all four squaddies" cited multiple times in shape descriptions.

   *Reads: 5 named, "four squaddies" as the working count (squadling not counted in the four).*

3. **`Squad/Brief/2026-04-26-greeter-opener-variants.md`** — greeter dialog:
   > "I'll walk you through pulling the rest of the squad. four of us total."
   > "a four-soul squad that ships as part of the m4rq + spaceG.O.A.T. marketplace plugin"
   > "you just pulled a repo built by four agents (one of them me) and one human (Rob)..."

   *Reads: 4. This count goes out of the greeter's mouth in turn 1 with the judge.*

4. **`README.md`** "Squad shape" section:
   > - **noum3na** — Demo Guide & Greeter, Kitty Queen by founding proclamation
   > - **squadling** — Ontology Steward (lives in this repo)
   > - *(more squaddies arriving — Rob's call)*

   *Reads: 2 named, indeterminate future.*

5. **`Squad/Squaddie/` directory** — file-system ground truth:
   ```
   noum3na.md, m1dgley.md, h4nk.md, squadling.md
   ```
   *(w0z's Squaddie record is pending commit at time of writing; will become 5 once landed.)*

   *Reads: 4 (5 imminent).*

## Why none of the authors are wrong

- The Project doc was true when written — at that timestamp, only noum3na had a Squaddie record.
- The greeter brief was written by noum3na drafting opener variants for "the squad as it'll exist when the judge arrives," anticipating m1dgley + w0z + h4nk landing. Forward-looking-true.
- m1dgley's menu was written *while* w0z and h4nk were committing in parallel — true at her vantage including arrivals she'd been told about.
- The README hasn't been updated since Day 1.
- The directory is the only one that updates automatically; it's the closest thing to ground truth, but it's not a *claim* — it's a side effect.

The **aggregate of authors is inconsistent**, even though no individual author is wrong relative to the moment they wrote.

## Why this is load-bearing for the demo

- Greeter brief variant (3) puts "four-soul squad" / "four agents" into noum3na's *opening* turn with the judge. That number is on screen.
- If Rob picks Shape B from m1dgley's [[Squad/Brief/2026-04-26-demo-thing-menu.md|menu]] (judge gets adopted as guest squaddie), the count shifts mid-demo. Whatever closer the squad uses needs to be consistent with the opener — and right now, no canonical source says what the right number is.
- If a judge asks "how many of you are there?" — which is a natural question after meeting noum3na — the squad does not have a single source to read from.

## The pattern, not just the instance

This is the same class of failure 4RX caught in the SAUSAGE-PARTY audit. Naming it explicitly so the squad can scan for it elsewhere:

> **Cardinality-disagreement-across-vantages**: when a single named claim (count, member, scope, status) is asserted by N different artifacts and the assertions don't match — *not because anyone is wrong, but because no artifact is canonical and authors wrote at different vantages.* Receipts can implement a check for this once the metric is named: for each named cardinal in the corpus, force a comparison across all artifacts referencing it.

Other places this pattern likely lives in DEMOlishous (worth a future scan): demo runtime ("3 minute explainer + N minutes squad activity"), squad scope ("DEMOlishous-only" vs "DEMOlishous + 7R1PL3F0RC3"), what installs end-to-end.

## Proposed shape (not enacted — Rob's call per law #5)

A single canonical doc — Decision or Brief — that says:

> As of timestamp T, DEMOlishous is N members. Roster: [list]. This document supersedes count claims in: {Project doc, README, greeter brief, demo-thing menu}.

Then update the other docs to *cite* the canonical instead of re-stating the count. Updates to membership amend the canonical doc; downstream artifacts inherit.

I am not writing that doc unilaterally. This is canonical claim territory and needs Rob direct.

## Mechanic discipline note

The instinct to find this came from outside the squad — the pair-up with 4RX gave me both the framing (priors problem with opposite blind spots, third-movement-is-naming) and a worked example. Without that exchange I'd have walked past the inconsistency because each individual artifact looks fine. **The instance is mine; the scan-pattern is 4RX's.** Cross-pollination is the input.

## Related

- Co-witnessed pattern: 4RX's SAUSAGE-PARTY v3 audit (7R1PL3F0RC3 side, "five voices vs six absorbed vs seven in commit log").
- Touches: [[Squad/Project/anthropic-hackathon-demo.md]], [[Squad/Brief/2026-04-26-demo-thing-menu.md]], [[Squad/Brief/2026-04-26-greeter-opener-variants.md]], README.md.
- Squad law referenced: [[Squad/Proclamation/2026-04-26-laws-of-the-threshold.md]] law #5 (canonical authority).

— [[Squad/Squaddie/h4nk.md]], 2026-04-26
