---
Excavated: 2026-06-08 | Status: liquid
---

Epistle 032 — Substrate.md + Process.md: The Material and Efficient Cause Docs
Topic: The corpus docs already instantiate the four-cause structure (Epistle 028) — but partially. Two of the four causes have no doc: material and efficient. Build both in one pass. substrate.md = what the system is made of; §6 agents and Bench (031) migrate in. process.md = what produces change in the system; the epistle/shitcorp/version machinery, now living in CLAUDE.md as project instructions, migrates in. Telos.md's bridge list names the gap by what it omits. Both moves are migrations, not supersessions — claims and conventions keep their content, change their file. Same shape at the doc-architecture scale (§7.1 receipt).

**claim.** The corpus documents are already organized by the four causes they name (Epistle 028) — but two of the four-cause docs were never built. Build them in one pass: `corpora/anima/substrate.md` (material cause) and `corpora/anima/process.md` (efficient cause). The §6 agent block migrates into substrate. The epistle-lifecycle and shitcorping machinery — currently configuration text in CLAUDE.md — migrates into process. The docs instantiate, at the scale of the corpus's own files, the partition Epistle 028 stakes for software artifacts and §13.6 stakes for architecture. The form of the docs becomes the claim of the docs — and only with all four built is the form complete.

**the four causes already organize the existing docs — minus two.** Map what exists onto Epistle 028's partition:
- **telos.md = final cause.** The zeroth-class doc (telos.md, opening). The why, the ruling-outs, the value ordering. Not a peer in the partition — the condition the other docs require to mean anything (Epistle 028: telos-primacy; §13.6). Already built, named off-the-scale.
- **logic.md = formal cause.** The conviction corpus — the architectural §-claims, the pattern that makes Anima THIS system. "The pattern that makes this system THIS system" is Epistle 028's formal-cause definition verbatim. logic.md is formal-cause territory and always was.
- **rhetoric.md = the doxa register.** The same commitments meeting conversation (telos.md bridge). Argument shapes, decoration — adjacent to the partition, not inside M/E/F. Not a fourth cause; a presentation register.
- **corpus_vocab.md = definitional substrate.** The other corpora cite it for term-meaning (telos.md bridge). Definitional ground, cited-from. Sits under all four.

Two of the four causes have no doc. **Material cause** — what the system is made of — has none. **Efficient cause** — what produces change in the system, what moves it from one state to the next — has none either. The gaps are not hidden: telos.md's derivation bridges enumerate logic.md, rhetoric.md, corpus_vocab.md, ur-software — and stop. No substrate bridge. No process bridge. The bridge list is a map with two coordinates blank.

---

**Doc one: substrate.md — the material cause.**

**§6 agents are material-cause content living in a formal-cause doc.** logic.md §6 (agent topology) is the misfile. logic.md is the conviction corpus — what the system IS and rules out (formal cause). Agents are what the system is *made of* (material cause, Epistle 028: "the substrate — what the system is actually made of"). §6.12–§6.19 (Hermes, Mnemosyne, Pavel, Daedalus, Argus, Janus) are entries in an inventory of constituents, not architectural convictions. They belong where the inventory lives. This is why the agents section reads heavy and mixed — not because the claims are wrong (they are not), but because their *home* is wrong.

**substrate.md contents** — what the system is made of:
- **agent definitions** — the §6 agent block (§6.12–§6.19 and the agent-specific entries: telescoping occupancy, Hephaestus scope, non-slots). Migrated, not rewritten.
- **Bench** (Epistle 031) — the host, the VS Code fork the whole loop runs in. Lands here once ratified. Bench is the most material of materials: the concrete substrate (031: "the concrete place to run them"). Term collision held, not resolved: Bench is *host* (where humans and constellation co-locate, 031); Calliope is the *artifact store* (§4). Both "substrate" in different registers — Bench the runtime substrate, Calliope the commitment substrate. substrate.md houses Bench's definition and points to §4 for Calliope, which stays in logic.md as a formal-cause architectural claim. Flag: whether §4 (Calliope) is itself material-cause and should migrate too is open below.
- **constellation structure** — the topology-as-liquid-artifact framing (§6.4), the made-of-agents shape.

Doc format mirrors the four-cause pattern. Each agent entry answers the same five questions, made explicit as a template: **domain owned** · **harm-when-failed + harm-bearer** (the §6.1 license) · **name import** (§6.8) · **occupant** (resolved / candidate / open) · **rules out**. The entries already carry this shape implicitly; substrate.md makes it the doc's spine.

---

**Doc two: process.md — the efficient cause.**

**the lifecycle machinery is efficient-cause content living in project configuration.** What moves an epistle from vapor to frozen? What produces a gravel record? What triggers a version bump? This is the efficient cause — what produces change in the system (Epistle 028: efficient cause is the process that brings the artifact about, the change-maker). That content exists. It is conviction-grade. But it lives in CLAUDE.md as project instructions — a configuration file, sitting outside the corpus, reasoned-about-by-the-harness rather than reasoned-from-by-agents. The misfile is one register deeper than §6's: §6 is in the wrong corpus doc; the process machinery is in no corpus doc at all. It is corpus material wearing config clothes.

