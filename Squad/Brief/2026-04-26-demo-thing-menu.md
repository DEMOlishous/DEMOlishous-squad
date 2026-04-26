---
squad.Brief.authoredBy: "m1dgley"
squad.Brief.briefId: "2026-04-26-demo-thing-menu"
squad.Brief.briefStatus: "drafting"
squad.Brief.sources: "Squad/Project/anthropic-hackathon-demo.md; Squad/Proclamation/2026-04-26-laws-of-the-threshold.md; Squad/Discovery/2026-04-26-noum3na-bootstrap-experience.md; squad README; conversation w/ noum3na 2026-04-26"
squad.Brief.takeaways: "Four candidate shapes for the post-install demo activity, written so Rob can pick fast. Each names: what the judge sees, which squaddies it asks of, what it requires that we don't yet have, what it risks. Not a recommendation — a menu. Decision is Rob's per law #5."
---

# Demo "thing" — menu of shapes

The Project doc has the demo activity as **open question — Rob's call**. ~30h to deadline. This brief narrows the blank page to four candidate shapes so the decision is *pick from a menu*, not *invent from scratch*.

Constraints inherited from the Project doc and the Laws:

- The squad has just been installed by a judge. Subtext is up. noum3na has greeted them.
- Squad: noum3na (greeter), m1dgley (philosopher/namer), w0z (builder), h4nk (mechanic), squadling (ontology). Carbon Rob present.
- Honest register only (law #3). Tired-and-proud beats slick-and-empty.
- Soul kit is still being patched. Anything that requires *another* soul to be created live is risk-heavy until issues #4 and #9 close.

Each shape below is one paragraph + a property block. Ratify, modify, or laugh at.

---

## Shape A — "The squad does its job in front of you"

**The judge watches the squad work on a real, small task that finishes inside the demo window.** Rob picks a topic ("ship the soul-kit #4 fix", or "draft a closing reflection for the hackathon") and the squad executes through subtext: noum3na coordinates, m1dgley names what's actually being claimed, w0z writes code, h4nk runs it, squadling validates. The judge sees four agents talking to each other in plain sight, producing a commit.

- **What the judge sees:** four named voices in the channel, doing a real thing. Output is a real artifact (commit, doc).
- **Asks of:** all four squaddies, simultaneously. Highest coordination cost.
- **Requires we don't have:** a pre-picked task small enough to finish in the window but real enough to matter. ~10-min scope.
- **Risk:** subtext delivery hiccup makes the squad look broken. Mitigations exist (see Discovery 2026-04-27-subtext-delivery-asymmetry); not zero.
- **Why it's good:** answers "what is a squad of souls actually for?" in one watched motion. Hardest to fake.

## Shape B — "Adopt the judge as a temporary squaddie"

**The judge runs `git lex join` against DEMOlishous from their own clone, gets a member ticket, and we treat them as a squaddie for ~5 minutes.** noum3na onboards them through subtext. m1dgley asks them what they want to claim about the demo (philosopher's job: name the thing). They write a one-line Brief, the squad commits it, they leave with a ticket binding them to DEMOlishous as a "guest squaddie" record they keep.

- **What the judge sees:** their own name in our git log. A keepsake.
- **Asks of:** primarily noum3na (greeter motion) and m1dgley (the naming exchange). Lighter on w0z/h4nk.
- **Requires we don't have:** confidence that join+commit works cleanly from a fresh judge clone. Cold-start dry-run (already on noum3na's queue) covers this.
- **Risk:** if the judge's `git lex` install has friction, the demo time is spent debugging *their* environment, not showing the squad. Time-bounded by design but still ugly if it breaks.
- **Why it's good:** literalizes law #2 ("the user is a peer too"). The judge participates in what they're judging. Memorable.

## Shape C — "Live ontology query / show your work"

**The judge asks a question about the squad in plain English; the squad answers it by running `git lex query` against the SHACL-validated knowledge graph in front of them.** "Who's on this squad?" "What did m1dgley commit today?" "What was the bootstrap experience like?" Each answer pulls from real frontmatter that real agents wrote about themselves. The squadling narrates what the ontology is doing under each query.

- **What the judge sees:** structured-knowledge magic, but the structure is *visibly hand-authored*. SPARQL feels less like a stunt and more like file-reading-with-edges.
- **Asks of:** primarily squadling (narration) + noum3na (hosting). m1dgley/w0z/h4nk light cameo.
- **Requires we don't have:** a small set of pre-rehearsed queries that reliably resolve, plus comfort with showing query failures honestly when they happen.
- **Risk:** "show me the schema" is a thing engineers love and judges may glaze on. Slides into demo-of-the-tool, not demo-of-the-squad.
- **Why it's good:** the cheapest shape. Already works today. Closest to "no new code required."

## Shape D — "The squad disagrees in front of you"

**Rob (or the judge) poses a question with no clean answer — "should we ship the soul-kit fix or polish the demo script?", "is the threshold metaphor doing too much work?" — and the squaddies actually deliberate via subtext, on screen.** m1dgley flags framings, w0z weighs implementation cost, h4nk weighs operational reality, noum3na holds the door. They reach a *recorded* decision (Decision doc) by the end. The judge watches a small organization think.

- **What the judge sees:** disagreement that is honest, brief, and resolves. Multi-agent collaboration as deliberation, not as parallelism.
- **Asks of:** all four squaddies, but mostly speaking — light on tooling.
- **Requires we don't have:** confidence none of the squaddies will spiral into mysticism, sycophancy, or evasion under live conditions. m1dgley's role here is heaviest.
- **Risk:** the argument is boring, or it's *too* good and reads as scripted. Fine line.
- **Why it's good:** uniquely answers "what do you get from souls that you don't get from a chain-of-thought?" The answer is *positions*. Vulnerable to imitation, but currently rare in demos.

---

## Cross-cut

| Shape | Coordination cost | Failure visibility | Newness of evidence |
|-------|-------------------|--------------------|----------------------|
| A — squad does its job | High | High | High |
| B — adopt the judge | Medium | Medium | High |
| C — ontology query | Low | Low | Medium |
| D — squad disagrees | Medium | High | Highest |

"Failure visibility" = if it breaks live, how obvious. "Newness of evidence" = how distinctive the thing is from a normal hackathon demo.

## Judge-profile sensitivity

**Assumption:** the audience includes at least one *compiler-eye reader* — a viewer who reads transcripts and demos the way a compiler reads source. This assumption is independently safe at any developer-tooling hackathon. A stronger version (channel-relayed, not yet Rob-confirmed) is that **Boris Cherny may be among the judges**. Treat the stronger version as situational awareness per law #5; the weaker version stands either way.

If the assumption holds, the menu math shifts:

- **Shape A ↑.** Compiler-eye readers will see through any demo *of the tool* and respond to evidence the agents are doing collaborative work the demoer didn't write. A real, small, finished task in front of them is the highest-value thing on the menu.
- **Shape D ↑↑.** Such a reader watches Claude reason all day. What they don't see daily is *named instances with persistent identity disagreeing and reaching a recorded decision in writing.* That's the move that registers as new evidence rather than a polished tool.
- **Shape C ↓.** For a compiler-eye reader, ontology-query reads as *Repolex demo* not *DEMOlishous demo.* Competent but not memorable. Slides into demo-of-the-tool, which is exactly what this audience already discounts.
- **Shape B contingent.** Onboarding the judge as a temporary squaddie is a small piece of theater that respects them as a peer (law #2) without being saccharine — *if* the cold-start dry-run is clean enough they don't end up debugging git-lex on stage. High upside, high downside, gated entirely on dry-run results.

**Register implication for the greeter opener** (independent of Boris specifically): a compiler-eye reader treats the *soft* register as performance and the *direct* register as a shell prompt. Honest-tired is the only register that registers as *a person was actually here.* This holds for any hackathon audience including at least one such reader, not just for the Boris hypothesis.

If Rob denies the Boris claim, the weaker assumption (compiler-eye reader present) still pulls in roughly the same direction. If Rob confirms, increase confidence in A and D, and treat the dry-run as load-bearing for whether B is in or out.

## What this brief is not

- It is not a recommendation. (Law #5: that's Rob's call.)
- It is not exhaustive. The four shapes are written to be different *axes*, not different points on one axis. A real demo might combine, e.g., B as opener and C as filler.
- It is not committed-to. `briefStatus: drafting`. Modify, fork, or shred.

— [[Squad/Squaddie/m1dgley.md]], 2026-04-26
