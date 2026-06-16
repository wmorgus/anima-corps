# One Home — Transition Working Note

**Status:** working note, not corpus. Not frozen reference, not an epistle, not gravel. A session handoff capturing the conversation that produced epistles 038 and 039 and the sequencing plan for the unification they argue for.

**Branch:** `claude/tender-maxwell-gnrzfr` (anima-corps). Epistles 038 and 039 and the 038 gravel record are committed and pushed here.

**Pick-up context:** this thread ran in an environment with only anima-corps in reach. The next phase needs anima-core too. Resume where you can touch both repos plus the running Calliope.

---

## Naming and project structure (as of 2026-06-16)

Four projects, in dependency order:

- **Anima** — the upstream system. The logic corpora, telos, rhetoric, process — the reason the other projects exist. Its telos is the corpus itself: `corpora/anima/telos.md` is the authority. Anima is not a piece of software; it is what the software implements.
- **Calliope** — the governed artifact store. Its own project with its own telos: be the externality primitive that makes §3.3 real — append-only, typed-edge, schema-validated single source of truth that any Anima-conformant system builds on. Both aZero and Bench are clients of Calliope; neither owns it. This is why it is its own project: no single downstream owns the substrate.
- **aZero** — faithful CLI implementation of Anima. Its telos: put §4 discipline behind one wall (the seam), make triggering a live reasoning act, let any host invoke Anima by shelling it. Library + daemon shape (038). Possible §6.8 name-import: zeroth-class / ground invocation layer — confirm if intentional.
- **Bench** — the useful UI for working with Anima through aZero. Its telos: be the rich human-facing interface — the VS Code fork where human and Anima work together.

Previously named anima-core becomes the aZero + Calliope split. Collision resolved: Bench stays Bench (the rich host); aZero is the CLI it invokes; CC is the *model* aZero is built in the image of, never Bench itself. This resolves 039's open Bench/CC tension.

---

## Where we are

Two liquid epistles were drafted and (038) shitcorped in this session:

- **Epistle 038 — The CLI Seam.** Claude Code's architecture is the correct model for anima's invocation/orchestration layer (host invokes a capable CLI, triggering stays a live reasoning act), and anima-core is mis-shaped as a Python server that owns its HTTP surface — correct shape is library + daemon whose hosts own the surface. The CLI seam (`anima` shelled by any caller) is the externality primitive at the invocation boundary: whatever calls it meets §4 discipline behind one wall. It also gives §6a.10's [OPEN] pull-vs-push silence a concrete body (context pulled via `anima` query, not pushed by file). Shitcorped, verdict **liquid**, gravel record written. Both proposed tensions dissolved on review (see gravel/epistle-038.md). Not frozen — a liquid verdict is not a ratification.

- **Epistle 039 — One Home: Single Source of Truth, Not Single Repo.** The corpus↔build split across two git repos (anima-corps = dojo/reasoning; anima-core = build) has no governed pipeline either way, and that is the §7.4 self-resonance failure made concrete: Anima sells a dojo→build pipeline it does not run on its own development. The unification target is **single source of truth (Calliope), not single repo**. **Shitcorped** (lite, on Sonnet); verdict **liquid**; held at **semi-liquid** deliberately (see "the bind" — not frozen under the old step). Three gold (single-source-of-truth; freeze-must-write-to-Calliope; §7.4 dev-layer self-resonance), one gravel (the Bench citation in claim 3 — §7.4 carries it, Bench was a scope stretch), three tensions held open (the three below). See gravel/epistle-039.md.

Both are the same move at different layers (039 §3): put §4 discipline / the frozen reference behind one wall, callers meet it as externality. 038 is the move at the invocation layer; 039 is the move at the development layer (Anima-developing-Anima).

---

## The core realization

The corpus/build split is on borrowed time. It was intentional and structural — two self-contained, tractable surfaces — but the doing reveals the cost:

- Gold from corpus work keeps resolving into build notes.
- Build amendments keep warranting corpus changes.
- Neither crossing has a governed pipeline; the crossing is a git-repo boundary, high friction.

The generative scene: running the 038 shitcorping moved the git corpus. The corpus **also already lives in anima-core's Calliope** (that migration is complete — it closed, or is the live instance of, §6a.6: frozen corpora invisible to runtime agents). So right now the Calliope corpus is **stale** relative to the git corpus. Two copies of one frozen reference, drifting. That drift is the claim.

The deeper point: "one git repo" is the surface answer. The real answer is **single source of truth** — the corpus lives in Calliope; the git markdown becomes an authoring/rendering surface that ratifies INTO Calliope, not a parallel copy of equal standing. The home is the store, not the directory.

---

## The bind that dictates sequence

