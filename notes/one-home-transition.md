# One Home — Transition Working Note

**Status:** working note, not corpus. Not frozen reference, not an epistle, not gravel. A session handoff capturing the conversation that produced epistles 038 and 039 and the sequencing plan for the unification they argue for.

**Branch:** `claude/tender-maxwell-gnrzfr` (anima-corps). Epistles 038 and 039 and the 038 gravel record are committed and pushed here.

**Pick-up context:** this thread ran in an environment with only anima-corps in reach. The next phase needs anima-core too. Resume where you can touch both repos plus the running Calliope.

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

**Then (Phase 2):** ratify 038/039 using the new freeze step.

**Then (Phase 3):** downstream epistles — CC-plugin delivery, CORPS_VERSION transform-or-dissolve, repo topology — surfaced by build pressure.

---

## File pointers

- `epistles/epistle-038.md` — The CLI Seam (liquid)
- `gravel/epistle-038.md` — 038 shitcorping record (corrected; verdict liquid)
- `epistles/epistle-039.md` — One Home (liquid, not yet shitcorped)
- `corpora/anima/process.md` — lifecycle, the two loops, VERSION + CORPS_VERSION discipline
- `corpora/anima/logic.md` — §2.5, §3.3, §3.10, §4.2, §5.2, §5.6, §6a.5–6a.8, §6.15, §7.4
- `corpora/anima/substrate.md` — §6.12 Hermes, §6.12b Ari (G3a), §6.18 Argus, Bench
