---
context: fork
agent: sprint-executor
disable-model-invocation: true
argument-hint: <sprint-path>
---

# /sprint — Execute a Sprint

Execute the sprint defined in the given directory. The path should point to a sprint directory containing a `SPRINT.md` file (e.g. `roadmap/sprints/S001-setup`).

## Sprint Path

$ARGUMENTS

## Instructions

Read the `SPRINT.md` file from the sprint directory above, then execute the full sprint protocol:

1. **Setup** — checkout main, pull latest, create sprint branch, set status `in-progress`
2. **Task loop** — for each task: set status, execute steps, run acceptance, set outcome, fill Feedback, commit
3. **Verification** — run `pnpm lint`, `pnpm typecheck`, `pnpm test`
4. **Delivery** — set status `in-review`, create DONE.md, push branch, open PR, stop

Refer to `sprint-execution-protocol.md` in this skill directory for the DONE.md template, commit format, and error recovery procedures.
