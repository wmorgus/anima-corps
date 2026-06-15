---
Excavated: 2026-06-15 | Status: liquid
---

Epistle 039 — One Home: Single Source of Truth, Not Single Repo
Topic: The corpus↔build split across two git repos has no governed pipeline either way. This is the §7.4 self-resonance failure made concrete — Anima sells a dojo→build pipeline it does not run on its own development. The unification target is single source of truth (Calliope), not single repo.

The scene that forces this. Run the 038 shitcorping → it moves the git corpus (epistles, gravel, corpus markdown in anima-corps). The corpus also already lives in anima-core's Calliope — that migration is done; it closed §6a.6 (frozen corpora invisible to runtime agents). So right now, on this branch, the Calliope corpus is stale relative to the git corpus. Two copies of one frozen reference. The drift is live, this minute. That drift is the claim.

---

## (1) The unification is single source of truth, not single repo

**One frozen reference, two homes that drift, is the §6a.6 failure one level up.** §6a.6 closed the case where the corpus lived in `docs/papers/` and runtime agents could not see it — corpus moved into Calliope. But it ALSO lives as git markdown in anima-corps, and 038's shitcorping just made the Calliope copy stale. The corpus is what agents reason FROM (§2.5 — coordinates, not facts). A reasoned-from reference with two copies that drift has no externality: §3.3 requires the validator external to the validated, recorded "somewhere both parties see and neither can retroactively edit." Two editable copies → no single place outside → §4.2 append-only satisfied in each copy separately while the pair drifts freely. The externality requirement is met inside each home and violated across them. Calliope is the single source of truth; the git markdown is an authoring/rendering surface that ratifies INTO Calliope, not a parallel copy of equal standing. Single source of truth ≠ single repo — the home is the store, not the directory.

## (2) Ratification must propagate to Calliope as part of the freeze act

**Drift is the freeze step leaving Calliope out.** Today freeze = update VERSION + git tag + edit corpus markdown (process.md VERSION discipline). The Calliope write is a separate manual migration → that gap is exactly where drift enters. process.md Step 3: the loop closes "when the claims land in the corpus." Under single source of truth, landing in the corpus MEANS landing in Calliope — via §3.10 supersession, the only mutation primitive — not just editing markdown. The markdown edit without the Calliope write is the loop reporting closed while the reasoned-from store still holds the predecessor. The freeze act must write the amendment to Calliope atomically with the git/version update, or it has not closed the loop. The git-markdown edit becomes the authoring gesture; the Calliope supersession is the freeze.

## (3) Same shape as Epistle 038, one level up

**038: put §4 discipline behind one wall, callers meet it as externality. 039: put Anima's whole loop — dojo→build — in one home, Calliope the single frozen reference everything reasons from.** 038 staked the CLI seam as the externality primitive at the invocation boundary (§5.2's place-outside-every-agent, one layer down) and the role-shedding at the process layer — both the same move. 039 is that move at the development layer: the externality principle applied to Anima-developing-Anima. §7.4 — Anima is its own first user — predicts the shape recurs; it does. Bench already stakes the one-host version at the substrate level: "Bench hosts the complete loop," pre-hinge forge/dojo → hinge → post-hinge, "one host, the whole alpha → spine → territory → omega → read-back." The two-repo development split contradicts the substrate's own one-host commitment. Anima sells a dojo→build pipeline and does not run it on itself — that is the §7.4 self-resonance failure stated plainly: gold from corpus work keeps resolving into build notes, build amendments keep warranting corpus changes, and neither crossing has a governed pipeline.

This is plausibly a structural-reshape, not a ratification — major-class per process.md VERSION discipline, the Epistle 032 reading (CORPS_VERSION pins corpus shape; a structural delta is what downstream must account for). The corpus's home changing standing — git-as-copy → git-as-authoring-surface-over-Calliope — is a shape change, not a new §-claim. But the version call belongs to the ratification step. This epistle is liquid; it stakes the direction, not the bump.

---

## Tensions named, not resolved

**Multi-device reachability is host-provided, not anima-built — pushes anima-core CLI toward a Claude Code plugin.** The author reaches Claude Code from personal laptop, phone, work laptop, because CC runs in the cloud, reachable from any device. Anima should inherit that flexibility. Building it into anima-core would be the `server` role 038 said to shed (§1.5 — borrowed obligation structure); riding CC-as-host gets it free. Direction this points toward, NOT settled: anima-core CLI distributed as a Claude Code plugin, running wherever CC runs; Calliope the persistent networked substrate any session reaches. This resurfaces 038's gold-9 multi-host `asserted_by` (§4.7 narrow extension, shared with Epistle 031) — multiple devices/hosts, one Calliope, provenance must distinguish them. The multi-device story IS the multi-host story. Open: the plugin-delivery mechanics, and whether Bench (the VS Code fork, rich workstation host) and CC-web/mobile (lightweight host) are two faces on one Hermes front door (§16.3) or strain substrate.md's "one extension because one front door." Genuinely open — do not read the plugin mechanism as decided.

**The discipline-boundary cost of unification.** The two-repo split crudely enforced two disciplines: corpus changes go through shitcorping/ratification; code changes go through normal dev. The repo wall was the enforcement. Collapse to one home → risk corpus markdown treated as just-more-source, edited in place — the §6a.8 mutable-frozen-artifact failure walking back in. The resolution direction: the discipline lives in Calliope + the ratification process (the store is append-only, supersession is the only mutation, §4.2/§3.10), not in the repo boundary. But this is a real cost to handle, not wave away. The split was intentional; self-contained tractability was a genuine benefit (recoverable via session/worktree isolation — name the cost, do not pretend it is free).

**CORPS_VERSION's fate.** CORPS_VERSION (core pins which corpus version it is faithful to) exists because of the split — it is the bridge across the repo boundary. The stale Calliope corpus is CORPS_VERSION showing its limit: a pin DETECTS a delta, it does not PREVENT drift. Under single source of truth there is no second copy → no pin to go stale. Open: does CORPS_VERSION dissolve, or transform into a "ratified-against" marker that survives inside one home (the marker of which supersession-state core was built against)? Reason it at ratification, do not assume it here. Genuinely open.

---

[→ §2.5, §3.3, §3.10, §4.2, §4.7, §5.2, §6a.6, §6a.8, §7.4, §1.5, §16.3, substrate.md Bench, Epistle 028, Epistle 031, Epistle 032, Epistle 038]
