# anima-corps

This repo holds the corpora and epistles for the Anima system. Two kinds of work happen here: writing epistles, and shitcorping them. This file is harness configuration — directory layout, agent locations, git mechanics. It is not the process authority.

**Process: see `corpora/anima/process.md`** — the epistle lifecycle, status states, the two workflows, the shitcorping loop, the gravel format, and VERSION semver semantics all live there. The corpus is the authority; this file defers to it. Where the two ever disagree, process.md wins.

---

## Structure

```
corpora/
  anima/
    logic.md        — conviction corpus; reason FROM this
    rhetoric.md     — doxa corpus; argument shapes and phrases
    process.md      — process authority; lifecycle, loops, versioning
  ur-software/
    *.md            — Pavel's positional diagnosis corpora

epistles/
  epistle-NNN.md   — one epistle per file, numbered sequentially

gravel/
  epistle-NNN.md   — shitcorpus record for each shitcorped epistle
                     what was kept, what was dropped, why
```

The corpora are frozen reference. Agents reason FROM them, not about them.

---

## Agent definitions

Project-local agents live in `.claude/agents/`:

- `builder.md` — writes epistles; commits shitcorpings to gravel
- `lite.md` — shitcorps epistles; proposes gold/gravel sorting

---

## Versioning — git mechanics

Current version is in `VERSION`. Semver semantics (what patch/minor/major mean for the corpus) are in `corpora/anima/process.md` and `logic.md §17`. The harness-level how-to:

**On a ratification or restructuring event:**
1. Update `VERSION`.
2. Git tag: `git tag v<version> -m "<epistle NNN ratified: one-line summary>"`.

**anima-core fidelity declaration:** core maintains a `CORPS_VERSION` file pinning the version it is built against. When corps minor/major bumps, core must explicitly update its pin and account for the delta.
