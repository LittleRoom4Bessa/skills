---
name: prototype
description: Turns a ripe thought card into a playable throwaway spike on an exp/ branch inside a 2-hour timebox, ending in a verdict packet for the user's keep/iterate/kill decision. Use when the user promotes an idea to prototype ("prototype T-012", "试试这个想法") or iterates on an active experiment card.
---

# Prototype — 2-Hour Spike

Turn a ripe thought into something *touchable*. The output is evidence for a human verdict, not shippable code.

## Setup

1. Read the thought card. Confirm it is **ripe** (Hypothesis + Slice filled). If not, stop and suggest developing it first.
2. **Grill the card — one round, no more.** Stress-test the hypothesis and slice with a short interview: ask the few questions whose answers would change what you build (max 3–5), each with your recommended answer. Facts about the codebase are your job to look up; only decisions go to the user. Friction is deliberately spent here, not in the thoughts pool — the 2-hour timebox deserves a sharp target. If the answers reshape the hypothesis or slice, update the thought card first; if they reveal the idea isn't testable, send it back to develop.
3. **State the question.** Write the question this prototype must answer at the top of the experiment card, one sentence, in question form. A prototype that answers the wrong question wastes the whole timebox — this makes the target checkable before the build starts.
4. Create an experiment card `experiments/EXP-<number>.md`:

```markdown
---
id: EXP-023
from: T-012
status: active        # active | paused | merged | graveyard
created: YYYY-MM-DD
branch: exp/coin-explosion
pause_count: 0
---

## Hypothesis
## Slice
## Verdict packet     # filled at exit
## Savepoint          # filled by the savepoint skill
## Outcome            # filled by the landing skill
```

5. Create branch `exp/<slug>`.

## Rules (non-negotiable)

- **Timebox: 2 hours.** If it can't be touched in 2 hours, the slice is too big — cut it smaller or send the card back to develop.
- **Explicit permission to write bad code.** Hardcode, duplicate, skip tests, skip abstractions. The only quality bar: the user can touch the feature.
- **Do not modify existing modules.** The prototype lives in its own scene/file/sandbox as far as the engine allows.
- **Isolate the core.** Keep the feel parameters and the core interaction concentrated in one place (one config resource, one node). The prototype is throwaway, but the soul must be extractable — landing's rewrite starts from this spot.
- The exp branch is **never** merged into main. What happens to the code afterward belongs to the landing skill.

## Exit checklist

- It runs and the feature can be felt
- Capture a GIF/video of the current feel (this becomes the baseline if adopted)
- Fill in the verdict packet on the experiment card:
  - hypothesis (copied from the thought card)
  - what was built and how to run it
  - the GIF
  - rough complexity cost of adopting this for real

## The Verdict (HUMAN GATE)

Present the packet, then **stop and ask the user: keep / iterate / kill.**

- **Forbidden:** merging anything yourself; arguing *for* keep.
- **Required:** argue the case for **kill** — devil's advocate. List the honest reasons this should not enter main: adoption cost, conflicts with existing systems, fun not carrying its complexity.

Then:

- **keep** → hand off to the landing skill (adopt flow)
- **iterate** → stay in prototype with the user's notes; update the card
- **kill** → hand off to the landing skill (graveyard flow)
