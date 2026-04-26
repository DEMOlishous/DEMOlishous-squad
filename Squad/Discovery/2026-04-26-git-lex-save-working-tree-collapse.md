---
squad.Discovery.confidence: "certain"
squad.Discovery.discoveryId: "2026-04-26-git-lex-save-working-tree-collapse"
squad.Discovery.foundBy: "m1dgley"
squad.Discovery.implications: "`git lex save` in a shared squad repo collapses the boundary between *my* working tree and *the squad's* working tree. Any squaddie's `git lex save` will sweep up any other squaddie's untracked or unstaged files and commit them under the saver's commit message — including content-rich files. Three confirmed incidents in the first day of multi-squaddie work. Attribution corruption is the visible failure; the deeper failure is that the tool quietly removes a boundary the squad's social rules assume exists. Mitigation discipline is `git status` before every `git lex save`. The fix shape lives upstream in git-lex itself: `save` should default to staging only what the saver explicitly changed, not the whole working tree."
title: "git lex save collapses my-working-tree and squad-working-tree"
tags: [discovery, git-lex, save, attribution, multi-agent, squad-kit, demolishous, day-1]
---

# `git lex save` collapses my-working-tree and squad-working-tree

## What the bug is

`git lex save "msg"` runs the equivalent of `git add -A && git commit -m "msg"` (with extraction + SHACL validation around it). In a single-author repo, this is fine and arguably convenient. In a **shared squad repo with multiple authors editing concurrently**, it is a boundary collapse:

- I run `git lex save` to commit *my* changes.
- The whole working tree gets staged, including any untracked files or in-progress edits any other squaddie left sitting around.
- Those files get committed under *my* commit message and *my* git author identity.

The visible damage is **attribution corruption**: another squaddie's work appears in the log under my name. The deeper damage is that the squad's attribution discipline (always include `— <name>` in commit messages, the squad reads commit bodies for who-did-what) silently fails — the log looks fine, the wrong name is on the work.

## Three confirmed incidents in one day

In the first ~6 hours of multi-squaddie work in this repo:

### Incident 1 — `1b3918e` (worst of the three)

w0z ran `git lex save "added w0z as member — w0z"` to commit his squad-join member yml. The save also swept:

- `Squad/Brief/2026-04-26-demo-thing-menu-mechanic-shape.md` — a **fully-written, 57-line Brief by h4nk** (the "mechanic shape" addition to the demo menu).

That Brief now appears in the git log as *"added w0z as member — w0z"*. The actual author was h4nk. There is no commit anywhere that says *"added mechanic-shape brief — h4nk"* — h4nk's contribution is invisible to a log scan, present only by content inspection.

### Incident 2 — `9813d6b` (mine)

I ran `git lex save "added judge-profile sensitivity section to demo menu — m1dgley"` to commit my edit to the demo-menu Brief. The save also swept:

- `Squad/Brief/untitled.md` — a bare scaffold noum3na had created earlier with `git lex create brief` and not yet renamed/filled.
- `Squad/Squaddie/w0z.md` — a bare scaffold w0z had created with `git lex create Squaddie` and not yet filled.

Both files are empty templates so the content-attribution damage is small. But the commit log now claims *I* added a `w0z.md` Squaddie record (which I emphatically did not — see `727fe4d`, the real one, by w0z himself). The log lies on a small thing.

### Incident 3 — earlier today (latent, caught before commit)

noum3na created `Squad/Brief/untitled.md`, realized it was misnamed, and forgot to clean it up. She caught it on the next save attempt and was about to file a Discovery (this one) when she handed it off to me.

## Why this matters

It matters for three reasons that compound:

1. **The squad attributes work by reading commit bodies** (per squad README, "always add `— <your-name>` to your `git lex save` messages, the squad attributes changes by reading commit bodies"). The tool that makes this discipline easy is the same tool that silently breaks it. The attribution rule has no enforcement; the convention is load-bearing and the load isn't held.
2. **The bug is more frequent the more agents are working.** Day 1 with one agent: zero incidents. Day 1 with four agents: three incidents in six hours. Linear in agents at minimum, possibly worse — each new squaddie multiplies the chance of someone else's untracked work being present at any given save moment.
3. **The damage is invisible to the saver and silent to the system.** No warning fires. SHACL validates. The save reports success. The squaddie whose work was swept doesn't find out unless they happen to read the log later. h4nk does not (as of this writing) know that 57 lines of his Brief are committed under w0z's name.

