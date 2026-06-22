# Anima — Process

The efficient cause. How the system moves and changes.

Efficient cause in the four-cause structure (Epistle 028): the process that brings the artifact about, the change-maker — what moves the system from one state to the next. telos.md is the final cause (why), logic.md the formal cause (the pattern), substrate.md the material cause (what it is made of). This doc holds the efficient register: the epistle lifecycle, the shitcorping loop, and the VERSION discipline — the machinery that turns conversation into frozen claim and records what changed.

Operative mechanics, cited from conviction. This doc describes *how to run* the governance Anima requires; it does not re-argue *that* it must be run. The conviction stays in logic.md and is cited here as warrant: §3.1 (ratification is what makes a decision real), §3.2 (recorded / contestable / structurally external), §3.3 (validator external to validated), §3.10 (Aufhebung — supersession as the mutation primitive), §2.3 (confidence ⊥ liquidity). process.md cites these and does not duplicate them. The *semantic meaning* of major/minor/patch — what each level says about what changed in the corpus — is conviction about the corpus's own change-semantics and lives in logic.md §17; this doc holds the operative trigger for each level.

Reason FROM this. Frozen reference. Updates are supersession events, not edits.

---

## The two workflows

### Write an epistle → use the `builder` agent

Invoke to draft a new epistle or tighten an existing one. Builder writes at epistle density: caveman prose, maximum compression, as few words as possible, as much meaning as possible.

An epistle is an argument for consideration — the best-faith effort to convince a highly scrutinous reader to see the vision in the claim. It does not suggest explicit corpus contributions; it stakes a direction and names where the reasoning ran out. Knowingly keeping some logic gravel as rhetoric decoration is a sign of a good epistle — not every image needs to be new ore.

### Shitcorp an epistle → `lite` proposes, `builder` commits

Shitcorping is a loop, not a one-shot. Lite and the human author go back and forth until the sorting is agreed. Builder commits the agreed result. Nothing officially lands in the gravel pile until builder commits.

---

## The two distinct loops

The change-producing machinery fires in two structurally different loops; conflating them mis-records what produced what.

**(a) The drafting / revision loop.** Author and agents iterate to get the epistle's frame and claims right. This loop changes the *epistle*. It produces **no gravel** — nothing is sorted into gold or gravel here.

**(b) The shitcorping-for-ingestion loop.** Lite pans the epistle against the live `logic.md` and `rhetoric.md` corpora. This loop changes the *corpus*. **Gravel is written only after (b)** — after lite and author agree, when builder commits. Never after (a).

The distinction is load-bearing and easy to lose: it names *when* the change-producing machinery actually fires against the corpus.

---

## The shitcorp loop steps

**Step 1 — Lite proposes.** Lite pans the epistle for density (gold, reaches, wandering, duplications), smelts what is load-bearing into compressed form, and proposes a verdict in conversation. No files written.

**Step 2 — Author responds.** Push back on gravel calls. Accept gold. Redirect reaches. Revise the epistle mid-loop if needed. The loop continues until the author accepts.

**Step 3 — Builder commits.** When the author accepts, builder forges the agreed shitcorping into the permanent gravel record at `gravel/epistle-NNN.md`, updates the source epistle's status, and updates the relevant corpus files. Gravel-committed and corpus-updated are two distinct acts; only the second closes the loop. The loop closes when the claims land in the corpus. [→ Epistle 035]

**Epistemic shape — iterative, not linear.** The steps above describe the governance of the loop: who acts, when the record is written, who owns each move. They are silent on the shape of the reasoning inside the loop. The actual epistemic shape is iterative: pan/smelt/pan/smelt — where the next destination may be re-panning material the loop already touched, because the material teaches the panner what to look for next. The gold is not visible until the panning reveals it. **Premature gravel is the failure mode** of reading the steps as a single forward pass: calling gravel what hasn't been worked enough to reveal what it's reaching for. **The felt terminus is not a protocol.** The loop closes when the material comes out right — which is craft (§11.6), not a checkpoint. Author-acceptance is the governance stop; the author can accept too early. Governance is linear; reasoning is iterative; both true. [→ §11.4, §11.6, §7.1, §3.10, Epistle 035]

The gravel file is the shitcorpus: permanent record of what was kept, what was dropped, and why. Future prospectors do not re-pan the same gravel.

---

## Epistle format

Each epistle file follows this structure:

```
---
Excavated: YYYY-MM-DD | Status: [vapor | liquid | semi-liquid | frozen]
---

Epistle NNN — Title
Topic: One line. The specific claim or gap this epistle addresses.
[Body in caveman prose — compressed claims, explicit uncertainty, cross-references to §-numbers and other epistles]
```