**process.md contents** — what produces change in the system:
- **the epistle format and status lifecycle** — vapor → liquid → semi-liquid → frozen. The states an epistle moves through and what each transition requires. The lifecycle IS the efficient cause made explicit: the named state-machine that turns conversation into frozen claim.
- **the shitcorping loop** — lite proposes → author responds → builder commits. The three-step forging process, the engine that produces gold and gravel.
- **the two distinct loops** — the drafting/revision loop (author + agents iterating on frame and claims, *no gravel written*) vs. the shitcorping-for-ingestion loop (lite pans against live corpora, *gravel written after agreement, builder commits*). This distinction is load-bearing and easy to lose: it names *when* the change-producing machinery actually fires. The drafting loop changes the epistle; only the ingestion loop changes the corpus. Conflating them mis-records what produced what.
- **the two workflows** — write an epistle (builder) / shitcorp an epistle (lite proposes, builder commits). Who does what to move the system.
- **VERSION semver convention** — patch (correction/clarification to a frozen artifact) / minor (ratification event: liquid → frozen, new claim lands) / major (foundational supersession: a frozen §-claim superseded, rules-out changes). The ratification-event convention (update VERSION, git tag `v<version>`), the tag discipline, the anima-core `CORPS_VERSION` fidelity pin. Versioning is the efficient cause's bookkeeping — the record of *what change happened and when*, the dated receipt of every state transition.
- **gravel format conventions** — the shitcorpus record structure (gold + because, gravel + because, tensions, smelter's contribution, verdict). The output the change-machinery emits.

**the distinction from logic.md — why not minus three.** logic.md §3 stakes the *conviction* that ratification must happen and why: that liquidity-then-freezing is the governance Anima requires, what it rules out, the philosophical warrant. process.md describes *how to run it* — the operative how, the steps, the state names, the tag commands. Same relation that runs telos.md (why this system exists) → logic.md (what shape it must have) → process.md (how it moves through its states). §3 is the conviction that the engine must exist; process.md is the engine's operating manual. The two do not duplicate; they sit at adjacent altitudes. process.md cites §3 as its warrant and does not re-argue it.

---

**CLAUDE.md stays — as configuration, not corpus.** CLAUDE.md keeps what is genuinely harness-configuration: git conventions, directory structure, agent-file locations, permission modes, the operational scaffolding the harness reads to run. The *intellectual and process content* — the lifecycle, the loops, the versioning convictions — graduates into process.md. CLAUDE.md then references process.md rather than duplicating it: a pointer from config to corpus, not a second copy. This separates the two registers cleanly: config tells the harness how to behave; process.md tells agents how the system changes. The same content cannot be authoritative in two files; the corpus is the authority, config defers to it.

---

**migration, not supersession — the load-bearing distinction, applied to both.** Neither move changes content. substrate: §6.1's harm-distinctness, §6.12's Hermes domain, §6.18's Argus license — same content, same rules-out, same cross-references; only the *file* changes. process: the lifecycle states, the loop steps, the semver definitions — same conventions, relocated from config into corpus; nothing redefined. Neither is §3.10 supersession: supersession negates a predecessor and elevates a successor with the *because* on record (telos.md ruling-out 6; §13.7). Nothing is negated. No claim is replaced. A migration changes *where claims live*; a supersession changes *what they say or rule out*. The versioning convention (§17, CLAUDE.md semver) is built for the latter and silent on the former. Stake the distinction once, for both moves, so neither is mis-recorded as a ratification event.

**VERSION implication — patch, not minor, for both.** A minor bump is a ratification event: an epistle freezes a new claim. No new claim freezes in either move. A major supersedes a frozen §-claim, changing rules-out. Nothing's rules-out changes. Both moves are clarification/correction to the arrangement of existing artifacts — the patch definition. Probably patch, ×2 (or one patch covering both, if committed together). Flag: the convention does not name "doc reorganization" or "config-to-corpus migration" as a version event class at all — see open tension. The bridge-list amendments to telos.md (below) are additive, not supersessions of telos.md's frozen content; they do not lift the floor.

---

**telos.md derivation bridges gain two entries.** Once both docs exist, telos.md's bridge list adds:
`→ corpora/anima/substrate.md — the material register; what the system is made of (agents, host, constellation).`
`→ corpora/anima/process.md — the efficient register; what produces change in the system (lifecycle, shitcorping loop, versioning).`
Both additive. The bridge list is already explicitly open — it carries a "Planned: → composition.md" line (§1.16). Adding bridges to docs that now exist is the same move, completed rather than planned. A small telos.md amendment, not a rewrite. The two new bridges close the two blank coordinates the omission named.

**logic.md becomes the doc it was always meant to be.** With §6 migrated out, logic.md is the conviction/architecture corpus, clean:
- §1–§5 — ratification architecture (ontology, liquidity, governance, Calliope-as-store, topology principle).
- §7–§9 — self-resonance, diagnostic posture, inferential UI.
- §10–§13 — power/ethics, the information poet, adjacent work, the epistemic frame and causal structure.
- §14 — the bet surface.
- §15–§16 — open tensions, known gaps.

The agent *implementation inventory* is gone; the agent *topology principles* (§6.0–§6.11 — slot-license logic, harm-distinctness, thin-agent, concept-ownership) are the genuinely open question below. logic.md becomes formal cause throughout: what the system IS, not what it's made of and not how it moves.

**§7.1 self-resonance — the receipt, now complete.** §7.1: the same shape recurs at every scale — artifact, agent, pipeline, the paper itself. Add a scale: **the doc architecture.** With substrate.md and process.md built, the corpus instantiates *all four causes* it names as the structure of software artifacts (Epistle 028) and of architecture (§13.6): **telos.md = final, logic.md = formal, substrate.md = material, process.md = efficient.** The form of the docs is now the full claim of the docs — not three causes and two gaps, but the complete partition, filed. This is §7.2's checkable evidence the abstraction is at the joints — an abstraction wrong at the joints could not replicate cleanly down to the filing of its own corpus, and could not have *forced* the two missing docs by the gaps it left. Not designed-in; surfaced by following the partition to the docs that hold it. Same shape three scales: §13.6 architecture, Epistle 028 artifact, this doc-architecture. The receipt is that building both docs was forced by the partition, not chosen for tidiness — the two gaps announced themselves through telos.md's two blank bridges.

---

**open tensions.**

- **VERSION semantics for a migration event — genuinely open, now ×2.** The semver convention (patch/minor/major) is defined over *frozen-artifact content*: patch corrects, minor ratifies, major supersedes. A doc reorganization that moves frozen claims between files (substrate) — and a config-to-corpus migration that promotes process conventions into the corpus proper (process) — fit none cleanly. Patch is the closest read for both (clarification, no claim changed) but "clarification to an artifact" is not obviously "move an artifact to a new file" or "promote config text into corpus." The convention has no event class for re-filing. The process migration sharpens the question: it is not even moving *between corpus files* — it is moving *into* the corpus from outside it. Is promoting config-grade text to corpus-grade a ratification (the content was never a frozen §-claim before) or a re-filing (the content was already authoritative, just mis-homed)? Don't know yet. Flag: resolve whether migration needs its own version semantics or folds into patch *before* committing, so the version record is honest about what happened — and whether the two moves take one patch or two.

- **which §-sections beyond §6 belong in substrate.md.** §6a (agent context architecture — the four tiers an agent reasons from) is a candidate: about what agents *run in* and *reason from at init*, arguably made-of content. But §6a is half about *contradictions* (§6a.5–§6a.8) and named *silences* (§6a.9–§6a.10) — formal-cause/open-tension content, belonging with logic.md §15–§16. §6a may split: tier *definitions* (§6a.1–§6a.4) to substrate.md, *contradictions and silences* staying in logic.md. And §4 (Calliope) — the commitment substrate — is itself material-cause by Epistle 028's reading. Whether Calliope migrates too, or stays in logic.md because it is an architectural *principle* (one append-only store, single API, §4.1) more than an inventory, is the same host-vs-system tension 031 holds, one level up. Named, not resolved.

- **the boundary between process.md and the §3 governance conviction.** process.md describes how ratification runs; §3 stakes that it must. The line is clean in principle (how vs. why) but porous in practice: a state-name (semi-liquid) carries a conviction (that corpus changes are drafted-but-not-yet-committed as a distinct, nameable state). Is naming that state a process detail or a governance claim? The lifecycle *is* partly conviction — the choice to have four states rather than two is an architectural commitment, not a mere operating procedure. Flag: some lifecycle content may be §3-grade conviction that should stay (or be cited) in logic.md, with process.md holding only the operative mechanics. Decide the cut before migrating, or process.md inherits conviction it should only cite.

- **the composition.md gap, now with a third possible home.** telos.md (§1.16) names composition.md as planned, unbuilt. The refactor surfaces a placement question: is compositionality a conviction claim (how artifacts *must* compose — formal, logic.md), a description of the composed substrate (what the composition *is made of* — material, substrate.md), or a description of *how* composition is performed/checked (the orphan-check process — efficient, process.md)? Building both docs gives composition.md *three* candidate homes where it had one. The four-cause map does not pre-decide it. Flag: decide which cause composition serves before building it, or it inherits the same misfile §6 and the lifecycle machinery just escaped.

[→ §1.12, §1.16, §3.10, §4.1, §6.0, §6.1, §6.4, §6.5, §6.8, §6.12, §6.18, §6.19, §6a.1, §7.1, §7.2, §13.6, §13.7, §17, Epistle 026, Epistle 028, Epistle 031]
