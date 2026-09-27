---
name: savepoint
description: Pause and resume in-progress work with low re-entry cost. Save banks the session onto the experiment card (runnable state, stuck type, dead ends, unspoken hunch, next step) when the user stops or is stuck ("先到这", "park it"). Load restores a paused card ("继续 EXP-023", "读档") with integrity check, short briefing, main-branch time-delta, and a 15-minute restart action.
---

# Savepoint — Pause & Resume

Manages the *session* lifecycle, cutting across every other stage. Code survives a pause on its branch; what evaporates is the context in the user's head — what was tried, what was suspected. This skill banks it.

## Save flow ("先到这", "park it", user is stuck or tired)

You draft everything from the session. The user answers exactly one question.

1. Draft the Savepoint section on the experiment card:
   - **Hypothesis** — one line
   - **Runnable state** — branch, how to run, current GIF
   - **Stuck type** — `feel` (can't articulate what's wrong) / `approach` (everything tried failed) / `energy` (just tired)
   - **Dead ends** — what was tried and one-line reasons it failed. The most valuable field: it prevents re-trying the same failures next session.
   - **Next first step** — small enough to finish in 15 minutes
2. Ask the one question: **"Any unspoken hunch or suspicion in your head?"** Record the answer verbatim. An empty answer is fine; skipping the question is not.
3. Set `status: paused`, increment `pause_count`.
4. Reply with one line: where the savepoint lives.

Keep the whole ritual short — this skill is invoked at the user's most tired moment.

## Load flow ("继续 EXP-023", "读档", "what was I doing?")

If the user gives no card ID, list all paused cards with one line each: name, days parked, stuck type.

1. Read the card.
2. **Integrity check.** Does the branch exist? Does it still run? Have deps or the engine moved? If it can't run, job one is *repairing the save* — nothing else until it runs.
3. **Briefing, 3–5 sentences max.** Open with the thought card's original raw sentence — it re-lights the motivation. Then: goal, where it runs, why it got stuck, dead ends, next step. Never dump the whole file.
4. **Time-delta analysis.** `git log` since the pause date, filtered to systems this card touches: what landed in main during the pause — new infrastructure that unblocks it, or new changes that conflict with it. A card is often parked waiting for a condition that now exists.
5. **Hands back first.** Run it and let the user play for 2 minutes before any discussion. Hands remember what brains forget.
6. Propose the 15-minute restart action, framed by stuck type:
   - `feel` → go play 2–3 reference games with the question in mind before touching code
   - `approach` → reframe the problem before writing anything
   - `energy` → just do the small step
7. Set `status: active`. If `pause_count` reaches 3, force the conversation: push through this time, or demote the card back to the thoughts pool carrying all its dead ends — it returns as a battle-scarred thought, not a failure.
