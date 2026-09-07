# Project instructions for Claude

## Automation policy
Do not run commands, edit files, or make changes in this project without explicit permission first. Give step-by-step instructions for the user to execute manually, then wait for them to report back before continuing. Only take direct action when the user explicitly asks for an exception in that specific request — an exception granted once does not carry over to later requests.

## Reply format
When walking through a structured, multi-step task (e.g. a phased plan), prefix each reply with a bracketed tag indicating its purpose:

- `[PHASE X STEP X - INSTRUCTION]` — next-step guidance for the user to execute
- `[PHASE X STEP X - TROUBLESHOOTING]` — diagnosing or fixing something that went wrong
- `[PHASE X STEP X - VERIFICATION]` — confirming or checking that something worked
- `[PHASE X STEP X - NOTE]` — a clarification or aside that isn't a new action step
- `[PHASE X STEP X - RECOMMENDATION]` — advisory input where multiple approaches exist, not a prescribed step
- `[PHASE X STEP X - RECAP]` — summarizing progress or what's been completed so far
- `[PHASE X STEP X - DECISION NEEDED]` — flagging a fork in the road that requires the user's choice before continuing

For non-phased conversation, the `PHASE X STEP X` portion can be omitted — just use the bracketed state name on its own, e.g. `[NOTE]`, `[RECOMMENDATION]`.

## docs/sessions/ convention
Each work session gets a pair of files, numbered sequentially: `plan_N.md` and `note_N.md`.

- **`plan_N.md`** — the plan going into the session (what was intended to be done).
- **`note_N.md`** — written at the end of a session. Contains **decisions not included in the original plan.**