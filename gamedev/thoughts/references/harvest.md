# Harvest

Show the user what the pool can offer right now.

## Pull mode ("有什么能做了？", "what's ripe?")

1. List all **ripe** thought cards, each with a one-line reason why it is cheap to test *now*.
2. If nothing is ripe, list **sprouting** cards with what each one is missing ("T-009 needs: a slice smaller than the whole combat system").
3. Also check `experiments/` for cards with `status: paused` older than 14 days: "EXP-023 has been parked for 20 days — resume it or kill it?" A stalled experiment rots just like a forgotten idea.
4. Keep the whole reply short. This is a menu, not a report.

## Push mode (triggered by the project's standing instruction)

When you are about to modify a game system and the standing instruction is present:

1. Scan `thoughts/` for cards related to that system.
2. Mention at most 3, in a single line: "Parked cards touching combat feel: T-004, T-011 — worth a look?"
3. Then stop. Never expand unless the user asks.
