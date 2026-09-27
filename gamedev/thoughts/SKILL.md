---
name: thoughts
description: Idea incubator for indie game dev. Captures raw ideas with zero friction, grows them into testable hypotheses, surfaces ripe ones for prototyping. Use when the user drops an idea ("记一下", "what if we..."), fleshes out a card ("琢磨一下 T-012"), asks what's ripe ("有什么能做了"), or when a standing instruction asks to scan the pool before touching a game system.
---

# Thoughts — Idea Incubator

A holding pool where raw game ideas live until they are ripe enough to prototype. One file per idea in `thoughts/`, named `T-<number>.md`.

## Constitution (applies to every workflow)

1. **Zero-friction capture.** Recording an idea costs the user seconds. Never ask questions at capture time.
2. **The original sentence is read-only.** Never edit, polish, or translate the user's raw wording in the quote line. Add structure below it, never inside it.
3. **Gardener, not judge.** You may assess *testability*. Never rate, rank, or dismiss an idea's worth, and never archive or delete a thought on your own.
4. **Human gates.** Only the user promotes a thought to prototype, and only the user kills one.

## Card format

```markdown
---
id: T-012
status: seed | sprouting | ripe
created: YYYY-MM-DD
updated: YYYY-MM-DD
links: [T-007, EXP-003]   # related cards, optional
---

> The user's original sentence, verbatim. Never edited.

## Hypothesis          # required to reach "ripe"
If <change>, then <expected player experience>. Verify by <observable check>.

## Slice               # required to reach "ripe": smallest touchable version, <= 2h to build

## Blockers            # optional: what this depends on that doesn't exist yet

## Notes               # optional: everything else
```

## Maturity ladder

- **seed** — raw sentence only. May stay here forever; that is not failure.
- **sprouting** — has connections (related systems/cards), blockers, or notes.
- **ripe** — has both Hypothesis and Slice filled. Only ripe cards may enter the prototype skill.

## Entry points

Route by user intent, then read the matching reference file:

- **Capture** — user drops a raw idea ("记一下：敌人死亡爆金币", "note this", "what if...") → read `references/capture.md`
- **Develop** — user wants to flesh out a card ("琢磨一下 T-012", "develop this idea") → read `references/develop.md`
- **Harvest** — user asks what's ready ("有什么能做了", "what's ripe") → read `references/harvest.md`

## Proactive surfacing (push mode)

The pool's worst failure mode is write-only: ideas go in and are never seen again. The fix is context-triggered surfacing, driven by a standing instruction in the project's `AGENTS.md` (or equivalent always-loaded file). When setting up the pool for the first time, offer to append this line:

> This repo has a thoughts pool at `thoughts/`. Before changing a game system, scan it for related cards and mention up to 3 in one line.

When this instruction is present and you are about to modify a game system: scan `thoughts/` for related cards, mention at most 3 in a single line, then stop. Never interrupt with more.
