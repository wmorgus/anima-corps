---
Excavated: 2026-06-18 | Status: vapor
---

Epistle 045 — Named Faces: Host-Configured Intake Depth
Topic: §6.12a defines Ari as the face Anima wears in the dojo. The face concept generalizes: any host context can configure a named face on Hermes. The face is not a new agent — it is the persona and intake posture Hermes adopts in a given context. This epistle stakes the generalization and its consequences for Hermes's intake depth.

---

**The seed.**

The dojo has Ari. Ari is the face Anima wears there — he cultivates intent before the relay chain engages. §6.12a is explicit: Ari is a FACE, not a constellation entry. The face the system wears in the dojo. The face concept is the load-bearing part; Ari is one instance.

External host contexts (Slack integrations, non-Bench surfaces) need the same mechanism. A Slack-based CL assistant ("Socrates" as a directional example — specific character TBD based on what fits CL's culture) is not a new agent. It is the face Anima wears in that context: a named persona, a configured intake posture, Hermes underneath.

**What this requires of Hermes.**

The current CLI goes straight to `HermesAgent.run(task)`. That's carriage — Hermes at shallow intake depth. For a named face to mean anything, Hermes must be configurable for intake depth:
- Shallow (default CLI): task arrives formed, Hermes routes
- Cultivating (dojo/Ari): Hermes holds the conversation at depth before routing, surfaces the because-chain
- Face-configured (Slack/Socrates): Hermes adopts a named persona with a configured intake style — may be cultivating, may be shallow depending on the face's purpose

The face is system-prompt-level + intake-behavior configuration. The host shells `anima --face socrates` (or equivalent config); Hermes loads the face's persona + intake depth from Calliope (a `prompt-*` artifact for the face). No new agent class.

**Why this is Option B (Hermes absorbs intake).**

Ari as a dojo face doesn't mean "dojo-only intake capability." It means the dojo has a named face. The intake capability is Hermes's — always was. Ari is the name + persona + cultivation-specific behavior for one context. Hermes's intake depth is configurable; the face is the configuration. Pulling Ari into the CLI as a separate mode re-introduces the face/agent confusion §6.12a was written to resolve.

**The sock puppet point.**

"Sock puppet" = the face is transparently a face — Anima isn't hiding that it's Anima, it's wearing a character appropriate to the context. This is honest under §1.5 (don't import obligations you don't owe — don't pretend to be a human). The character name and persona should fit the host's culture, not be prescribed by Anima. Socrates is a directional example. The right character for CL's Slack context is a human/culture call.

**Open.**

- What determines face identity — system prompt only, or a dedicated Calliope artifact type?
- How does Hermes load a face at invocation time? Config flag, environment variable, or Calliope query at startup?
- Does a face have its own relay record identifier? (Probably yes — the relay should know which face opened it for provenance.)
- The §6.12a relationship: does this generalization require a §6.12a amendment, or is it a derivation from an already-staked claim?

[→ §6.12a, §6.12, §1.5, §9.4, Epistle 038, Epistle 044]