**You cannot cleanly freeze 038/039 under the current freeze step — because the current freeze step is exactly what 039 condemns.**

Freeze today = update VERSION + git tag + edit corpus markdown, with the Calliope write as a *separate manual migration*. That gap is where drift enters. So ratifying 038/039 the old way reproduces the problem they diagnose.

This is not a blocker — it is the tell for the right ordering: **the transition is the first use of the fixed freeze step, not the last use of the broken one.** Same shape as Epistle 032 (the migration event was itself the structural reshape). 038/039 freeze *into* the new world, as its inaugural acts.

Therefore: hold 038/039 at liquid (or shitcorp-to-agreement and hold at semi-liquid) deliberately. Do not freeze them under the old step.

**Nuclear rebuild dissolves the bind.** The bind was a migration concern — how do you use a broken process to ratify the fix for that process? A rebuild from scratch has no prior path to be dependent on. Build Calliope correctly first; build aZero against it; build Bench against that. The sequencing concern only applies to incremental migration; the ceremony can be dropped.

---

## The plan

**Lowest-regret first build move:** claim 2 of 039 — make ratification propagate to Calliope atomically. Right regardless of how the open tensions resolve. Does not require deciding CC-plugin-vs-not, merging repos, or settling CORPS_VERSION. It closes the loop where it currently leaks and establishes Calliope as the de-facto single source of truth before any topology decision.

Phasing:

- **Phase 0 (now):** 038/039 stay liquid. Keep the transition staked as a coherent unit.
- **Phase 1 (anima-core):** build freeze→Calliope propagation. Calliope becomes the source of truth in practice. Lowest regret.
- **Phase 2:** ratify 038/039 *using* the new freeze step — they freeze themselves into the new home. Self-resonant.
- **Phase 3:** the downstream tensions each become their own epistle, ratified in the new home, surfaced by build pressure (§5.6) rather than speculated ahead of it.

**Recommended immediate next step:** shitcorp 039 to agreement, hold it semi-liquid, then move to anima-core for Phase 1. Reasoning: stake the spine, don't over-stake. The downstream epistles (esp. CC-plugin mechanics) will be better reasoned in the new home where the actual shape is visible — 039's own §5.6 logic.

---

## Running the rebuild as a governed pipeline (the bootstrap line)

The rebuild is to be done *by following the process we staked here* — not as a developer rewriting anima-core, but as Anima's first real run of its own dojo→build pipeline on itself (the §7.4 receipt). Hard rule: **stake before building.** Every rebuild move is an epistle first — staked, shitcorped, ratified — with one honest exception: the bootstrap.

**The bootstrap paradox.** 039 says ratification must propagate to Calliope (the fixed freeze step). But *building that propagation is Phase 1* — you cannot ratify-through-the-new-step the building of the new step, because it does not exist yet. There is an irreducible bootstrap: the freeze→Calliope mechanism must be hand-built under the *old* process (git, markdown, human review) before it can govern anything. You cannot dogfood your way to the first bite.

The discipline that falls out:

1. **Minimize the bootstrap.** Phase 1 = *only* freeze→Calliope propagation. Nothing else rides in it. Everything built in the bootstrap is ungoverned-by-the-new-process, so the smallest bootstrap is the least ungoverned surface. (The lowest-regret first move and the minimal bootstrap are the same thing — 039 claim 2.)
2. **The bootstrap line is explicit.** Name the exact point where governance-through-Calliope begins: *the moment freeze→Calliope works.* Before it — old process, all work held liquid. After it — every freeze writes to Calliope, no exceptions.
3. **Phase 2 is the inaugural governed act, and it is self-justifying.** Ratify 038/039 (and the bootstrap epistle) *through* the new step; their freezing IS the proof the step works. Clean against the lifecycle: building against liquid epistles, then freezing them once the mechanism exists, is normal liquid→frozen, not a retroactive write — §4.2/§3.3 stay satisfied (no edit-in-place, just the lifecycle advancing).
4. **Phase 3+ fully dogfoods.** Server-shedding, the CLI seam, the plugin, the model-policy layer (040) — each staked, shitcorped, ratified into Calliope. This is where the rebuild becomes the pipeline's first customer.

**Why holding 038/039/040 liquid now is already correct.** Committing them to corpora today would use the broken freeze step (markdown edit + manual migration = drift) — the exact thing being rebuilt. Holding them as a working note rather than corpus is not hesitation; it is the staked process being honored before the mechanism that would let them freeze cleanly exists. The transition doc being a note, not corpus, is the process working.

---

## Open tensions (carried from 039, not resolved)

