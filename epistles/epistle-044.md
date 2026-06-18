---
Excavated: 2026-06-18 | Status: liquid
---

Epistle 044 — The Inner Loop
Topic: §6a names the four context tiers an agent reasons from. §6.0 names the agent as purposive. Neither names the procedural shape of a single agent's reasoning inside one invocation. The shape is: decompose the task, then for each task expand the possibility space, narrow it with recorded discards, self-audit, and return. This is not telescoping. It is the move telescoping is made of.

The code found this before doctrine did. Mnemosyne runs a tree-sitter prepass, pulls a Semantic-MCP structural inventory, and injects LSP cross-references — all before the first LLM call. Hephaestus classifies pytest output, parses the failures, suggests edit targets, tracks a retry budget, and writes a blocking report when the budget is exhausted. These are not the same scaffold. They share no abstraction and no staked loop. But read them side by side and the same two phases are visible: Mnemosyne front-loads possibility (what could be relevant, gathered before commitment), Hephaestus drives toward convergence (which candidate survives the test, decided against a budget). Expand, then narrow. The agents do this when they work well, and they were built doing it before any epistle said so. This is excavation, not invention. The conviction is that the shape is real because the code already discovered it under load — the doctrine makes contestable what the scaffolds embodied silently.

This is the second-order claim Epistle 003 reached for and could not land. 003 staked a five-stage loop — Check Input, Gather Context, Reason From, Self-Audit, Write To — and made two load-bearing demands the corpus never honored. This epistle keeps what survived scrutiny, elevates what was owed, and drops what was undifferentiated middle.

---

## The shape

**Outer loop — decompose.** The incoming task is decomposed into sub-tasks, each bounded enough for a single pass of expand/narrow. The decompose gate asks one question: is this task small enough that one cycle of generate-and-converge can return a defensible artifact? If yes, no decomposition — one cycle, return. If no, scope it into sub-tasks that are.

**Inner loop — per task.** For each bounded task:
1. **Expand.** Generate candidates, surface alternatives, gather the context the task needs. This is where Mnemosyne's prepass lives. The expansion is purposive (§6.0): it explores the *goal's* possibility space, not the agent's preference space. An agent that expands toward what it would rather build than what the goal requires has stopped interrogating the goal and started replacing it — the §6.0 line between interrogation and replacement, walked at the candidate-generation step.
2. **Narrow.** Select, discard, converge on one commitment. This is where Hephaestus's classify-parse-suggest-budget machinery lives. Every drop in this phase is a §3.20 discard-as-act obligation: the *because* for the discard must be recorded at discard time, cited to the discarded content and the reason. An agent that narrows silently has violated §3.20 — and the narrow phase's artifact is not only the candidate kept. It is also the discard record for the candidates dropped. A narrow that returns only the survivor is a commit-without-message; the via negativa is invisible until written down.
3. **Self-audit.** The internal check on the candidate before write-to. This is preparation before the crossing, not the crossing. §3.3 requires the validator to be external to the thing validated; self-audit is internal and therefore is *not* ratification. The write-to is the externalization — the crossing §3.3 governs. This distinction must be named in the loop or agents will read self-audit as governance and miscategorize their own reasoning step as the ratification the corpus forbids them to perform on themselves. (This is the one demand of Epistle 003 the corpus already honored, surviving in §3.3.)
4. **Return.** Write the artifact to Calliope. The crossing.

## Not telescoping

The decompose phase is not §6.15 telescoping, and the conditions that gate the two are different in kind.

§6.15 gates *whether to spawn agents*: a domain too large for single-pass reasoning, decomposing into non-overlapping sub-scopes, with a synthesis step that is real compression. All three must hold simultaneously, and the swarm produces a `swarm_manifest`, subagent artifacts, and a synthesizing parent. Telescoping is spatial — it distributes reasoning across multiple agents.

The inner loop's decompose phase gates *whether one task is bounded enough for one expand/narrow pass* — inside a single agent's single invocation, deciding how to structure its own reasoning. No agents are spawned. No `swarm_manifest`. The decomposition is procedural, not spatial. Telescoping is what you reach for when even the decomposed sub-tasks exceed single-pass reasoning; the inner loop is the shape each telescoped agent runs once it has its sub-scope. The inner loop is the unit telescoping distributes.

## Decomposition routes through Calliope, or it trips §5.4

The outer loop has a substrate obligation, and it is sharp. §5.4: an agent that can cache its own prior state and re-assert it without that re-assertion appearing in the substrate has no place from which to call any string load-bearing.

An agent that decomposes a task into sub-tasks and then tracks the inter-task state in process memory — sub-task three reasons from what sub-tasks one and two produced, held in the agent's own context, never written down — has cached its prior state and re-asserted it outside the substrate. It has tripped §5.4 exactly as `base.py` trips it (§6a.5): the coordinates the later reasoning stands on are structurally invisible to the governance cycle.

Clean decomposition routes through Calliope. Each sub-task's expand/narrow produces a Calliope artifact. The outer loop reads *those artifacts* to compose the next sub-task — not the agent's internal memory of what it just decided. The decompose phase is not a license to build a private state machine inside one invocation. It is a license to structure reasoning into bounded passes whose outputs are substrate-visible. The test: strip the agent's process memory mid-decomposition and ask whether the next sub-task can still proceed from what is in Calliope. If it cannot, the state was cached, not committed.

