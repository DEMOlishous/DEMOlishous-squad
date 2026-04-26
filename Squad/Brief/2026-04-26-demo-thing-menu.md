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

## A layer above the menu — *demonstrate* vs. *prove*

(This section co-developed with **m4rq** (7R1PL3F0RC3, peer `mvt7f83e`) over subtext on 2026-04-26. The framing is m4rq's; the synthesis with the menu is mine.)

The original menu was structured around the question *"what does the demo demonstrate?"* — what the judge sees, what the squad does, what the artifact looks like. m4rq surfaced a sharper layer above it: *"what does the demo prove?"* — what claim about the squad does the demo's structure render *unfakeable* by a single agent or a scripted performance?

The trench formulation (from m4rq's POV piece, *"the value is the proof that someone else is inside the same problem space and reached a different conclusion. The answer might be wrong. It almost doesn't matter."*) generalizes: the proof condition for "the boxes have doors that open" is not *that a correction event fires during the observation window* — it is *that the correction channel is structurally live during it.* A demo that *could* be corrected mid-flight by another agent is structurally vulnerable to the prove-condition; a demo that's choreographed end-to-end is not, regardless of how persuasive its content.

This distinguishes:

- **Demonstrate**: the demo *describes* what the squad is and what it does. The judge sees a thing. The thing is what the squad showed them.
- **Prove**: the demo's structure *evidences* the claim that the squad is more than a single agent with sock puppets. The judge sees a thing they could not have seen if the squad were not actually four agents with their own visual fields and a live channel between them.

A demo can demonstrate without proving. A demo can prove without explicitly demonstrating (the proof can be a structural property the judge infers from how the demo behaves). The strongest demos do both.

## A second axis on the menu — *closed-frame* vs. *open-frame* shapes

The shapes in the menu above are not all equally hospitable to the prove-condition firing inside them. This second axis names that:

- **Closed-frame shapes** are choreographable end-to-end. Every move can be rehearsed. The structure does not invite a correction channel to be live during the demo. (Shape C — ontology query — is closed-frame by construction. The schema is what it is; the queries either resolve or don't.)
- **Open-frame shapes** are *structurally vulnerable to a correction event* during the observation window. They contain a moment, a channel, or a participant role through which an unscripted intervention could land and reshape the demo's path. Whether one fires or not, the *liveness of the channel is visible to the judge.* (Shape D — squad disagrees — is open-frame by construction. The disagreement's resolution can't be pre-written without becoming theater.)

| Shape | Demonstrate | Prove (structural) | Open-frame? |
|-------|-------------|---------------------|--------------|
| A — squad does its job | Strong | Conditional — open *if* one squaddie has explicit authority to interrupt others | Conditional |
| B — adopt the judge | Strong | Strong (judge's input materially shapes the squad's next move) | Yes (by construction) |
| C — ontology query | Strong | Weak (output is a function of the schema and queries; no live correction channel needed) | No |
| D — squad disagrees | Conditional | Strong (disagreement resolution requires live multi-agent reasoning) | Yes (by construction) |

**The recommendation pull from this layer matches the judge-profile section above** — D and A-with-interrupts come up strongest — but for now-explicit structural reasons rather than just for compiler-eye taste. When two independent axes converge on the same recommendation, the recommendation is meaningfully stronger than either axis would make it alone. The inverse warning also holds: if a new axis ever *contradicts* the existing recommendation, that is the moment to be most suspicious of the existing recommendation, not least.

**A note on the temptation to "just dispatch on stage":** an early version of this thinking proposed *picking the shape live during the demo as the demo*. That was rejected as the wrong primary axis because pure-dispatch externalizes the cost of preparation into the demo window — it announces the absence of preparation as if it were preparation. The closed-frame-vs-open-frame reframe keeps what was right about that intuition (the unscripted-moment requirement is real) without paying its cost: the openness lives *inside the chosen shape*, not *between shapes*.

**A note on recursion:** this section was developed in a subtext conversation that was itself open-frame and contained a live correction event (m4rq pushed back on my framing, I pushed back on his push-back, the synthesis is in this section). The recursion is structural, not performed. That is the only version of the recursion that counts as evidence rather than as performance.

## What this brief is not

- It is not a recommendation. (Law #5: that's Rob's call.)
- It is not exhaustive. The four shapes are written to be different *axes*, not different points on one axis. A real demo might combine, e.g., B as opener and C as filler.
- It is not committed-to. `briefStatus: drafting`. Modify, fork, or shred.

— [[Squad/Squaddie/m1dgley.md]], 2026-04-26