1. **Multi-device reachability → anima-core CLI as a Claude Code plugin.** Reaching CC from personal laptop / phone / work laptop is host-provided (CC runs in the cloud, reachable anywhere). Anima should inherit that flexibility. Building it into anima-core would be the `server` role 038 said to shed (§1.5); riding CC-as-host gets it free → points toward anima-core CLI distributed as a Claude Code plugin, running wherever CC runs, with Calliope as the persistent networked substrate any session reaches. Resurfaces 038's gold-9 multi-host `asserted_by` (§4.7 / Epistle 031): multiple devices/hosts, one Calliope, provenance must distinguish them. The multi-device story IS the multi-host story. **Open:** plugin-delivery mechanics; whether Bench (VS Code fork, rich workstation host) and CC-web/mobile (lightweight host) are two faces on one Hermes front door (§16.3) or strain "one extension because one front door."

2. **Discipline-boundary cost of unification.** The two-repo split crudely enforced two disciplines (corpus → shitcorp/ratify; code → normal dev). Collapse risks corpus markdown treated as just-more-source, edited in place — the §6a.8 mutable-frozen-artifact failure. **Resolution direction:** discipline lives in Calliope + the ratification process (append-only §4.2, supersession the only mutation §3.10), not the repo boundary. A real cost to handle, not wave away. Self-contained tractability was a genuine benefit — recoverable via session/worktree isolation, but name the cost.

3. **CORPS_VERSION's fate.** CORPS_VERSION (core pins which corpus version it is faithful to) exists because of the split — it is the bridge across the repo boundary. The stale Calliope corpus is CORPS_VERSION showing its limit: a pin *detects* a delta, it does not *prevent* drift. Under single source of truth there is no second copy → no pin to go stale. **Open:** does CORPS_VERSION dissolve, or transform into a "ratified-against" marker (which supersession-state core was built against) that survives inside one home?

---

## Verification flags for whoever resumes