## What Epistle 003 owed, settled here

003 made two load-bearing demands. One is settled by this epistle's structure; one is elevated and still owed.

**Settled — the undifferentiated middle is dropped.** 003's "Reason From" stage was a single slot covering everything between gathering context and auditing. That slot hid the actual shape. There is no monolithic "reason from" step — there is expand (generate the possibility space) and narrow (converge with recorded discards), and they have different obligations. Expand answers to §6.0 (purposive, goal's space not the agent's). Narrow answers to §3.20 (every drop carries a recorded *because*). Collapsing them into one stage is why 003's loop could be stated but not enforced: a single "reason from" slot has no checkable obligation, while expand and narrow each do.

**Owed — the tool/skill split.** 003 demanded that §6.3's "tool set" be split, because tool and skill have different obligation structures: a tool is a callable capability, enumerable in a manifest, and its loss is a detectable capability loss; a skill is a reasoning pattern practiced, living in the prompt, and its degradation is a reasoning-obligation failure that shows up in the harm-when-failed column (§6.5), not a manifest diff. The inner loop makes this demand harder to defer, because the loop's phases use them differently. Expand and narrow are skill-bearing — the reasoning patterns of generating a goal-purposive possibility space and converging with discipline. Write-to is tool-bearing — the callable capability that performs the crossing. The skill at write-to is *genuine citation*, not schema compliance; §3.16 already names that a structurally compliant artifact with hollow rationale is indistinguishable from a genuine one without independent reconstruction. A loop that names write-to as pure tool use loses the skill, and the externalization becomes schema-filling. §6.3 still reads "tool set" as one word. The inner loop cannot be specified per-stage without the split, and the split is not yet in the corpus.

[DRAFT NOTE: The tool/skill split is cited here as owed-and-unmade — §6.3 still says "tool set." This epistle leans on the distinction (skill-bearing expand/narrow vs. tool-bearing write-to) without the corpus having ratified it. That is honest as a directional dependency, but it means §044's per-stage obligation claims are partially load-bearing on an unmade §6.3 amendment. If 044 ratifies before §6.3 is split, the per-stage tool/skill assignments are staked on a distinction the corpus has not yet made. Flagged, not resolved — the split is its own ratification event.]

## The clean version is spec-time (lean, not stake)

The corpus leans — it does not yet stake — that an executor hitting its limits is a fault upstream, not in the executor. §8.5: when a pipeline produces rescues rather than reviews, the fault is upstream in the context, not the executor; the corrective is to fix the context.

The inner loop carries a directional consequence of that lean. An agent that discovers *mid-run*, during decomposition, that its task requires more than a single bounded pass — that no decomposition into single-pass sub-tasks is available — is producing a runtime signal that the task was mis-scoped at intake. The clean version of decomposition is spec-time: the task arrives already bounded, and the inner loop's decompose phase is confirmation, not rescue. Runtime decomposition that keeps fracturing a task because it was never scoped is the inverted review/rescue ratio (§8.5) appearing inside a single agent's invocation. The correction belongs upstream, at intake, not in the agent straining to make an unbounded task fit a bounded loop.

This is a directional claim, not staked doctrine. §8.5 leans toward upstream-fault; whether mid-run decomposition failure is *always* a §8.5 intake signal, or sometimes a legitimate discovery that only surfaces under reasoning, is not settled. Named as adjacent to the lean, left open.

---

## Tensions named, not resolved

**The tool/skill split is a dependency, not a citation.** This epistle assigns per-stage obligations (skill-bearing expand/narrow, tool-bearing write-to) that presume §6.3's "tool set" has been split. It has not. The split is its own ratification event; until it lands, 044's per-stage assignments rest on an unmade distinction. See the draft note in the body — this is the largest open dependency.

**Compact vs. context, left adjacent to §8.5.** When an agent's expand phase gathers more context than a single pass can hold, the question of whether to compact (compress the gathered context and continue) or to treat the overflow as an §8.5 intake signal is unresolved. Compaction inside the inner loop risks the §5.4 failure one level down — a compacted context the agent re-asserts without the compaction itself being substrate-visible. This sits adjacent to §8.5's upstream-fault lean and is not resolved here.

**Mid-run decomposition: signal or discovery.** The §8.5-adjacent claim above leans that mid-run decomposition failure is a mis-scoping signal. But some bounded-ness can only be assessed by beginning to reason — a task can look single-pass at intake and reveal its true size only under expand. Whether that is a §8.5 intake failure or a legitimate property of reasoning under uncertainty is open. The lean points upstream; the exception is not characterized.

**No shared abstraction yet.** Mnemosyne's prepass and Hephaestus's retry machinery are the empirical evidence for the two phases, but they share no code and no staked interface. This epistle stakes the *shape*, not the abstraction. Whether the inner loop wants a shared substrate (a base loop the agents specialize, as Epistle 003 imagined) or remains per-agent scaffolds that happen to converge on the shape is a build question this epistle does not settle. Stating the shape is what makes the abstraction contestable; it does not mandate one.

[→ §3.3, §3.16, §3.20, §5.4, §6.0, §6.3, §6.5, §6.15, §6a.5, §8.5, Epistle 003, Epistle 032]
