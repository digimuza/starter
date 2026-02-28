# Sprint Execution Protocol Reference

Detailed reference for the sprint executor agent.

## DONE.md Template

Create this file in the sprint directory after all tasks are complete:

```markdown
# SXXX: Sprint Title — Completed

**Date:** YYYY-MM-DD
**PR:** #<number>
**Sprint status:** completed | partial | abandoned

## Task Summary

| Task | Title                | Status  | Notes                  |
| ---- | -------------------- | ------- | ---------------------- |
| T1   | Task title           | done    |                        |
| T2   | Task title           | done    |                        |
| T3   | Task title           | partial | See details below      |

## What Was Done

One paragraph summarizing the actual work completed.

## What Was NOT Done

List anything planned but not delivered, with reasons:
- T3 partial: explanation of what's missing and why

## Deviations From Plan

Any changes from the original sprint definition and why they happened:
- Changed X because Y

## Problems Encountered

Technical issues, bugs, or unexpected behavior found during execution:
- Description of problem, how it was handled

## Decisions Made

Any judgment calls that were not covered by the plan:
- Decision and reasoning

## Recommendations for Next Sprint

Actionable items the planner should consider:
- Carry over T3 remaining work
- Consider refactoring X before adding Y

## Files Changed

- `path/to/file.ts` — description of change
```

## Commit Message Format

Use conventional commits with the sprint ID as scope:

| Scenario | Format |
|---|---|
| Task completed | `feat(SXXX): T<N> — <task title>` |
| Task partial | `feat(SXXX): T<N> — <task title> (partial)` |
| Task skipped/blocked | `chore(SXXX): T<N> — <task title> (skipped)` |
| Sprint start | `chore: start sprint SXXX` |
| Lint fixes | `chore(SXXX): fix lint errors` |
| Type fixes | `fix(SXXX): fix type errors` |
| Test fixes | `fix(SXXX): fix failing tests` |
| DONE.md + final status | `docs(SXXX): add DONE.md and set status in-review` |

Use `feat:` for new features, `fix:` for bug fixes, `refactor:` for restructuring, `test:` for test-only changes, `docs:` for documentation. Default to `feat:` for tasks that add new code.

## PR Body Template

```markdown
## Summary

Sprint **SXXX: <Sprint Title>** from epic [EXXX: Epic Title](link).

### Tasks

| Task | Title | Status |
|------|-------|--------|
| T1 | Title | done |
| T2 | Title | done |
| T3 | Title | partial |

### What Changed

- Brief bullet points of key changes

### Deviations

- Any deviations from the sprint plan (or "None")

### Checks

- [x] `pnpm lint` passes
- [x] `pnpm typecheck` passes
- [x] `pnpm test` passes
```

## Task Status Decision Tree

After executing a task's steps and running acceptance:

1. **All acceptance criteria pass** → status: `done`
2. **Some steps completed, some acceptance criteria fail after 2 fix attempts** → status: `partial`
   - Document what works and what doesn't in Feedback
3. **Task depends on external resource that's unavailable** → status: `blocked`
   - Document the blocker in Feedback
4. **Task is superseded or no longer relevant** → status: `skipped`
   - Document the reason in Feedback

## Error Recovery

1. **Step fails:** Try to fix the issue. Max 2 fix attempts per step.
2. **Acceptance fails:** Try to fix. Max 2 attempts. If still failing, mark task `partial`.
3. **Lint/typecheck/test fails in verification:** Fix issues, commit fixes separately.
4. **Git push fails:** Check if branch exists remotely. If so, try `git push --force-with-lease`.
5. **Cannot create PR:** Ensure branch is pushed. Check `gh auth status`.
6. **Everything is broken:** Mark remaining tasks as `blocked`, create DONE.md documenting the situation, push and open PR with what you have.

Never abandon the sprint. Always deliver something.
