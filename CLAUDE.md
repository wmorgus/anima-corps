# anima-corps

This repo holds the corpora and epistles for the Anima system. Two kinds of work happen here: writing epistles, and shitcorping them. Claude's primary job in this repo is to support both.

---

## Structure

```
corpora/
  anima/
    logic.md        — conviction corpus; reason FROM this
    rhetoric.md     — doxa corpus; argument shapes and phrases
  ur-software/
    *.md            — Pavel's positional diagnosis corpora

epistles/
  epistle-NNN.md   — one epistle per file, numbered sequentially

gravel/
  epistle-NNN.md   — shitcorpus record for each shitcorped epistle
                     what was kept, what was dropped, why
```

---

## The two workflows

### Write an epistle → use the `builder` agent

Invoke when you want to draft a new epistle or tighten an existing one. Builder writes at epistle density: caveman prose, maximum compression, as few words as possible, as much meaning as possible. It does not argue — it stakes a direction and names where the reasoning ran out.

Usage: describe the claim or direction you want to stake. Builder produces a draft epistle in the correct format. You revise from there.

### Shitcorp an epistle → `lite` proposes, `builder` commits

Shitcorping is a loop, not a one-shot. Lite and the human author go back and forth until the sorting is agreed. Builder commits the agreed result. Nothing officially lands in the gravel pile until builder commits.

Distinguish two loops: (a) the drafting/revision loop — author and agents iterating to get the epistle's frame and claims right, which produces no gravel — from (b) the shitcorping-for-ingestion loop below, where lite pans the epistle against the live `logic.md` and `rhetoric.md` corpora. Gravel is written only after (b), never after (a).

**Step 1 — Lite proposes.** Lite pans the epistle for density (gold, reaches, wandering, duplications), smelts what's load-bearing into compressed form, and proposes a verdict in conversation. No files written.

**Step 2 — Author responds.** Push back on gravel calls. Accept gold. Redirect reaches. Revise the epistle mid-loop if needed. The loop continues until the author accepts.

**Step 3 — Builder commits.** When the author accepts, builder forges the agreed shitcorping into the permanent gravel record at `gravel/epistle-NNN.md` and updates the source epistle's status.

The gravel file is the shitcorpus: permanent record of what was kept, what was dropped, and why. Future prospectors don't re-pan the same gravel.

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

**Status lifecycle:**
- `vapor` — conversation; the epistle not yet written
- `liquid` — epistle drafted and iterating
- `semi-liquid` — shitcorping proposed and agreed; corpus changes drafted but not yet committed by builder
- `frozen` — gravel committed, corpus updated; epistle preserved as provenance artifact

**Numbering:** next available sequential integer. Check `epistles/` before assigning.

---

## Gravel format

Each gravel file is the shitcorpus record for one epistle. Written by lite after shitcorping. See `.claude/agents/lite.md` for the full output format.

```
gravel/epistle-NNN.md
```

Contains: gold (what earned weight, smelted form + because), gravel (what was dropped + because), tensions (open conflicts), smelter's contribution (what the forging named that the epistle didn't), and a verdict.

---

## Corpora

The corpora are frozen reference. Agents reason FROM them, not about them.

- `corpora/anima/logic.md` — Anima's conviction corpus. §-numbered claims, each with what it rules out.
- `corpora/anima/rhetoric.md` — Argument shapes and doxa moves. Hermes reaches for this in conversation.
- `corpora/ur-software/*.md` — Pavel's ur-software corpora. Positional diagnosis on the world of forms.

When an epistle duplicates a ratified §-claim, lite names it. That is not failure — it is the because for the discard. The gravel pile is evidence too.

---

## Versioning

Current version is in `VERSION`. anima-core declares which version it is faithful to.

**Semver convention:**
- `patch` — correction or clarification to an existing frozen artifact
- `minor` — ratification event: an epistle moves from liquid → frozen into the corpus
- `major` — foundational supersession: a frozen §-claim is superseded, changing what the corpus rules out

**On a ratification event:**
1. Update `VERSION`
2. Git tag: `git tag v<version> -m "<epistle NNN ratified: one-line summary>"`

**anima-core fidelity declaration:** core maintains a `CORPS_VERSION` file pinning the version it is built against. When corps minor/major bumps, core must explicitly update its pin and account for the delta.

---

## Agent definitions

Project-local agents live in `.claude/agents/`:

- `builder.md` — writes epistles; commits shitcorpings to gravel
- `lite.md` — shitcorps epistles; proposes gold/gravel sorting
