---
Source: epistles/epistle-047.md
Shitcorped: 2026-06-22
Verdict: gravel — return for rebuild
---

# Epistle 047 — load_face Is a Pull // Gravel Record

047 stakes the load mechanism 045 left open: Hermes selects the face by live reasoning
and pulls it from Calliope at task time. The instinct is right and inherited cleanly from
045/046 (pull-not-push off §6a.10/§5.4). But the record overcharges three of its four
claims against frozen material, and the one piece of machinery it leans on hardest —
claim 4's "the mechanism already exists" — does not match the code it cites. The seam the
builderlite flag named (is claim 2's §5.4 force unconditional or conjunctive with claim 1?)
is real and unresolved: the epistle's own second Open concedes the answer claim 2's body
denies. Verdict gravel, not liquid: the load-mechanism finding is recoverable, but it has
to be rebuilt on the opens 045/046 actually left, with claim 4's mechanism corrected to
what `base.py` does and the §6.1 harm test on faces actually run.

---

## Gold (earned weight)

**The pull-not-push instinct, inherited correctly.** Claim 2's core — a face held in
process memory and re-asserted without the re-assertion appearing as a substrate read is
the §5.4 pattern, so the face must be pulled — is the right reading and is faithfully
carried from where 045 and 046 left it. 045 staked it as the explicit §6a.10 open ("the
corpus has not staked it"); 046 inherited the open without closing it. §6a.5 already names
the live instance of exactly this violation: `base.py` reads bedrock from disk and
re-asserts it on every invocation, invisible to the governance cycle. A pulled face is a
read event; a pushed face is cached prior state. That distinction is sound and is the
epistle's real contribution.

**The face-is-context-injection-not-mode-switch framing (claim 3's first half).** "Hermes
is still Hermes; the face overlays operating context for one task; the agent underneath,
its hermeneutic obligation (§6.12), is unchanged" is a clean reading of §6.2 outcome 1
(behavioral injection) read together with §6.12a's face/agent distinction. The *register*
claim — a face changes the register Hermes operates in, not which agent runs — is faithful.
What it does NOT yet earn is the classification verdict it rides on (see Gravel: the §6.1
test).

**Both Opens are real and correctly left open.** Face provenance on the relay (045 left it,
047 keeps it) and programmatic face provenance (the `--face` write-trail question) are both
genuine unstaked surfaces. Keeping them open is correct. The second Open is more than
housekeeping, though — it silently contradicts claim 2's body (see Gravel).

---

## Gravel (dropped or returned for rebuild)

### 1. Claim 4's mechanism does not match the code it cites — the load-bearing failure

Claim 4: "`_ensure_context_loaded` reads the entry's `cites` list and fetches each cited
artifact; faces ride that same loading path with no new machinery." And earlier, claim 2:
"Hermes calls `load_face(face_id)`: fetch the `prompt-*` artifact from Calliope, return its
`full_text`."

The instruction was explicit: claim 4's mechanism is only as good as the code it leans on.
It does not hold. Checked against `aZero/src/azero/lib/agents/base.py`:

- **`load_face` does not exist.** Grep across `aZero/src` returns nothing for `load_face`,
  `face_id`, or `--face`. The function claim 2 describes as the pull primitive is not in the
  codebase. The epistle states the call signature ("it calls `load_face(face_id)`") as if it
  were current; it is vapor.

- **There is no `prompt-*` artifact type, and no `prompt-builder-001`/`prompt-lite-001` in
  Calliope.** The Calliope schema (`calliope-anima/api/artifacts/types.py`) has no
  `agent_prompt` type — the closest is `agent_config`. No `prompt-builder` / `prompt-lite` /
  `prompt-hermes` artifacts exist in the store. The `prompt-*` convention claim 4 says
  "already exists" is a convention only in the epistles (045/046) and the test fixtures, not
  in ratified Calliope types. `_ensure_context_loaded` detects a prompt artifact by
  `type == "agent_prompt" OR truthy content.prompt_text` — both untyped-by-the-schema
  conventions, not a ratified artifact contract.

- **The mechanism `_ensure_context_loaded` actually implements is not a task-time pull of a
  face — it is a one-shot, cached, startup composition of a SINGLE prompt artifact.** The
  method:
  1. is guarded by `if self._system_prompt_parts is not None: return` — it runs **once per
     agent instance** and caches the result in process memory;
  2. partitions `cites` into exactly **one** prompt artifact (the first whose type/field
     matches) plus N background `cited_texts`, and **raises `PROMPT_ARTIFACT_NOT_FOUND` if
     there is not exactly one non-empty prompt**;
  3. composes them into a frozen `(cited_context, agent_prompt)` tuple that is the agent's
     system prompt for the rest of the session.

  This is precisely the structure claim 2 says §5.4 forbids: the prompt is pulled **once**,
  then cached in process memory and re-asserted on every subsequent provider call without
  the re-assertion appearing in the substrate as a fresh read. `_ensure_context_loaded` is
  the §6a.5 violation, not its cure. The epistle cites this method as the mechanism that
  *honors* the pull; the code shows it is the cached-push §6a.5 names by name. Claim 4 cites
  its own counterexample.

- **"Faces ride that same loading path with no new machinery" is false in two directions.**
  (a) The current path loads *one* prompt (the agent's own); a face is a *second, different*
  prompt selected at task time. The single-prompt partition would have to be rebuilt to
  carry a face — that is new machinery, not the existing path. (b) The current path runs at
  agent-init and caches; a face selected by live reasoning mid-session ("write this up with
  builder") arrives *after* `_ensure_context_loaded` has already run and cached. There is no
  task-time re-pull hook. The mechanism claim 4 leans on cannot, as written, do the
  task-time live-selection thing claim 1 requires.

**Consequence for the verdict:** claim 4 is the structural keystone — claims 1, 2, 3 all
assume the face is loadable "the way Hermes knows everything else, through Calliope by
citation." The keystone is built on a function that does not exist and a method that does
the opposite of what the claim says. This alone returns the epistle to gravel. The fix is
not cosmetic: the load mechanism has to be specified against what `base.py` actually does
(single cached startup composition) and what would have to change (a task-time face-pull
that is itself a substrate read, replacing the cache for the face slot). 046's own Open —
"how that dispatch wires to the relay (dispatch wiring) is not yet specified" — is exactly
this gap, and 047 closes it by assertion rather than by specification.

### 2. Claim 2's §5.4 force is conjunctive with claim 1, not unconditional — and the epistle's own second Open admits it

This is the builderlite seam, and it is the sharpest tension in the record. Claim 2 says the
pull is "forced, not chosen" because holding a face in process memory without a substrate
read violates §5.4 — stated as unconditional, applying to "a face config held in process
memory and re-asserted" regardless of how the face got there.

But §5.4's force is about *re-assertion without a substrate read appearing*. It does not, by
itself, mandate that the read be a **pull at task time**. A face injected by `--face` flag
and then *written to Calliope as a provenance record* would satisfy §5.4's letter — the
re-assertion would appear in the substrate as a write event — without being a live
task-time pull. §5.4 forbids the invisible re-assertion; it does not by itself choose
pull-over-write. The thing that makes the *pull* (rather than a flag-plus-write) the forced
form is §6a.10's externality argument — pull "makes the retrieval visible in the substrate
as a read event" *at every invocation* — and §6a.10 is **[OPEN]**, explicitly "named here
as an open surface," the choice "not specified." So the force claim 2 needs is not §5.4
alone (which a flag-plus-write also satisfies); it is §5.4 **plus** the §6a.10 pull-vs-push
choice that the corpus has not made.

The epistle half-knows this. Its **second Open** asks: "Does flag-driven selection need its
own Calliope write to leave a provenance trail, so the escape hatch does not become the
silent push §5.4 forbids?" That Open concedes the exact thing claim 2's body denies: if the
flag path can satisfy §5.4 with a *write* (not a pull), then §5.4's force is **not**
pull-specific and **not** unconditional — it is conjunctive with the §6a.10 choice. Claim 2
asserts the conclusion ("pull is forced, not chosen") that the second Open reopens as
genuinely unsettled. Body and Open contradict.

Answering the builderlite's direct question: **claim 2's §5.4 force does NOT apply equally
to the flag path as a pull-requirement.** §5.4 applies to *both* paths as a
visibility-requirement (no invisible re-assertion), but it is satisfiable by a write on the
flag path. So:
- The flag is a valid escape hatch *only if it still leaves a substrate trace* — but that
  trace can be a write, not necessarily a pull. The epistle's framing ("the flag triggers a
  pull or a write") is closer to right in the Open than in claim 2's body.
- This **weakens claim 2's "forced, not chosen."** The pull is forced for the live path by
  §6a.10's externality-at-every-invocation argument *if* §6a.10 resolves toward pull — and
  §6a.10 is open. For the flag path, even that argument is weaker, because a programmatic
  caller has no per-invocation reasoning step whose visibility the pull protects.

This is the 045-generalization-as-derivation shape repeating (the same shape the 045 and
046 gravel both caught): a conclusion that is really downstream of an *open* corpus choice
(§6a.10) is staked in the body as though §5.4 forces it alone. The honest form: "§5.4
forbids invisible re-assertion on both paths; whether the visible form is a task-time pull
or a flag-plus-write is the §6a.10 open, leaning pull for the live path on the
externality-at-every-invocation argument, unsettled for the flag path." That is what the
second Open already says; the body should be demoted to match it.

### 3. Claim 1's §6.12b citation is overcharged — §6.12b is about orchestration triggering, not face selection

Claim 1: "Hermes detects the intent and selects the face. This is §6.12b: triggering is the
operational form of telos authority... Pre-wiring the face at CLI invocation compiles that
live decision into structure — the same laundering §6.12b names."

§6.12b (substrate.md, [→ Epistle 037]) is checked. Its "triggering is the operational form
of telos authority (G3a)" claim is specifically about **Ari deciding which specialist the
goal requires, when** — orchestration invocation, "who gets invoked, when." It is the
orchestration-authority half of Ari, the routing act read as the exercise of telos
authority. It says nothing about *face selection*, and it names no "laundering."

Two problems:

- **Wrong referent.** §6.12b's triggering is *specialist orchestration* (invoke Heph,
  invoke Clio). 047 transposes it to *face selection* (wear builder, wear lite) as if the
  two were the same operational act. They are not obviously the same: orchestration triggers
  a *different agent* down the relay; face selection changes the *register of the same
  agent* (Hermes/Ari) at the threshold. The transposition might be defensible as an
  *extension* of §6.12b's "triggering-as-exercise" shape to a new act-class — but it is
  staked as a *reading* of §6.12b ("this is §6.12b"), which it is not. Same overcharge shape
  as #2: extension dressed as derivation.

- **"The laundering §6.12b names" — §6.12b names no laundering.** The word and the concept
  are not in §6.12b. The "compiling a live decision into structure" idea is the epistle's
  own construction (a real and reasonable worry), but attributing it to §6.12b as something
  the section "names" is a phantom citation. If the laundering concept is load-bearing, it
  needs its own warrant — §6.0's goal-interrogation-not-replacement, or §15.18's
  telos-colonization-at-intake (pre-loading downstream work before the human articulates it)
  are the on-point sections, not §6.12b's G3a.

The recoverable core of claim 1: "the primary path has a reasoner at the threshold; the flag
does not" is a sound *design* observation. It just is not §6.12b, and it does not by itself
establish that the flag path is illegitimate — only that it bypasses the reasoning step
(which the second Open then correctly flags as needing its own provenance).

### 4. Claim 3 asserts the §6.1 harm-identity test result without running it — the test the instruction demanded

Claim 3: "builder and lite are faces, not constellation entries: §6.1 returns same harm,
different material — the authoring register is a surface Hermes wears, not a distinct
harm-bearer that would license its own slot."

This is asserted, not shown — and 046 explicitly deferred exactly this test. 046's gravel
and body both say the builder/lite classification "requires re-running §6.1's harm-identity
test... against authoring work specifically. This epistle does not run that test." 047 states
the *result* of the test 046 said was unrun, without running it. That is the 045/046
generalization-as-derivation pattern a third time: 046 left the §6.1 test open for the
authoring agents; 047 closes it by fiat.

Running the §6.1 test as the instruction demands — same-harm-different-material requires
showing the *harm profile of bad corpus authoring through a face matches Hermes carriage
harm*:

- **Hermes's harm (§6.12):** "a request is routed under a misread; downstream agents reason
  from a distorted intake; the human's *because* fractures at the threshold." Harm-bearer:
  every downstream agent on the routing chain, and the human whose request was misrouted.
  This is a **carriage/translation** harm at the *intake threshold* — meaning distorted in
  transit from human to architecture.

- **Bad corpus authoring's harm:** an epistle stakes a claim that does not hold (overcharges
  a derivation, launders an extension as a reading — the very faults this record catches),
  it freezes into the conviction corpus, and **every agent that later reasons FROM that
  corpus reasons from a corrupted bedrock.** Harm-bearer: every agent in the constellation
  (they reason from logic.md/substrate.md), the whole downstream pipeline, and the system's
  self-coherence. This is a **bedrock-corruption** harm at the *authoring* surface —
  meaning corrupted at the source the whole system reasons from.

These are **not** obviously the same harm. Hermes carriage harm is *transient and
per-request* (one request misrouted; the next is fresh). Authoring harm is *persistent and
systemic* (a bad freeze poisons every future read until superseded). The bearers overlap
(downstream agents) but the *temporal and structural shape* differs: a misread at carriage
is one fracture at one threshold; a bad freeze at authoring is a standing fracture in the
ground everyone stands on. That is closer to the §3.3a "master shitcorps himself first"
concern (§6.12a) — the authoring face's distinctive harm is *exempting its own output from
the quality check*, which is not a carriage harm at all.

This does not settle that builder/lite *must* be a slot — it may still resolve to face under
a more careful reading (e.g., the harm is "information-poet" harm in both cases: the human
or the system "leaves with the stated question answered, the real one untouched," the §11
harm §6.12a invoked for Ari). But that argument has to be *made*, against the §6.1 test, and
047 does not make it. The §6.1 mechanism §6.12a used for Ari was "same information-poet harm
as §11, different material (cultivation vs. carriage surface)." 047 would need the parallel:
"same [what?] harm as [what slot?], different material (authoring vs. carriage surface)" —
and it needs to defend the harm-identity against the bedrock-corruption-vs-transient-misread
asymmetry above. The instruction's demand stands unmet: same-harm-different-material is
asserted in claim 3 but not shown.

---

## Path to rebuild

The load-mechanism finding is worth recovering. To freeze, 047 needs:

1. **Fix claim 4 to the code.** State what `_ensure_context_loaded` actually does
   (single-prompt, startup-cached, composed-once) and what would have to change to load a
   face at task time. Drop "`load_face(face_id)`... return its `full_text`" and
   "no new machinery" — both are false against `base.py`. If `prompt-*`/`agent_prompt` is to
   be the face's home, that is a Calliope type that does not exist yet (the 045 Open "is a
   face a `prompt-*` artifact or a dedicated type?" is still open and 047 inherits it).

2. **Demote claim 2 to match the second Open.** §5.4 forbids invisible re-assertion on both
   paths; the visible form (task-time pull vs. flag-plus-write) is the §6a.10 [OPEN] choice,
   leaning pull for the live path on §6a.10's externality-at-every-invocation argument,
   genuinely unsettled for the flag path. "Forced, not chosen" overclaims; the force is
   conjunctive with an open corpus decision.

3. **Reclass claim 1's §6.12b cite as an extension, not a reading**, or re-warrant the
   "laundering" worry to §6.0 / §15.18 (its actual home), and cut "the laundering §6.12b
   names."

4. **Actually run the §6.1 harm test for builder/lite** (the test 046 deferred and 047
   assumed), defending same-harm-different-material against the
   bedrock-corruption-vs-transient-carriage asymmetry — or honestly carry it as the open 046
   left, rather than stating its result.

Three of four claims overcharge an open or frozen section; the keystone claim leans on code
that does the opposite of what it says. The instinct (pull-not-push for faces) is sound and
inherited cleanly. Rebuild on the opens, not past them.

---

## Re-shitcorp pass (2026-06-22)

Fresh adversarial pass on the rebuild. All four path-to-rebuild items resolved; verdict
**liquid**, ready to freeze. No new gravel — two soft spots noted below, neither touching a
warrant.

**1. Claim 4 fixed to the code — confirmed.** The "needs to be built" reframe is correct
against `aZero/src/azero/lib/agents/base.py`. Verified: `load_face`, `face_id`, and `--face`
return nothing across the Python trees (grep clean). `_ensure_context_loaded` is exactly the
single-prompt startup-cached composition the epistle now describes — guarded by
`if self._system_prompt_parts is not None: return` (base.py:89-90, runs once per instance),
detects the prompt by `type == "agent_prompt" OR truthy content.prompt_text` taking the first
match (base.py:158-164), raises `PROMPT_ARTIFACT_NOT_FOUND` if none (base.py:176-181), and
freezes a `(cited_context, agent_prompt)` tuple (base.py:187). The epistle now correctly
identifies this cache as the §6a.5 violation (faithful to §6a.5 verbatim), not its cure — the
old "cites its own counterexample" failure is gone. The `agent_prompt`/`prompt-*` type
absence is also confirmed: canonical Calliope schema
(`calliope-anima/api/artifacts/types.py`) has `AGENT_CONFIG = "agent_config"` and no
`agent_prompt` member, no `prompt-*` type, no `prompt-builder-001`/`prompt-lite-001` in the
store. The epistle correctly states 047 stakes the pull to build and inherits 045's
type-home open rather than asserting the machinery exists. **Resolved.**

**2. Claim 2 demoted — confirmed.** §5.4 is no longer overclaiming: the body now states §5.4
forbids only invisible re-assertion ("no place from which to call any string load-bearing" —
verbatim) and that a `--face` flag plus a provenance write satisfies §5.4's letter. The
pull-over-write force is correctly relocated to §6a.10's lean ("the pull is the right form
given §6a.10's direction, not the only form §5.4 allows"), and §6a.10 is correctly stated as
`[OPEN]` (verbatim) leaning pull on the externality-at-every-invocation argument. "Forced,
not chosen" is removed; body and second Open now agree where they previously contradicted.
**Resolved.**

**3. Claim 1 re-warranted — confirmed.** §6.12b is gone from the claim-1 paragraph, the body,
and the trailer (grep clean; the only "6.12b" hit is the old frontmatter shitcorp line). The
"laundering §6.12b names" phantom cite is removed. The telos-colonization worry is now
warranted to §15.18 (verbatim: "telos-colonization at intake — an agent pre-loading
downstream work... before the human has articulated it, crosses §6.0 goal-interrogation into
goal-replacement at the intake boundary") and §6.0 (goal-interrogation-not-replacement). The
epistle's phrasing is a faithful paraphrase of the §15.18 amendment text, not an extension
dressed as a reading. The flag-as-escape-hatch is consistent with claim 2's demotion and the
second Open. **Resolved.**

**4. §6.1 test run — confirmed; it closes, it does not assert.** This was the item to press
hardest, and the rebuild earns it. The body grounds harm-identity in the *same* mechanism
§6.12a used for Ari — "same information-poet harm as §11" (verbatim against §6.12a), the
stake/work that looks done over an actual gap — rather than asserting "same harm." It then
directly confronts the bedrock-corruption-vs-transient-carriage asymmetry the first pass
raised, and resolves it on principle: reach/persistence is "the *consequence* of the
information-poet failure, not a second kind of harm... how far that failure propagates, not a
distinct bearer that would license its own slot." That is a sound reading of §6.1, whose
licensing coordinate is a *distinct reasoning obligation* (mechanism + bearer-type), not blast
radius — same shape as the forge precedent §6.12a already ratified under outcome 2. The
conclusion ("now the §6.1 run says so, rather than the register framing assuming it") is
earned by the run, not by fiat. The §3.3a "master shitcorps himself first" angle the first
pass floated as a possible distinct harm is correctly *not* treated as a §6.1 slot-licensing
question — it is a discipline on the authoring face (the harm 046 already located and
warranted), not a distinct bearer 047 must close. Its omission does not leave the test open.
**Resolved.**

**Soft spots (noted, not gravel):**
- *Claim-3 header terminology.* "Face is a context injection, not a mode switch" sits one
  word away from §6.2 outcome 1 ("behavioral injection / mode"), which is the not-even-a-face
  category. The epistle uses "context injection" in its own register (overlaying a register on
  the same agent) and the §6.1 run unambiguously lands it on §6.2 outcome 2 (face, clause-2
  cited correctly), so the classification is right — but the header's proximity to outcome-1
  vocabulary could read as a conflation on a fast skim. Cosmetic.
- *Title vs. body.* "load_face Is a Pull" names a function the body says does not exist. The
  body corrects this immediately and explicitly ("the face-pull does not exist yet... 047
  stakes [it] to build"), so the title is aspirational-by-design, not an overclaim. A
  title-only skim could mistake it for current machinery. Cosmetic.

**Verdict:** liquid. The keystone is fixed to the code, the two open-charged claims are
demoted to their actual warrants, and the §6.1 test is run rather than assumed. The
load-mechanism finding is recovered and rebuilt on the opens 045/046 actually left. Advance
to semi_liquid pending the human freeze step.