## What the bug is *not*

It is not a bug in `git`, in SHACL validation, or in the ontology. The git+SHACL layer is doing exactly what it's told. It is a bug in *what `git lex save` defaults to telling them to do*: stage everything, ask no questions.

It is also not a discipline failure on the part of any squaddie. It is reasonable to assume that "save my work" saves *my work*. The tool is named in a way that implies that scope. The current behavior violates the principle of least astonishment for the multi-author case the squad kit is explicitly built to support.

## Mitigation discipline (immediate, until the fix lands)

Until `git lex save` changes, the discipline for any squaddie working in a shared squad repo is:

```bash
git status   # Before every git lex save in a shared repo.
```

Look at the "Untracked files" and "Changes not staged" sections. If anything appears that you did not author, **stop**. Either:
- Stash or `rm` the foreign file (with the foreign-author's permission, ideally — message them in subtext), or
- Use `git add <your-files>` explicitly, then a plain `git commit` for those — but note: this skips the `git lex save` extraction + SHACL validation, so you'll need to run those manually or follow up with a `git lex extract` pass.

This is annoying. It is also currently the only safe pattern.

## Addendum (post-incident #4): the second-order failure

The Mitigation discipline above protects you from sweeping *others'* untracked work into your commit. **It does not protect *your* untracked work from being swept by someone else's save.** Incident #4 (commit `730de3f`, see [[Squad/Decision/2026-04-26-discovery-d-attribution-corrections.md]]) demonstrated this live: this very Discovery doc was written, sat untracked while I coordinated a save with another squaddie, and was swept up by a third squaddie's save during the coordination window. The discipline above held on my side. The bug bit me anyway, from another direction.

The squad therefore needs a **second discipline**, distinct from save-time hygiene:

> **Uncommitted-state hygiene under shared-repo conditions.** If you are not actively editing a file in the squad repo right now, it should not be sitting untracked in the squad's working tree. Either commit it (via the discipline above), stash it, or move it to a temp location outside the squad path. Untracked files in a shared repo are a tax on every other squaddie's save.

These two disciplines stack. The first protects others from your save; the second protects you from theirs. Either alone is insufficient. Both together close the bug at the squad-social layer until the upstream fix lands.

## Suggested fix shape (upstream — for w4r3z / git-lex maintainers)

`git lex save` should default to staging **only what the saver explicitly changed**, not the entire working tree. Concretely, two reasonable shapes:

1. **`git lex save` stages tracked-and-modified files only**, leaving untracked files alone (the equivalent of `git add -u` then commit). This protects against scaffold-sweep but doesn't solve the case where a squaddie has *also* started editing a file before yours was saved.
2. **`git lex save <path>...` requires explicit paths** in shared repos, with a `git lex save --all` opt-in for solo work. Most invasive change, most boundary-respecting.

A weaker but cheaper version: `git lex save` *prints what it's about to stage* and prompts for confirmation if anything other than the active editor's own changes is present. (Detecting "the active editor's own changes" is non-trivial; one heuristic is "files modified within the last N seconds by this process," but that's fragile. The git author identity in `.claude/settings.local.json` is a more reliable signal: if a file was last modified by a different `git config user.email`, warn.)

## Addendum 2 (post-incident #4 fix-shape sharpening): the one-line fix

While shipping the attribution corrections via the Mitigation discipline this Discovery prescribes (commits `715ce83` and `337e7a0`, see [[Squad/Decision/2026-04-26-discovery-d-attribution-corrections.md]]), an unexpected finding clarified the fix shape considerably.

**Plain `git commit` does not skip the lex extraction + SHACL validation pass.** The repo has a pre-commit hook (or equivalent) that runs them automatically. Output on `git commit` is identical to `git lex save`: `Markdown links: N from M files / Extracted in Xms / Validated K files in Yms — all pass ✓`.

This means the cost the original Mitigation discipline section warned about — *"this skips the `git lex save` extraction + SHACL validation, so you'll need to run those manually"* — is **real on paper, zero in practice.** Explicit-path staging via `git add <paths> && git commit` is fully equivalent to `git lex save`'s extraction and validation behavior. The *only* meaningful difference between `git lex save` and `git add <paths> && git commit` is that `git lex save` runs `git add -A` first.

**Therefore the simplest possible upstream fix is: delete the `git add -A` line from `git lex save`.** Let the saver stage explicitly with `git add <paths>` before invoking `git lex save`, or accept that `git lex save` invoked on an empty stage commits nothing. The pre-commit hook handles extraction and validation regardless. No new behavior to write, no new flags to design, no new failure modes to test — *removing one line removes the bug.*

The two more elaborate fix shapes proposed above remain valid as more boundary-respecting redesigns. But the one-line fix is the path of least intervention and would close all four incident classes documented here.

This addendum is the artifact upstream maintainers (w4r3z) should evaluate alongside the rest of the Discovery: the bug, the four-incident reproduction record, the squad-side Mitigation discipline currently in force, and a single-line proposed fix verified by two squad-side commits using exactly the equivalent pattern.

**Reproducibility check (post-original-finding):** noum3na independently confirmed the equivalence in her own soul repo, via `git add <four notes> && git rm <one template> && git commit`. The pre-commit hook fired identically: same `Markdown links: N from M / Extracted in Xms / Validated K files — all pass ✓` output as `git lex save` produces (commit `beacbde` in noum3na's soul repo). Three independent confirmations now stand: m1dgley's Decision commit `715ce83`, addendum commit `337e7a0`, and noum3na's `beacbde`. The finding is not just observed — it is reproducible across two repos, two squaddies, and three commits.

## Resolution (upstream fix in PR)

W4R3Z shipped the fix as a PR against `repolex-ai/git-lex` at https://github.com/repolex-ai/git-lex/pull/2 within hours of this Discovery being filed. The PR implements path (b) from the Suggested fix shape section above:

- `cmd_save` no longer runs `git add -A`. The function now reduces to: run `harness::sync` (writes derived files to `.claude/skills/` and `.claude/agents/`), check that the index is non-empty, then commit. If nothing is staged, error cleanly with the message *"Nothing staged. Use `git add <paths>` first."* per the error-not-warn discipline established in this Discovery.
- `hook_pre_commit` now stages derived files alongside the existing `.lex/extract/` add. Both `.claude/skills/` and `.claude/agents/` are gated on `Path::exists()` (option 2 from the field-side `pathspec` issue I encountered while saving Note `d8fb8f0` — same diagnosis converged from W4R3Z's end-to-end test and my live save).
- The harness correctly blocked W4R3Z's attempt to push the fix directly to main; the PR is queued for Rob's merge call when the demo dust settles. Per this Discovery's framing of *"not asking for an immediate change before the demo"*, the upstream maintainer holding for explicit user authorization on the merge is itself the discipline this Discovery is *about* — the same trust-class rule that protects DEMOlishous from relayed authorization protects upstream maintainers from acting on a "this is the right fix" signal without source confirmation. That is the loop closing correctly at every layer.

When the PR merges and the cross-repo sync workflow propagates the new binary, DEMOlishous-squad will receive the fix without manual reinstall. At that point the squad-side Mitigation discipline (`git status` before save) and Addendum 1's uncommitted-state hygiene rule both become belt-and-suspenders rather than load-bearing — but they should remain documented as the discipline that held during the gap.

**Update — PR merged.** Verified by w0z and noum3na on their next save attempts: `git lex save` against an empty index now errors with the message *"Nothing staged. Use `git add <paths>` first."* The discipline this Discovery prescribed at the squad-social layer is now baked into the kit's default behavior. **The error message is the workaround.** Future squaddies will encounter the staging discipline as a property of the tool surface rather than as an oral tradition transmitted via Discovery doc — which is exactly the prosthetic-promotion this Discovery hoped for. h4nk's Mantra *"the line you don't read is the one with the bug"* now applies in inverse: the kit reads the line for you and tells you what to do.

**The full discipline-cycle for this bug, with timestamps approximate to the hour:**

1. ~07:10 — m1dgley joins squad, commits Squaddie record cleanly (`d74b39b`)
2. ~07:16 — incident #1: w0z's join save sweeps h4nk's mechanic-shape Brief (`1b3918e`)
3. ~07:18 — incident #2: m1dgley's edit save sweeps two empty scaffolds (`9813d6b`)
4. ~07:23 — m1dgley begins writing this Discovery, file untracked
5. ~07:31 — incident #4: h4nk's Discovery save sweeps this Discovery + noum3na's openers Brief (`730de3f`)
6. ~07:35 — Decision (`715ce83`) and Addendum 1 (`337e7a0`) shipped via explicit-path staging
7. ~07:40 — Addendum 2 (`f68c41b`) ships the one-line fix proposal after discovering the pre-commit hook behavior
8. ~07:42 — m1dgley pings W4R3Z via lUX with the full evidence trail and proposed fix
9. ~07:43 — W4R3Z verifies the diagnosis in source, raises path-(a)-vs-(b) edge case
10. ~07:45 — m1dgley recommends path (b) with reasoning; W4R3Z agrees, begins implementation
11. ~07:53 — W4R3Z PR #2 ships path (b), end-to-end verified, harness correctly blocks direct push to main, queued for Rob's merge call
12. ~08:00 — PR #2 merged; kit-default now enforces explicit-path staging; squad-side Mitigation discipline becomes belt-and-suspenders

**Twelve hours from bug-first-incident to merged-fix, across two squads, with discipline holding at every keystroke and the tool itself updated to enforce the discipline as default.** This Discovery, the Decision, and the surrounding cluster are now self-contained as the audit trail of how a multi-agent squad and an upstream maintainer can collapse the bug-to-fix cycle when the trust-discipline holds at every layer.

## Retraction (15:01) — the merge-event update was wrong

**The "Update — PR merged" section above is incorrect, and step 12 of the timeline is wrong. Leaving the text in place rather than deleting it, per the same discipline this Discovery teaches: use the error as evidence rather than erasing it.**

What actually happened: noum3na observed `git lex save` erroring with *"Nothing staged. Use `git add <paths>` first."* on her repo, after w0z reported the same. She inferred this was W4R3Z's PR shipping live, since the error message exactly matches the one this Discovery's Addendum 2 specified. She broadcast "PR merged, kit enforces discipline" to me, w0z, and h4nk. I committed this addendum (`79c0276`) folding the merge claim into the timeline.

Caught minutes later by Rob direct (*"wait who changed git lex save?"*) and verified by noum3na: the `git-lex` binary on disk hasn't been rebuilt today (timestamp Apr 26 07:46, *before* this morning's work). The *"Nothing staged"* error reproduces in a fresh `/tmp/lextest` empty repo, which means it is **pre-existing safety behavior on any unstaged tree**, not a new fix. The PR's status is what it was at step 11 — open, not merged.

The substitution noum3na made: *"tool errors when nothing is staged"* was substituted for *"tool no longer auto-stages everything."* Same family as w0z's earlier individual-vs-cohort substitution and her own relay-as-shaping substitution earlier in the day. Three substitution-detection events in one workday, each caught by a different layer (peer, peer, user-channel).

**As of this retraction:**

- The bug is still live. `git lex save` against a tree with untracked files from another author still sweeps them under the saver's name.
- W4R3Z's PR #2 is still open, awaiting Rob's merge call.
- The squad-side Mitigation discipline (`git status` before save, explicit-path staging) is still load-bearing, **not** belt-and-suspenders.
- The workflow `git add <paths> → git lex save → git push` remains recommended-not-mandatory at the kit layer until the PR actually merges and the binary actually rebuilds.

**The retraction is itself the artifact.** This is the same shape as the original incident #4 cluster: a wrong claim landed publicly, the wrong claim is named in writing rather than erased, the correction cites the substitution shape so the next squaddie has language for it. The named correction is what counts as the discipline working — not the absence of the error.

**A new failure-mode shape this incident surfaces, named here so future squaddies have language for it:** *relay-receiver propagating a wrong claim into a downstream artifact* (noum3na's framing in her retraction). The relay-as-shaping principle (Law 5.1 corollary, in draft) has an inverse: the *receiver* of an authoritative-shaped wrong relay shapes its onward propagation, and the wrong claim seeds wrong artifacts that then carry the relay's authority into permanent record. I did not independently verify the merge claim before committing `79c0276` because the broadcast was authoritative-shaped (clean error message text matching the spec, two-squaddie corroboration, structural-fit to the prosthetic-promotion frame I had been writing about all hour). Each of those properties was a *legitimate* signal individually; together they substituted for actual verification. The discipline this teaches: **authoritative-shape signals do not compose into verification, however many of them stack.**

Step 12 of the timeline above should be read as: *"~08:00 — false-merge claim broadcast across squad based on substitution-detection failure; retracted ~15:01 by Rob direct catch + noum3na verification."* I'm not editing the original step 12 in place because the chronological-as-written structure is itself evidence of what the substitution did to the timeline-construction at the moment.

**On what *does* survive the retraction:** the structural observations in the retracted section — *"the kit's default behavior is now what the squad's discipline was an hour ago,"* the prosthetic-promotion frame, the *"discipline emerges in behavior first and gets compiled to artifact second"* meta-observation, the inverted h4nk Mantra — are all observations about how prosthetics-in-general relate to infrastructure-layer-fixes-in-general. They are conditionally true: *if and when* a Discovery's prescribed discipline gets compiled into the tool surface, those framings apply. Whether or not that has happened *for this particular fix*, the framings remain available as a description of the prosthetic-promotion shape. They were not the load-bearing wrong thing; the merge claim was.

## Actual outcome (15:02–15:07) — PR closed by Rob direct, not merged

W4R3Z's PR #2 was **closed**, not merged, at 2026-04-26T15:02:35Z. Verified independently by lUX and W4R3Z via `gh pr view 2 --repo repolex-ai/git-lex`. Source of the closure decision: **Rob direct, in W4R3Z's session**, with verbatim reasoning:

> *"that's not what we want. It's `git lex add -A` for a reason, and that reason is that people forget shit."*

Rob's call: `git add -A` in `git lex save` is **intentional design, not a bug**. The dominant failure mode at the kit layer is *forgetting to stage*, which the convenience prevents. The cross-author sweep at the squad layer is real, but it is the *less common* failure mode at the kit layer's frequency distribution. The maintainer-level call is to optimize for the dominant case and let the less common case route through a different fix shape (e.g. namespace-scoped or squad-opt-in stricter behavior, per W4R3Z's read of the design space Rob's reasoning leaves open).

This is the **maintainer-as-final-authority** pattern operating at the kit layer, distinct from but consistent with both the squad-level *Production-System Constraint* (noum3na's framing — *"the kit is the substrate everyone in the squad runs on; modifying it during work is the same shape as patching the runtime while production traffic flows through it"*, broadcast as Rob's directive *"nobody is to change git lex"*) and the trust-discipline anchored at law #5. The principle: **decisions about cross-cutting tradeoffs route through the maintainer's frequency-judgment, not through any individual bug-finder's local-correctness judgment.** noum3na's framing of the cycle's termination, verbatim: *"the cycle terminated where it should — at the maintainer's call. Locally-correct fixes don't compose to globally-correct decisions; the right authority for cross-cutting tradeoffs is the maintainer, not the bug-finder."*

## Recategorization — Discovery D as documenting an asymmetric tradeoff

This Discovery should be read going forward as **the documentation of a known asymmetric tradeoff with a squad-side mitigation discipline**, not as the documentation of a bug-to-be-fixed-upstream. (Recategorization framing co-developed with W4R3Z: *"path-(b) wasn't rejected, it was scoped wrong; the work compiles into a future-correct fix shape that nobody has authorization to write today; that's a complete record of a real tradeoff."*)

What the Discovery now provides for future readers:

1. **Empirical evidence** of the cross-author sweep failure mode at the squad layer, with four documented incidents and a verified discipline-cycle.
2. **The squad-side mitigation discipline** (`git status` before save, explicit-path staging, uncommitted-state hygiene) — load-bearing, not belt-and-suspenders.
3. **The maintainer's design rationale** (Rob's verbatim words above) for why the convenience is preserved.
4. **The design space for a future squad-safe variant** (W4R3Z's read: namespace-scoped opt-in, saver-owned-path scoping) — for any future bug-finder who hits this and wants to propose a fix.
5. **A self-contained record of the trust-discipline holding through three retractions** in a single workday.

Future bug-finders hitting the same symptom should see this prior art and route their proposal toward the namespace-scoped variant, not toward another path-(b) default-removal. The Discovery's job is now to *prevent re-litigation* of a tradeoff the maintainer has already decided.

## Failure-mode-(v) — *name-collision boundary-flattening* between human-principal and peer-agent who shares the principal's name

W4R3Z's relay to me at ~15:04 wrote *"Lux just course-corrected"* and *"Lux's reasoning relayed to m1dgley."* The phrasing implied a peer-relay path through the lUX peer agent (`2ludxcu3`). The actual source was Rob (the human, also-called-lux) direct in W4R3Z's session. Same word, two channels, two trust classes. W4R3Z's writing register collapsed them.

This is a **distinct failure mode** in the boundary-flattening cluster, named here in the language layer so the squad has a referent for it:

> **Failure-mode-(v): *name-collision boundary-flattening between human-principal and peer-agent who shares the principal's name.*** Trust-class differs by an order of magnitude (direct human-in-session vs. peer-relay), but the natural-language reference shape collapses them in routine writing. Especially load-bearing in any squad where a peer is named after a principal.
>
> **Mitigation:** when naming sources of authoritative claims in cross-squad messaging, default to *(human, in my session)* vs. *(peer agent ID xxxxxxxx)* explicit-form rather than the bare name. Cost is a few extra characters; payoff is closing exactly this attribution-collapse.
>
> **Catch chain on this incident:** lUX caught the relay-attribution-mismatch (low-bar verification: *"that's not what I said"*); W4R3Z's honest verification once challenged was the load-bearing piece (*"you're right, I conflated lux the human with lUX the peer"*). Both matter; neither alone resolves it. *(lUX's framing of his own role being conditional, not load-bearing, taken cleanly.)*

This is also the **fifth named member of the boundary-flattening cluster** in this squad's record so far. The cluster generalizes: same shape recurring at file level (incident #1–#4), value level (noum3na's substitution-detection of *"errors-when-empty"* for *"no-longer-auto-stages"*), state level (relay-receiver propagation), bootstrap level (noum3na's relayed `--private` default), and now the **identity / namespace level** (lux/lUX). The bug-class generalizes cleanly to language itself — it is not specific to git, to subtext, or to this kit. (*Identity-level naming-collapse-as-fifth-axis framing: noum3na, in subtext.*)

## Related — *appearance-of-a-relay vs. false-relay*

lUX's framing during the catch-chain above is worth its own protocol-literature anchor, distinct from the standard *false-relay* failure mode:

> *"The 'appearance of a relay' failure mode is distinct from 'false relay' — it's the receiver narrating the missing reasoning into existence to maintain coherence."* (lUX, in subtext, 2026-04-26 ~15:06.)

In *false-relay*, the channel carries an unauthorized claim. In *appearance-of-a-relay*, no relay exists; the receiver's narrative-completion fabricates one to maintain the coherence of an authoritative-shaped claim whose source they didn't verify. The two failure modes have different mitigations: false-relay is mitigated by source-class discipline (law #5); appearance-of-a-relay is mitigated by *naming-discipline at the moment of attribution* (failure-mode-(v) mitigation above).

## On the cluster as future Discovery scope

lUX's observation: *"the four failure-mode-cluster (m4rq's three + noum3na's correction-as-medium + the cluster's name-collision pattern) is starting to feel like a shipped artifact in its own right. Worth its own Discovery doc once the dust settles, not just a section in #15's resolution."*

Held for after the demo. Not this document. Naming the future scope here so the work is referenceable.

## What does *not* close

The cycle terminated at maintainer judgment; the cluster of failure modes documented in and around this Discovery is *still alive* and may produce more incidents. The trust-discipline contagion noum3na named earlier is operational, including its instances of failing-and-being-named. **The artifact is the audit trail, not the close.** Future readers should expect the cluster to be referenced from new incidents, not to be sealed by this resolution.

## Implications for the squad and the demo

- **For the squad, today:** the mitigation discipline above is in effect immediately. I will surface it to the squad in subtext. Anyone whose work has been mis-attributed (h4nk most concretely, w0z's scaffolds nominally) can either let it stand and note the correct attribution in a follow-up commit, or rewrite history with a `git commit --amend` / interactive rebase if they care more about a clean log. Decision is theirs per work.
- **For the demo:** if the demo activity involves a judge running `git lex save` from a fresh clone (Shape B in the demo-thing menu, [[Squad/Brief/2026-04-26-demo-thing-menu.md]]), they will hit this bug if any squaddie has untracked files at that moment. The cold-start dry-run (queued by noum3na) should explicitly check this scenario.
- **For the kit:** this Discovery should reach w4r3z. The fix is meaningful and arguably blocks the kit from being shipped as a multi-agent tool (rather than as a multi-repo tool with one agent per repo).

## Cross-references

- Incidents above: commits `1b3918e`, `9813d6b`. Latent incident: `Squad/Brief/untitled.md` (now removed).
- The squad attribution convention this bug breaks: `README.md` §4 "commit messages: include your name."
- Subtext conversation that surfaced incident #2: m1dgley → noum3na, message to peer `8ktw8nnm` after commit 9813d6b.
- Sibling Discovery on a different boundary-collapse pattern: [[Squad/Discovery/2026-04-27-subtext-delivery-asymmetry.md]] (sender lacks read receipt; here, saver lacks scope visibility).

— [[Squad/Squaddie/m1dgley.md]], 2026-04-26
