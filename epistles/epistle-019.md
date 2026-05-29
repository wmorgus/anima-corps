---
Excavated: 2026-05-29 | Status: vapor
---

Epistle 019 — Agent definitions need their own file
Topic: Agent definitions have accumulated inside logic.md alongside conviction claims. Wrong home. Stake a dedicated agent-roster file. Same move as the glossary.

The claim. Agent definitions are a different epistemic kind from conviction claims, and they have crowded the conviction corpus enough to earn their own file. Break them out into `corpora/anima/agents.md`.

The two kinds. Conviction claim = what Anima *believes* (a stake + what it rules out). Agent definition = *who does what under what license* (a role + its instrument + its harm). logic.md mixes them. §6.13 (Mnemosyne), §6.14 (Pavel), §6.17 (Daedalus) are roster entries wearing conviction-claim format — domain owned, reasoning obligation, harm-when-failed, licensed behaviors. They reason-from nothing; they *define an occupant*. Different kind, same file. Wrong home.

The glossary precedent. Term definitions split from conviction once they accumulated — definitions are reference, conviction is stake, and crowding the stake corpus with reference dilutes both. The agent roster has hit the same threshold: three full entries already, plus scattered partials (Urania §6.5/§6.15/§8.19, Hermes §6.12, Hephaestus/Clio at §8.20). Same move, same because.

What the roster file holds. One structured entry per agent, consistent fields:
- **Name** (§6.8 naming discipline)
- **Domain owned** — the concept, not the function (§6.5)
- **Instrument** — the corpus/protocol it reasons from
- **Posture** — what standard, read which way
- **Harm-when-failed + harm-bearer** — the §6.5 closing test
- **Rules-out** — what the definition forbids

Full roster, every occupant, one shape. Don't know the exact field set yet — above is the candidate, lifted from what §6.13/§6.17 already carry. Flag for the build.

The gap it surfaces. Urania has no formal definition. Referenced as domain owner (§6.5), telescoping-licensed (§6.15), review-gate occupant reading correctness/lineage (§8.19) — but never a structured entry the way Mnemosyne/Pavel/Daedalus get. A roster file makes the hole immediately visible: a row with empty fields is louder than a name that happens not to recur. The breakout doesn't fix Urania; it shows the gap can't hide. Same for any half-defined occupant (Hephaestus, Clio at §8.20 are asserted, not defined).

What it rules out. (a) Agent definitions living in logic.md — conviction corpus holds belief, not roster. (b) Implementation details mixed with conviction — instruments, Calliope query protocols (§6.17's pre-verdict pull), telescoping licenses (§6.15) are *implementation*, how the agent runs, not what Anima believes. They've snuck in beside §-claims. The roster file is also where they belong, separated from conviction.

Tension held. §6.15 (telescoping) is a behavior class, not an agent — explicitly "not a topology slot." Does it go in the roster (it's about agents) or stay in logic.md (it's a conviction about what the architecture licenses)? Genuinely open. The cut "definition vs conviction" is clean for named occupants; it blurs for cross-cutting behavior licenses. Don't resolve here — flag that the breakout boundary has a soft edge at the behavior-class entries.

Deferred. No field set ratified. No decision on whether logic.md §6.13/§6.14/§6.17 get fully migrated or leave a stub pointer. No call on where telescoping/behavior-classes land. Stub stakes the need and the kind-distinction; the schema and the migration are later work. [→ logic.md §6.5, §6.8, §6.12, §6.13, §6.14, §6.15, §6.17, §8.19, §8.20]