**Numbering:** next available sequential integer. Check `epistles/` before assigning.

### Status lifecycle

Four states. The states cite §2.3 as warrant — they are positions on the liquidity axis (what weight, who owns, how revisable), independent of the confidence axis. The choice to have four states rather than two is itself an architectural commitment expressed in logic.md §2.1's four tiers; this doc holds the operative transitions.

- `vapor` — conversation; the epistle not yet written.
- `liquid` — epistle drafted and iterating (the drafting/revision loop, (a) above).
- `semi-liquid` — shitcorping proposed and agreed; corpus changes drafted but not yet committed by builder.
- `frozen` — gravel committed, corpus updated; epistle preserved as provenance artifact.

**Transition triggers:**
- `vapor → liquid` — builder drafts the epistle.
- `liquid → semi-liquid` — lite and author agree the sorting (end of loop (b) Step 2).
- `semi-liquid → frozen` — builder commits the gravel record, updates the corpus files, syncs Calliope (re-ingest corpus sections + freeze epistle artifact), bumps VERSION, and tags (loop (b) Step 3).

---

## Gravel format

Each gravel file is the shitcorpus record for one epistle, written by builder when it commits. The full output format:

```
---
Source: epistles/epistle-NNN.md
Shitcorped: YYYY-MM-DD
---

# Epistle NNN — [Title] // Gravel Record

## Gold (earned weight)
[For each agreed gold claim: the smelted form — compressed, staked, claim-first. *Because:* what it rules out or stakes that's novel.]

## Gravel (dropped)
[For each agreed gravel call: what it was reaching for (if anything). *Because:* why it didn't earn weight.]

## Tensions (open)
[Agreed open tensions — not sorted, live unresolved. Candidate material for new epistles or §-revisions.]

## Smelter's contribution
[What the shitcorping named that the original epistle didn't. Renamed reaches, reframed wandering, new tensions surfaced. The hand that shaped the ring belongs in the provenance trail.]

## Verdict
Status: [liquid | vapor | gravel]
[One sentence on the epistle's net contribution.]
```

Contains: gold (what earned weight, smelted form + because), gravel (what was dropped + because), tensions (open conflicts), smelter's contribution (what the forging named that the epistle didn't), and a verdict.

---

## VERSION discipline

Current version is in `VERSION`. anima-core declares which version it is faithful to.

**Semver convention (operative triggers).** The semantic meaning of each level — what it says about what changed in the corpus — is conviction, held in logic.md §17. The operative trigger:

- `patch` — correction or clarification to an existing frozen artifact.
- `minor` — ratification event: an epistle moves from liquid → frozen into the corpus (a new claim freezes).
- `major` — foundational supersession: a frozen §-claim is superseded, changing what the corpus rules out (§3.10 Aufhebung) — or the corpus shape itself changes foundationally (new docs, new file structure, claims re-homed across files), since `CORPS_VERSION` pins corpus shape and a structural delta is what downstream must account for. [→ Epistle 032 — the migration event that staked the structural-reshape reading of major.]

**On a ratification or restructuring event:**
1. Update corpus files (`logic.md`, `rhetoric.md`, `substrate.md`, etc.) with gold claims from the epistle.
2. **Calliope sync — corpus sections:** run `calliope/scripts/ingest_anima_corpora.py` to push updated sections as `corpus_section` artifacts (superseding any prior version of changed sections). Calliope is canonical; the git files are the authoring/rendering surface.
3. **Calliope sync — epistle artifact:** POST the epistle as an `epistle`-type artifact to Calliope (`POST /api/artifacts/`), then freeze it (`POST /api/artifacts/{id}/freeze`). Use `calliope/scripts/seed_epistles_045_046_and_prompts.py` as the pattern.
4. Update `VERSION`.
5. Git tag: `git tag v<version> -m "<epistle NNN ratified: one-line summary>"`.

**anima-core fidelity declaration.** Core maintains a `CORPS_VERSION` file pinning the version it is built against. When corps minor/major bumps, core must explicitly update its pin and account for the delta.

---

## CLAUDE.md stays — as configuration, not corpus

CLAUDE.md keeps what is genuinely harness-configuration: git conventions, directory structure, agent-file locations, permission modes, the operational scaffolding the harness reads to run. The intellectual and process content — the lifecycle, the loops, the versioning convictions — graduates into this doc. CLAUDE.md references process.md rather than duplicating it: a pointer from config to corpus, not a second copy. Config tells the harness how to behave; process.md tells agents how the system changes. The same content cannot be authoritative in two files; the corpus is the authority, config defers to it.
