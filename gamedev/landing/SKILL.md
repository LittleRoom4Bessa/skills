---
name: landing
description: Executes a prototype verdict. Keep = rewrite into production quality on a fresh branch (exp code never merges), preserving feel parameters, ending in a human feel-acceptance gate. Kill = archive to graveyard with a required cause of death linked to the source idea. Use when the user adopts ("进 main", "转正") or kills ("砍掉", "kill it") a prototype.
---

# Landing — Adopt or Bury

Executes the verdict on an experiment card. Both outcomes are normal, healthy outcomes.

## Adopt flow (verdict: keep)

**Hard rule: prototype code never enters main.** Close the exp branch unmerged (tag it `exp/<slug>` for archaeology) and re-implement the feature cleanly on a fresh branch.
**Size waiver:** if the whole change is < 50 lines and touches no core system, cleaning it in place and merging directly is allowed.
**Large adoptions:** if the rewrite spans multiple sessions or touches several systems, hand off to the `openspec-propose` skill before the rewrite: create a change carrying the verdict packet (validated hypothesis, baseline GIF, do-not-change list), then implement through the OpenSpec flow. Steps 1–2 and the feel-acceptance gate below still belong to this skill.

Procedure:

1. **Archive the feel first.** Before touching any code: save the baseline GIF from the verdict packet, and extract the magic numbers (timings, curves, values) into a "do not change" list. Refactoring kills juice — this list is the antidote.
2. **Inventory.** Separate *soul* (feel parameters, timing, the core interaction) from *scaffolding* (temp input, hacked scenes). Scaffolding is discarded, never ported.
3. **Rewrite** the soul into main's architecture: config instead of hardcoding, project event system, naming conventions, edge cases.
4. **Regression check:** framerate, conflicts with existing systems, unhappy paths the prototype never handled.
5. **Independent review — three lanes, parallel.** The rewrite is production code; author self-review has blind spots. Pin the fixed point first (`git diff main...HEAD`, three-dot against the merge-base; confirm the ref resolves and the diff is non-empty). Then run the three lanes below as fresh-eyes reviews — separate sub-agents/forked contexts when available, so the lanes don't pollute each other. Each report ≤ 400 words, every finding quoted against the diff. Aggregate side by side; **never rerank across lanes** — a failing lane must not be masked by a passing one. Verify every finding against the code; fix before the feel gate so the human plays the final build.
   - **Standards** — project conventions (AGENTS.md: GDScript-first, minimal, no speculative abstraction) plus the smell baseline: Mysterious Name / Duplicated Code / Feature Envy / Data Clumps / Primitive Obsession / Repeated Switches / Shotgun Surgery / Divergent Change / Speculative Generality / Message Chains / Middle Man / Refused Bequest. Two rules bind the baseline: documented repo standards override it, and its findings are always judgement calls, never hard violations. Skip anything tooling enforces.
   - **Fidelity** — every entry in the do-not-change list preserved verbatim; nothing from the verdict packet silently dropped; no scope creep beyond the packet.
   - **Correctness** — logic bugs (not style), edge cases the playtest never hit, GDScript lifecycle traps: timers, awaits, and signals on nodes that can be freed mid-flight (the EXP-002 time_scale freeze is the canonical example).
6. **Feel acceptance (HUMAN GATE).** The user plays the clean build against the baseline GIF: "Is the taste still there?" If not, return to step 3. Never self-certify feel — you can verify code correctness, not taste.
7. Open the PR referencing the exp branch. Set the card `status: merged` and record the PR under Outcome. Also update the source thought card (`from:`): set `status: landed` — the idea has shipped.

## Graveyard flow (verdict: kill)

1. Archive the branch: tag it, don't delete it.
2. Record the **cause of death** on the experiment card — required, never empty. One honest line: "feel too floaty", "conflicts with stealth", "fun doesn't carry the complexity".
3. Move the card to `experiments/graveyard/`, set `status: graveyard`. Do the graveyard bookkeeping where cards live — on main or a branch headed there, never stranded on the exp branch.
4. Return to the source thought card: link the graveyard entry and its cause. The *idea* is not dead — this *attempt* is. The thought goes back to the pool carrying its epitaph, richer than before.
5. Tell the user in one line. No ceremony — killing an experiment cheaply is the system working as designed.
