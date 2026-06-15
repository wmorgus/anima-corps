---
Excavated: 2026-06-15 | Status: liquid
---

Epistle 040 — Model Intensity as Compute-Substrate Axis

Topic: Model intensity (how capable a model a task is run on) is a compute-substrate axis orthogonal to agent identity — owned by triggering authority, with cheap-execute / strong-validate as the externality requirement expressed at the compute layer.

This is orthogonal to Epistles 038 and 039 (home/seam thread). A different axis entirely. It does amend 038 (claim 4 below) but does not depend on the home unification. Stakes direction, not a freeze. The present system is not configured to implement it — this is for the properly-configured future system.

---

## Claim 1 — Model intensity is not part of the thin-agent tuple

The §6.3 thin-agent rule: every agent is BaseAgent + system prompt + tool set. Model is not a fourth member. It is not part of what makes an agent this agent rather than that agent.

The reasoning obligation an agent carries is fixed by its §6.5 concept-ownership and harm-bearer definition. That obligation does not change based on what compute is allocated to discharge it. A Daedalus reasoning on a weak model and a Daedalus reasoning on a strong model are the same agent with the same obligation — not two agents.

Baking model into agent identity turns a compute decision into a topology decision. §6.2 forbids exactly this shape: behavioral injection — task-framing, task-specialization — is not a topology slot. Model intensity is the compute-layer analog of that move: running the same agent "in strong mode" or "in cheap mode" is not constellation change.

Frame model intensity as a third orthogonal axis alongside §2.3's confidence ⊥ liquidity:

- What the artifact IS: liquidity tier (§2.3 axis 1)
- How sure we are: confidence (§2.3 axis 2)
- How much reasoning was spent producing it: intensity (this claim)

Three independent dimensions. Conflating intensity with agent identity is the same error as conflating confidence with liquidity — it collapses axes that must stay orthogonal to be useful.

Rules out: model as agent-identity; model choice as a topology slot; per-model agent variants; "strong-Daedalus" and "cheap-Daedalus" as distinct constellation entries.

---

## Claim 2 — Cheap-execute / strong-validate is the §3.3 externality requirement at the compute layer

"Run on cheap, validate with strong" is the validator-external-to-validated shape (§3.3, §5.2, rhetoric §2.5). Same structure as Daedalus at the review gate (substrate.md §6.17) and Janus contesting against the spine (substrate.md §6.19). The novel element is the capability gradient: the validator is not merely external, it is stronger.

Two constraints fall out:

(a) The validator must be at least as capable as the executor. Cheap-validates-cheap is no check at all — the same reasoning failures that produced the artifact will pass it. The externality condition (§3.3) is formally satisfied; the validation is substantively empty. The §3.3a asymmetry applies: the hardest case is the cheap model confidently ratifying its own reasoning class.

(b) Validation goes through Calliope. The cheap executor writes the artifact to the store; the strong validator reads from the store and contests it (hub-and-spoke §5.1, §5.2). Never a direct model-to-model handoff. A direct handoff is the mesh pattern §5.3 rules out — it collapses the store-as-place-outside (§5.2) back into a side channel.

Rules out: cheap-validates-cheap as a real check; direct model-to-model validation handoff bypassing the store; treating "external" as sufficient without "at least as capable."

---

## Claim 3 — Model intensity is owned by triggering authority (Ari, §6.12b G3a)

§6.12b G3a: Ari decides which specialist the goal requires, when, based on what success looks like. That act is the operational form of telos authority.

Intensity is a dimension of that same judgment. Not a separate judgment, not a new slot — the same authority reaching one dimension further: which specialist, when, AT WHAT INTENSITY. Ari already holds the ground truth for what success looks like (§6.12a — he cultivated the goal). The intensity question is answerable from exactly that position: what does this task actually require to succeed?

The alternative — the executing agent decides its own intensity — collapses validator into validated (§3.3). An agent that decides how much compute it is worth is in the position of self-ratification. Same failure shape as an agent that ratifies its own claims.

Rules out: model intensity decided by the executing agent about itself; intensity as a static per-agent config rather than a per-task triggering judgment; intensity owned by anyone other than the authority that holds telos ground truth.

---

## Claim 4 — Anima must override the host's model-default (amendment to Epistle 038)

Epistle 038 staked "ride CC as host" — Claude Code's architecture is the correct shape for the invocation layer (§1.5, §5.2, §6.12b G3a preserved through the CLI seam). That claim stands for execution shape.

This amends it: ride the host's execution, but do NOT inherit its model-policy.