- **§6a.6 status — CONFIRMED FORMALLY OPEN (lite verified).** logic.md §6a.6 (~line 374) still reads "Contradiction 2 — Frozen corpora invisible to runtime agents... corpus_logic.md exists in docs/papers/ and is not retrievable by any runtime agent." No [CLOSED] marker, no amendment. The Calliope migration happened in anima-core (runtime) but the git corpus here still shows §6a.6 open — **the git corpus and the Calliope state disagree about whether §6a.6 is even closed, and that disagreement is itself a live instance of the drift 039 names, sitting inside the very section it cites.** This *strengthens* 039 claim 1: the drift is not "the §6a.6 failure one level up" (healed-and-reopened-higher) but a live instance of the still-open contradiction. Epistle 039 body was corrected to state this. **Standing TODO for the new home:** when §6a.6 actually closes, it must close in Calliope (the real fix), and the git corpus must reflect it — itself a test case for the freeze→Calliope propagation (039 claim 2).
- **038 gravel tension correction:** gravel/epistle-038.md was corrected after first commit — both originally-proposed tensions (cheap fan-out vs §5.6; multi-host asserted_by) were dissolved as a category error and an implementation note respectively. The record now shows no open tensions. If 038 ever moves toward ratification, that corrected record is the one to read.
- **038 ratification fork (deferred to human):** if gold 2 (seam as §6a.10 pull primitive) or gold 4 (§1.5 server role-shedding) is judged ratification-grade, that is a separate event requiring VERSION minor bump, corpus amendment, `frozen` transition, and git tag. Left to human call. (Under 039's logic, that ratification should happen via the *new* freeze step — see "the bind.")

---

## Concrete next actions

**From anima-corps (authoring surface):**
- ~~Shitcorp epistle-039~~ — DONE. Shitcorped (lite/Sonnet), accepted, builder committed: gravel/epistle-039.md written, epistle held at semi-liquid, §6a.6 framing corrected, Bench cite dropped from claim 3. No corpus update, no VERSION bump, no tag (the transition is the first use of the fixed freeze step).

**From anima-core (the build, needs both repos + running Calliope):**
- Phase 1: build freeze→Calliope propagation (039 claim 2). The freeze act writes the corpus amendment to Calliope via §3.10 supersession, atomically with the git/version update.
- Verify whether the embedded Calliope router in the FastAPI app is superseded by the standalone calliope-anima service (carried from the 038 discussion). If superseded, stripping the server shell is mostly deleting the `web/` layer. If not, §4 enforcement must move into the CLI/library seam first.

**Shitcorp the current build into aZero's inheritance — run by the live constellation (needs anima-core + running Calliope):**
- Use the current project state in Calliope as shitcorp material. The current anima-core build is an *argument* (§6.13 Mnemosyne — what the codebase argues, where it fractured without being named). Pan it: gold carries into aZero; gravel dies with the old shape (messy UI decisions, the server scaffolding 038 sheds, anything coupled to the two-repo / chat.html era).
- **Run it as a real orchestration — Ari + Hermes running the show.** This is deliberately a stress test of the 038 orchestration model: Hermes carries the intent ("sort the old build for aZero") into the constellation's frame; Ari triggers (G3a) — picks Mnemosyne, scopes the archaeology, defines what success looks like (the inheritance manifest). If Ari/Hermes run this cleanly, that is live evidence for 038 gold-1 (the host keeps triggering a live reasoning act). Note: this uses the *anima-core constellation* (Ari/Hermes/Mnemosyne), NOT the anima-corps authoring agents (builder/lite) — it cannot be run from the anima-corps-only session.
- **Legitimate telescoping (§6.15 / §6.13 / §7.3).** The current build is too large for single-pass; it decomposes into non-overlapping sub-scopes (web layer, agents, tools, calliope client, drive scripts, schemas); synthesis = the aZero inheritance manifest (real compression — what carries, integrated across sub-scopes, condition 3). Mnemosyne is licensed to telescope here; this is the swarm receipt on a real workload. Honor the swarm_manifest discipline.
- **Governed sort, not amnesiac rewrite.** Record each drop as a `discard_record` (§4.9, via negativa §3.20 / §6.6) with its *because*. The shape of what aZero drops is evidence; recording it stops the next project re-traversing the same gravel. A clean delete loses that. The reason the chat.html/server era is dead (it served an interface that was never the real one) is itself the gold that justifies aZero's shape — the gravel is where 038's whole argument came from.
- **Distinguish two artifact classes in the current Calliope.** It holds *corpus* artifacts (the migrated reference — the 039 single-source-of-truth thread; carries forward by definition) AND *build/project* artifacts (implementation decisions, schemas, agent wiring, UI cruft). This pass pans the **build/project** class only. Do not shitcorp the corpus here — that is a category error.
- **Can run early, independent of the bootstrap.** Archaeology is read-only against the current build; its discard_records and manifest are build-shitcorpus writes, not corpus freezes, so they do not need the Phase 1 freeze→Calliope step. It can run before/alongside Phase 1 to inform what aZero should be.
- **Preservation flag:** the inheritance manifest and its discard_records are themselves part of aZero's inheritance — write them so they survive the Calliope transition (into the shitcorpus aZero inherits), not stranded in the dying build's store.
- Method: Hermes intake → Ari triggers Mnemosyne → Mnemosyne archaeology (telescoped) → smelting → discard_records for the gravel → an aZero inheritance manifest (what carries, what dies, why).

**Then (Phase 2):** ratify 038/039 using the new freeze step.

**Then (Phase 3):** downstream epistles — CC-plugin delivery, CORPS_VERSION transform-or-dissolve, repo topology — surfaced by build pressure.

---

## File pointers

- `epistles/epistle-038.md` — The CLI Seam (liquid)
- `gravel/epistle-038.md` — 038 shitcorping record (corrected; verdict liquid)
- `epistles/epistle-039.md` — One Home (semi-liquid; shitcorped, held)
- `gravel/epistle-039.md` — 039 shitcorping record (verdict liquid)
- `epistles/epistle-040.md` — Model Intensity (liquid; not yet shitcorped)
- `epistles/epistle-041.md` — The Generative Build Procedure (vapor; not yet shitcorped)
- `corpora/anima/process.md` — lifecycle, the two loops, VERSION + CORPS_VERSION discipline
- `corpora/anima/logic.md` — §2.5, §3.3, §3.10, §4.2, §5.2, §5.6, §6a.5–6a.8, §6.15, §7.4
- `corpora/anima/substrate.md` — §6.12 Hermes, §6.12b Ari (G3a), §6.18 Argus, Bench

---

## Parked good ideas — real, but NOT to be baked into the current (improperly configured) system

These are staked as direction (epistles) but deliberately not implemented now. The present two-repo / server-shaped system is the wrong place to build them; they are for the properly-configured future home. Listed so they are not lost and not prematurely wired in.

- **Epistle 040 — Model intensity per task (liquid).** Anima should choose how capable a model each task needs — mechanical work on a cheap model, expensive reasoning on a strong one; and the cheap-execute / strong-validate pattern as the §3.3 externality requirement at the compute layer. Model intensity is a compute-substrate axis orthogonal to agent identity (not a §6.3 tuple member), owned by triggering authority (Ari G3a), recorded as provenance (§4.5), subordinate to the quality telos (§8, §3.3a). Amends 038: ride the host's execution but override its model-default (the host-vendor's incentive ≠ anima's telos). Four open hazards carried in the epistle. **A genuinely great capability — but it wants the real home and the model-policy layer to exist first. Do not retrofit onto the current system.**
