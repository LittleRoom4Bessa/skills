---
name: game-flow
description: Router for the indie game dev workflow. Decides which toolkit fits the current work — the game-dev loop (thoughts → prototype → landing) or OpenSpec — based on whether "done" is known or must be felt. Use when starting any non-trivial work, when unsure which skill applies, or when a prototype verdict needs routing to production.
---

# Game Flow — Router

One routing question decides everything:

> **Do you know what "done" looks like, or do you need to feel it to know?**

- **Know it** (save system, settings menu, level loader, CI, input remapping) → **OpenSpec** (`openspec-propose` → `openspec-apply-change` → `openspec-archive-change`). Skip the game-dev loop entirely. Nobody prototypes a save system.
- **Feel it** (combat feel, a new mechanic, juice, pacing) → **the game-dev loop** below. A spec cannot answer "is this fun" — only a playable thing can.

## The game-dev loop

```
thoughts ──ripe?──► prototype ──verdict──► landing ──┬─ kill → graveyard (idea returns to pool)
  (pool)             (2h spike)           (gate)     └─ keep → adopt
```

- **thoughts** — zero-friction idea pool. Capture anything; only ripe cards (hypothesis + slice) may leave. No grilling here — friction would kill the pool.
- **prototype** — 2-hour throwaway spike on an `exp/` branch. Opens with a one-round grilling gate that sharpens hypothesis and slice before the timebox starts. Output is evidence (GIF + verdict packet), never shippable code.
- **landing** — executes the verdict. Adopt = rewrite cleanly on a fresh branch, preserving feel parameters; kill = graveyard with a required cause of death.

## Handoff rules

1. **Never spec an experiment.** Specs are commitments; prototypes are questions. Do not create an OpenSpec change for "try X" — the loop exists so killing ideas is cheap.
2. **Prototype first, spec the adoption.** When verdict = keep:
   - whole change < 50 lines, no core system touched → landing adopts directly.
   - anything bigger → hand off to `openspec-propose`. The spec nearly writes itself: validated hypothesis, feel baseline GIF, extracted magic numbers. OpenSpec then tracks the production rewrite (this is what "tasks are created with OpenSpec" in AGENTS.md means).
3. **Pure engineering enters at OpenSpec directly.** No thought card needed — though if the work touches a game system, scan `thoughts/` for related cards first (standing instruction).
4. **savepoint is orthogonal.** It pauses/resumes *any* work — an experiment card or an OpenSpec change. Reach for it whenever the user parks work ("先到这", "park it") or resumes ("继续", "读档"), regardless of which toolkit is active.

## Route by situation

| User says / situation | Skill |
|---|---|
| "记一下…", "what if we…", raw idea | `thoughts` (capture) |
| "琢磨一下 T-012", develop an idea | `thoughts` (develop) |
| "有什么能做了", what's ripe | `thoughts` (harvest) |
| "试试这个想法", "prototype T-012" | `prototype` |
| keep / kill verdict on a prototype | `landing` |
| "先到这", "I'm stuck", park it | `savepoint` (save) |
| "继续 EXP-023", "what was I doing?" | `savepoint` (load) |
| "add save system", known-shape feature/fix | `openspec-propose` |
| Big validated prototype entering production | `openspec-propose` (via `landing` adopt) |
| Unsure which of the above | this skill — ask the routing question out loud and pick |