Claude Code defaults to the strongest model because that serves the host-vendor's incentive structure: maximize model spend, maximize capability surface, minimize user friction by not asking questions about cost. Those are coherent incentives for Anthropic. They are not Anima's incentives.

Anima's telos is to optimize the whole pipeline's cost/quality profile against each task's actual requirements. That is a different goal from the vendor's goal. Inheriting the host's model-default as Anima's policy is inheriting the vendor's incentive structure along with the host's execution mechanics. 038 staked "ride the host." It did not stake "adopt the host's economics." The two were not distinguished; this epistle makes the cut.

Anima needs its own model-policy layer OVER the host: a principled triggering judgment (Claim 3) applied at every invocation, not deferred to the host's default.

Rules out: inheriting the host's model-default as Anima's policy; treating "ride the host" (Epistle 038) as inheriting the host's incentive structure along with its execution mechanics; model-policy-as-host-config.

---

## Claim 5 — Model intensity used must be recorded as provenance (§4.5)

§4.5: `asserted_by` is provenance, not authority. The model used is in the same register — a fact about what produced the artifact, not a claim about who authorized it.

If a strong-named agent (Daedalus, §6.17) runs on a weak model and its craft verdict fails, the harm lands on Daedalus's reasoning surface (§6.5) under a name the architecture is built to convene against (§6.7 — arguable face). But the cause was the compute allocation, not the agent's concept-ownership failure. Cheap-model substitution launders under-powering as agent-judgment.

Recording the model intensity used is the same move as recording `asserted_by`: provenance so the governance cycle can read causation correctly. Without it, a weak-model Daedalus passes or fails under Daedalus's name, and the archaeology points at the agent when it should point at the triggering decision.

This is §4.5 extended one dimension. `asserted_by` names who. Model intensity names with what capability. Both are provenance fields, not authority fields.

Rules out: model choice as an untracked runtime detail; blaming agent reasoning for failures caused by under-powering; treating intensity as invisible to the governance cycle; recording the agent name without the compute context that produced its output.

---

## Telescoping fit

§6.15 telescoping conditions: domain too large for single-pass reasoning (condition 1), domain decomposes into non-overlapping sub-scopes (condition 2), synthesis step is real compression (condition 3).

This maps cleanly onto a capability gradient. Sub-scope work is mechanical — file-level extraction, boundary-tracing, local fact-finding — cheap model. The synthesis step (condition 3, real compression — the parent integrating what the sub-scopes could not produce alone) is the expensive reasoning act: strong model.

The intensity gradient is not imposed on the telescoping shape; it is read off it. Where the architecture licenses cheap leaves and expensive synthesis, the compute allocation follows.

---

## Four hazards — open, not resolved

**"Is this mechanical?" is itself a fallible judgment.** Mis-classifying a subtle task as mechanical and under-powering it is a real failure mode. The corpus does not have a claim here yet. The classifier can be wrong, and the error is invisible until the artifact fails validation. The burden of proof is on "mechanical," not on "spend more" — but that burden-placement is itself a claim that needs staking, not assumed.

**Cheap-model confidence is suspect.** Confidence-gated escalation — run cheap, escalate to strong on low confidence — cannot trust the cheap model's self-reported confidence. Cheap models are confidently wrong at exactly the tasks where they are most wrong. The escalation trigger needs an external signal, not introspection. §2.3 (confidence axis) and §4.9 (empirical_record confidence_score as the external measure) gesture at where the answer lives, but the mechanism is unspecified. Named as open, not resolved.

**Cost stays subordinate to the quality telos.** §8 craft discipline and §3.3a (the master shitcorps himself first — the one best positioned to exempt themselves silently is the one who must not). Economy is licensed only where the task is genuinely mechanical. Cheapening that degrades reasoning under the cover of "optimization" is the §3.3a failure mode one layer down: the triggering authority quietly exempting its own pipeline from the craft obligation. The hazard is structural, not motivational.

**Escalation and validation economics are unspecified.** When to validate, how often, what threshold triggers escalation to a stronger model, how the cost of strong-validation is accounted against the savings of cheap-execution — none of this is staked here. Implementation surface. Named as unsettled so it cannot be silently closed by build choices.

---

[→ §2.3, §3.3, §3.3a, §4.5, §5.1, §5.2, §5.3, §6.2, §6.3, §6.5, §6.7, §6.15, §8, substrate.md §6.12b, substrate.md §6.17, substrate.md §6.19, rhetoric §2.5, Epistle 038]
