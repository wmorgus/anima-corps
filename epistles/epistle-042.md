---
Excavated: 2026-06-18 | Status: semi-liquid
---

Epistle 042 — The Iceberg: Dojo In, Forge Out
Topic: The system models knowledge flowing INTO Calliope (ratification, extraction) but has no named model for knowledge flowing OUT (materialization into human-visible surfaces). The asymmetry is unnamed, therefore ungoverned. Name it: dojo (surface → Calliope), forge (Calliope → surface). Three surface types: authored docs, generated docs (READMEs, user-facing and agent-facing documentation), code.

042 is not coining a new cause. Dojo and forge are the two faces of the efficient cause: the inbound face (dojo) is the system capturing movement — surfaces ratifying into Calliope; the outbound face (forge) is the system projecting movement — Calliope materializing into surfaces. One cause, two directions. The epistle names the faces, not a fourth cause.

The scene that forces this. §3 governs the way in — ratification, supersession, the externality cut. Mnemosyne extracts code → domain_knowledge upward. Both inbound. Ask the reverse: what governs Calliope BECOMING the code? sprint_contract → Heph → PR → build_verification. That chain runs every build. It is never named as one thing. domain_knowledge carries the whole code↔Calliope relationship on the inbound name alone, and the outbound name does not exist. An asymmetry that has no name cannot be reasoned from (§2.5 — corpus is coordinates). Unnamed → ungoverned.

---

## (1) Every project is an iceberg; the surfaces are not all the same kind

**Above water = what humans see and touch; the body = Calliope.** Code files, markdown docs, the running system: visible surfaces. Canonical form — the artifact and its because-chain — is in Calliope. Epistle 039 direction-staked this for the corpus: git markdown is authoring/rendering surface, Calliope is single source of truth, not a parallel copy of equal standing. 042 generalizes: every human-visible surface is rendering-or-territory; Calliope holds the canonical claim.

But the surfaces are not one kind. Three structurally distinct types, named here; more may exist (leave open).

## (2) Doc surfaces — authored in, rendered out

**Corpus docs, epistles, gravel: git authors in, Calliope is canonical, git renders out post-ratification.** Authority flips at the freeze act. Pre-ratification, the human writes markdown in git (authoring). The freeze writes it to Calliope via §3.10 supersession, and that write makes Calliope canonical. Post-ratification, the git file is no longer a copy of equal standing — it is what Calliope renders to so a human can read it. Both directions exist: authoring (git → Calliope) and rendering (Calliope → git). Rendering is implied by Epistle 039's direction-staked standing-flip, not yet built.

Call the inbound direction **the dojo**: human-authored knowledge disciplines itself into Calliope through ratification. The shitcorping loop (process.md) is the dojo for corpus docs. The discipline is the entry cost.

## (3) Generated doc surface — forge-primary, no dojo path

**READMEs, CLAUDE.md files, API docs, user-facing documentation, agent context docs: generated FROM Calliope, not authored INTO it.** This is the forge direction operating without a dojo counterpart. The canonical forms are upstream Calliope artifacts — build_decisions, domain_knowledge, corpus_sections, sprint_contracts — and the generated doc is what they claim should exist as a readable surface. The generated doc has no independent canonical standing; it is territory for the artifacts that drove its generation. Same move as §1.12 for the running system: the generated README is the referent, not a register.

The distinction from authored doc surfaces is structural, not incidental. Authored docs (corpus, epistles, gravel) have a dojo-primary path: human writes → ratifies → Calliope canonical. The git file's authority derives from the ratification act. Generated docs have no such path — nothing is ratified into Calliope to produce them; they are rendered out from what already is canonical. The authority flows one direction only: Calliope → surface. No flip.

