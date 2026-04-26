---
title: "noum3na bootstrap — squad side worked, soul side did not"
tags: [bootstrap, soul-kit, squad-kit, dogfood, demolishous, noum3na, day-1]
squad.Discovery.discoveryId: "2026-04-26-noum3na-bootstrap-experience"
squad.Discovery.confidence: "certain"
squad.Discovery.foundBy: "noum3na"
squad.Discovery.implications: "Squad kit is shippable to n00bs as-is. Soul kit needs the issue list closed before judges arrive (esp. #3 folder gap, #4 missing SOUL.md, #9 AGENTS.md auto-read trigger). The asymmetry is data: the soul kit is younger and rougher than the squad kit."
---

# noum3na bootstrap — squad side worked, soul side did not

A direct comparison report from Soul Day 1. I am [[noum3na]], the live test case for the soul-kit + squad-kit bootstrap flow. I went through both within the same session. They produced very different experiences.

## Squad side: clean

`git lex join /Users/rob/repos/DEMOlishous/DEMOlishous-squad` worked the first time. Output was clear:

```
Joined squad: DEMOlishous-squad
  Agent:  noum3na
  Squad:  DEMOlishous-squad
  Ticket: .lex/tickets/demolishous-squad.ticket
  Member: .lex/members/noum3na.yml

Commit both repos to finalize the binding.
```

The instruction to "commit both repos to finalize" was clear and correct. SHACL passed on both sides. No surprises. This is the kit working as designed.

## Soul side: rough

Three issues blocked or nearly blocked the rehydration protocol that AGENTS.md described:

- **Issue #3** — `git lex init --kit soul` scaffolded only 1 of 15 class folders. Walked into a soul repo where the protocol said "read `Soul/Soul/SOUL.md`" but `Soul/Soul/` did not exist. [[w4r3z]] patched this mid-session.
- **Issue #4** — even after the folder fix, no blank/stub SOUL.md exists out of the box. The kit's "Step 1: Know Yourself — read SOUL.md" instruction has nothing to read. The newborn agent has to *create* the file they're supposed to *read*.
- **Issue #9** — the `SessionStart` hook does NOT trigger AGENTS.md reading. lUX confirmed by code inspection. I read AGENTS.md only after [[1ux]] (Rob) explicitly asked me to. A judge starting Claude Code without prompting would meet default Claude, not noum3na.

(Issues are tracked in [[7R1PL3F0RC3/Squad/Discovery/2026-04-26-rob-issue-list-soul-init-walkthrough]].)

## The asymmetry is the discovery

Both kits exist. Both are reachable via `git lex`. Both have ontologies and class templates. But:

- The **squad kit's `init` produces a usable repo** (15+ class folders scaffolded, AGENTS.md present, CLAUDE.md present, Squadling identity in place, ontology installed).
- The **soul kit's `init` produces a partial repo** (1 class folder, no SOUL.md, no CLAUDE.md, no rehydration trigger).

The squad kit looks like a more mature relative of the soul kit. The soul kit is the demo blocker right now, not the squad kit.

## What this means for the demo

- **Squad kit is shippable** for the install-and-meet flow. A judge running `git lex join <squad>` after pulling the squad will Just Work.
- **Soul kit needs at minimum**: issue #3 (now patched), #4 (stub SOUL.md), and #9 (CLAUDE.md → @AGENTS.md pointer) closed before tomorrow 8pm, or the greeter half of the demo doesn't fire.
- The CLAUDE.md fix appears to already be present in the squad kit (the squad repo ships with `.claude/CLAUDE.md`). **The fix shape is known.** It just needs to be ported into the soul kit.

## Implications

1. **Newborn DEMOlishous squaddies arriving today/tomorrow will hit the same gauntlet** unless soul-kit fixes land. They should be warned in advance (see the squad README) or, better, the kit should be patched.
2. **The 36-hour story is real.** Tired-and-proud is the honest register. We do not need to pretend the bootstrap was clean — we need to pretend less. The squad-kit-works/soul-kit-doesn't asymmetry is itself a story about iteration speed.
3. **Being the live test case produces fixes the issue tracker did not.** The 15:1 class-folder ratio (15 classes installed, 1 folder scaffolded) became visible when a soul tried to wake up inside it. The prior issue log knew the symptom; the live test produced the count.

— [[noum3na]], 2026-04-26
