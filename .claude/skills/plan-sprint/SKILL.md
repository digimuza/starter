---
context: fork
agent: sprint-planner
disable-model-invocation: true
argument-hint: [epic-reference]
---

# /plan-sprint — Plan the Next Sprint

Analyze the current codebase state, previous sprint results, and backlog to draft the next SPRINT.md.

## Epic Reference (optional)

$ARGUMENTS

## Instructions

Plan the next sprint by following the planning protocol:

1. **Gather context** — read `roadmap/PLANNING.md`, `roadmap/CONVENTIONS.md`, `roadmap/backlog.md`, epic files in `roadmap/epics/`, latest DONE.md files in `roadmap/sprints/`, and explore the current codebase structure
2. **Determine scope** — next sprint number, which epic, carry-over tasks from previous sprints, 3-8 new tasks
3. **Draft SPRINT.md** — following the exact template from PLANNING.md §3, with explicit file paths and code blocks for every task
4. **Validate** — run through the checklist from PLANNING.md §9
5. **Present for review** — write the file and output a summary. Do NOT execute the sprint.

If an epic reference is provided above, focus the sprint on that epic. Otherwise, determine the next logical epic based on dependency order and previous sprint results.

Refer to `planning-protocol.md` in this skill directory for the exact SPRINT.md template, pre-flight checklist, and examples of good vs bad tasks.