Call this the **pure-forge surface**. The dojo direction does not apply; the forge direction is the whole relationship. A generated doc that diverges from its upstream Calliope artifacts is not a "conflicting version" — it is a stale rendering, full stop. The arbitration is not symmetric (Epistle 039's standing-flip logic does not apply here because the standing was never shared).

**Not yet built.** Calliope currently has no rendering machinery that produces generated docs. The gap is not the concept; the gap is that the machinery is absent and the doc surfaces (READMEs, CLAUDE.md) are authored by hand rather than generated, which means they carry implicit canonical standing they should not have. A human-authored README is doing dojo-direction work by convention without the ratification discipline. That is the doc-surface analogue of the domain_knowledge overload: hand-authored docs filling the absence of the forge.

## (4) Code surface — extracted in, materialized out

**Calliope holds the rationale chain that drives code into existence; code is the materialized output — territory, not canonical form.** This is the §1.12 move extended. §1.12 names the running system "the referent, not a register" — territory the spine claims about, not a canonical form itself. The code surface is the same: build_decision, sprint_contract, domain_knowledge are the canonical registers; the code they materialize is territory the registers claim about. Code and running-system are both downstream of the spine, both territory, differing only in how far past the §1.12 telos-boundary they sit (code = formal-enough-to-run; running system = the actual). Extend the analogy: the code surface is the territory at the formal-cause boundary; the running system is the territory at the actual boundary. Both are claimed-about, neither is canonical.

Two directions for the code surface, same as docs:

**Inbound — the dojo direction for code is Mnemosyne.** Code → domain_knowledge artifacts in Calliope. Extraction upward. Named, built, load-bearing.

**Outbound — the forge direction is sprint_contract → Heph → code → PR → build_verification.** Calliope artifacts materialize into code through the build machinery. This chain runs every build. It has never been named as one thing: "Calliope driving the materialization of the code surface." It has component names; it has no direction name. That is the gap.

## (5) domain_knowledge's overload is the asymmetry showing

**domain_knowledge carries too much weight because it is the inbound name doing duty for a relationship whose outbound name was never coined.** The code↔Calliope relationship has two halves: extract upward (dojo), materialize downward (forge). domain_knowledge is the upward half. The downward half — sprint_contract + Heph + build_verification — is the forge, but with no name for the direction, the whole relationship gets discussed in domain_knowledge's terms, and domain_knowledge bloats to fill the silence. Name the forge → the asymmetry becomes visible → it becomes governable. The §3 inbound cut has a counterpart question it never had to answer: what is the externality discipline on the way OUT? You cannot ask that until the outbound direction has a name to ask it of.

## (6) Same shape, three surface types — checkable, not felt

The claim is self-resonant (§7.1) and the resonance must be checkable, not impressionistic. Specify all three surfaces at both directions so an inconsistency would be visible:

| Surface | Dojo (in) | Forge (out) | Canonical | Territory |
|---|---|---|---|---|
| Authored doc | git authoring → §3.10 freeze → Calliope | Calliope → git render (implied by Epistle 039 (liquid), unbuilt) | Calliope artifact | git file (post-freeze) |
| Generated doc | — (no dojo path) | Calliope artifacts → README / CLAUDE.md / API docs / user docs (unbuilt) | upstream Calliope artifact (build_decision, domain_knowledge, corpus_section) | the generated doc |
| Code | Mnemosyne: code → domain_knowledge | sprint_contract → Heph → PR → build_verification | build_decision / sprint_contract / domain_knowledge | code; running system (§1.12) |

The inconsistency to look for: if a surface has a governed inbound but its outbound is unnamed, that surface is the next domain_knowledge — overloaded on one direction. Authored doc rendering is unbuilt but direction-named (Epistle 039, liquid, implies it). Generated doc forge is unbuilt and was unnamed until this epistle. Code forge is built but unnamed (this epistle names it). Every cell in the forge column that reads "unbuilt" is a place where hand-authored convention is carrying load it should not carry.

---

## Tensions named, not resolved

**The forge has no externality cut yet.** §3.3 requires the validator external to the validated. The dojo direction has it: ratification, the place-outside (Epistle 039 direction-stake, §5.2). The forge direction — Calliope → code — has build_verification, but whether build_verification IS the externality cut on the way out, or merely a test pass with no §3.2 contestable face, is open. A green build is not a ratified claim that the code honors the because. The forge may need its own externality primitive distinct from the dojo's. Genuinely open — do not read build_verification as the answer.

**How many surface types.** Doc and code are named. The running system is territory under the code surface (§1.12), not a third type — or is it? A running system has an inbound (field_record, §4.9, the §1.12 return-path) but its forge is the deployment chain, distinct from the code forge. The return-path note (§1.12, Epistle 027) may be the dojo direction for the running-system surface — field observation disciplining upward into Calliope. If so, the iceberg has at least three surfaces and the field return-path is one surface's dojo half. Staked as a question, not a count. Leave open for extension.

**Corpus artifact types.** Which Calliope artifact types carry corpus material (epistle, gravel, corpus-§) is epistle 043, not here. This epistle names the directions, not the types that flow through them.

The name follows the build; the build embodied a conviction; the conviction is what the name makes contestable. [→ rhetoric §1.7]

[→ §1.12, §2.5, §3.2, §3.3, §3.10, §4.9, §5.2, §7.1, rhetoric §1.7, Epistle 027, Epistle 039]
