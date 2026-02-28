# Planning Methodology

How to plan, structure, and write sprint files that an AI agent can execute reliably.

---

## Core Principles

### Self-Contained Sprints

Every sprint file must be **self-contained**. The AI agent reading it should never need to search for context, guess at intent, or make architectural decisions. All decisions are made during planning, not during execution.

### Iterative Development From Current State

Sprints are planned **iteratively, starting from what exists right now**. You do not plan the entire project upfront. Instead:

1. **Assess the current state** of the codebase — what's built, what's working, what's missing.
2. **Plan the next 1–3 sprints** based on what exists today.
3. **Execute one sprint**, review the result.
4. **Re-assess** and plan the next batch of sprints from the new state.

This is critical because:
- AI execution may deviate from the plan. Later sprints must account for what actually happened, not what was planned.
- Requirements evolve. Discoveries during one sprint inform the next.
- Planning too far ahead creates waste — detailed plans for sprint 20 are fiction when sprint 3 hasn't run yet.

**Rule: Never plan more than 3 sprints ahead in detail.** You can have a rough epic-level roadmap, but detailed sprint files should only exist for the immediate next batch.

### One Sprint = One Pull Request

Every sprint must end with a **pull request to `main`**. This is non-negotiable.

- Every sprint branch **must be created from `main`**. Always pull the latest `main` before starting.
- The AI creates a branch (`sprint/S001-short-name`), does all work there, then opens a PR.
- The PR is the review checkpoint. Nothing merges without human review.
- Each PR must pass all checks (`pnpm lint`, `pnpm typecheck`, `pnpm test`) before merge.
- The next sprint starts from `main` after the previous sprint's PR is merged.
- If a sprint's PR is rejected or needs changes, those changes happen on the same branch before merge — not in a new sprint.
- Never branch from another sprint branch. Always from `main`.

This ensures:
- Every sprint produces a reviewable, mergeable unit of work.
- `main` is always in a working state.
- There's a clear audit trail of what each sprint changed.

---

## 1. Hierarchy

```
Epic → Sprint → Task → Step
```

| Level    | Purpose                          | Scope                    | File                        |
| -------- | -------------------------------- | ------------------------ | --------------------------- |
| **Epic** | A major feature or system        | Weeks to months          | `epics/E001-name.md`       |
| **Sprint** | A shippable slice of an epic   | 1–3 hours of AI work     | `sprints/S001-name/SPRINT.md` |
| **Task** | One logical unit of work         | 5–30 minutes of AI work  | Section inside SPRINT.md    |
| **Step** | One concrete action              | A single tool call       | Checklist item inside task  |

---

## 2. Epics

An epic describes **what** and **why** at a high level. It does NOT describe implementation details — those belong in sprint files.

### Epic Template

```markdown
# E001: Epic Title

## Goal

One sentence describing the end-user outcome.

## Why

Why this epic matters. What problem it solves.

## Success Criteria

- [ ] Criterion 1 (observable, testable)
- [ ] Criterion 2

## Sprints

| Sprint | Title              | Status    | PR   |
| ------ | ------------------ | --------- | ---- |
| S001   | Sprint title here  | completed | #12  |
| S002   | Sprint title here  | in-review | #15  |
| S003   | Sprint title here  | planned   |      |

## Open Questions

Things that must be decided before sprint work begins.

## Out of Scope

What this epic explicitly does NOT include.
```

### Rules for Epics

- Keep them short. A few paragraphs, not pages.
- Success criteria must be observable — "the user can log in with email/password", not "auth works".
- List sprints in dependency order. Earlier sprints must not depend on later ones.

---

## 3. Sprints

A sprint is the **executable unit**. When you hand a sprint file to an AI agent, it should be able to complete all tasks without asking questions.

### Sprint Sizing

- A sprint should contain **3–8 tasks**.
- Total work should take an AI agent **1–3 hours**.
- If a sprint has more than 8 tasks, split it into two sprints.
- If a task takes more than 30 minutes, split it into multiple tasks.

### Sprint Template

```markdown
# S001: Sprint Title

> Parent epic: [E001: Epic Title](../epics/E001-name.md)
> Status: `planned`

## Objective

One sentence. What is shippable after this sprint is done.

## Prerequisites

- S000 must be completed (if applicable)
- List any external dependencies (APIs, credentials, services)

## Context

Brief technical context the AI needs. Include:
- Which packages/frameworks are already set up
- Relevant file paths and their purpose
- Architectural decisions that constrain this work
- Links to docs if a specific library version matters

Keep this to 5–15 lines. If you need more, the sprint is too big.

## Tasks

### T1: Task Title — `pending`

**Goal:** What this task produces (a file, a behavior, a passing test).

**Steps:**

- [ ] Step 1: Concrete action. Include the exact file path, function name, or command.
- [ ] Step 2: Another concrete action.
- [ ] Step 3: ...

**Acceptance:**

- Describe how to verify this task is done.
- Prefer commands: `pnpm test`, `pnpm typecheck`, `pnpm lint`.
- If no automated check exists, describe what to manually verify.

**Feedback:**

_Filled in by AI after execution. Leave blank during planning._

---

### T2: Task Title — `pending`

**Goal:** ...

**Steps:**

- [ ] ...

**Acceptance:**

- ...

**Feedback:**

_Filled in by AI after execution. Leave blank during planning._

---

(repeat for each task)

## Verification

How to verify the entire sprint is complete:

- [ ] All tasks checked off
- [ ] `pnpm lint` passes
- [ ] `pnpm typecheck` passes
- [ ] `pnpm test` passes
- [ ] Brief manual smoke test description (if applicable)

## Delivery

- Branch: `sprint/S001-short-name`
- PR target: `main`
- PR title: `sprint(S001): Short description of what this sprint delivers`

## Notes

Any edge cases, gotchas, or decisions that are not obvious.
```

### Sprint Statuses

The sprint status (in the header) tracks the overall sprint lifecycle:

| Status | Meaning |
|--------|---------|
| `planned` | Sprint is defined but work has not started |
| `in-progress` | AI is actively working on this sprint |
| `in-review` | PR is open, waiting for human review |
| `changes-requested` | PR was reviewed, changes are needed |
| `completed` | PR merged into `main` |
| `abandoned` | Sprint was cancelled or replaced |

### Task Statuses

Each task has its own status (in the task heading) updated by the AI during execution:

| Status | Meaning |
|--------|---------|
| `pending` | Not started yet |
| `in-progress` | AI is currently working on this task |
| `done` | Task completed, acceptance criteria met |
| `partial` | Task partially completed — see Feedback for details |
| `skipped` | Task was intentionally skipped — see Feedback for reason |
| `blocked` | Task could not be completed due to an external dependency |

### Task Feedback

Every task has a **Feedback** section. The AI fills this in after working on the task. It must include:

- **What was actually done** — concrete description of changes made.
- **What was not done** — anything from the steps that was skipped or deferred, and why.
- **Problems encountered** — errors, unexpected behavior, missing dependencies.
- **Decisions made** — any judgment calls the AI had to make despite planning (ideally none, but reality happens).
- **Notes for next sprint** — anything the planner should know when writing the next sprint.

If the task completed cleanly with no issues, a one-liner is fine: "Completed as planned. No issues."

### Rules for Sprints

1. **No ambiguity.** Every task has one clear interpretation.
2. **No decisions required.** The AI does not choose between approaches — you already chose.
3. **Ordered by dependency.** T1 before T2 if T2 depends on T1's output.
4. **Self-contained context.** Don't say "see the auth module" — say "see `libs/shared/src/auth.ts`".
5. **Explicit file paths.** Always use paths relative to the monorepo root.
6. **Specify behavior, not just structure.** Not "create a user model" but "create a user model with fields: id (uuid, primary key), email (string, unique, not null), ..."

---

## 4. Tasks

A task is one logical unit of work. It produces a concrete, verifiable artifact.

### What Makes a Good Task

| Good                                                         | Bad                                          |
| ------------------------------------------------------------ | -------------------------------------------- |
| "Create `libs/db/src/schema/user.ts` with a users table"    | "Set up the database"                        |
| "Add POST `/api/auth/login` that accepts email and password" | "Implement login"                            |
| "Write tests for the `createUser` function in `libs/db`"    | "Add tests"                                  |
| "Install `drizzle-orm` and `drizzle-kit` as dependencies of `libs/db`" | "Set up ORM"               |

### Task Granularity Rules

1. **One concern per task.** A task does not both create a schema AND write an API endpoint.
2. **Explicit inputs and outputs.** State what exists before the task and what exists after.
3. **Include the "what", skip the "how" if obvious.** If the step is "install a package", you don't need to explain `pnpm add`. But if there's a non-obvious configuration step, include it.
4. **Include exact values for anything non-trivial.** Table names, column types, route paths, environment variable names, validation rules, error messages.

### Task Size Guide

| Too small (merge up)        | Right size                        | Too big (split)                    |
| --------------------------- | --------------------------------- | ---------------------------------- |
| "Create a file"             | "Create user schema with fields"  | "Create all database schemas"      |
| "Add one import"            | "Add auth middleware to API routes"| "Implement full auth system"       |
| "Fix a typo"                | "Add input validation to signup"  | "Add validation to all forms"      |

---

## 5. Steps

A step is a single concrete action. It maps roughly to one tool call or one small code change.

### Writing Steps

```markdown
# Good steps:

- [ ] Create file `libs/db/src/schema/user.ts`
- [ ] Define the `users` table with columns: `id` (uuid, pk, default gen_random_uuid()), `email` (text, unique, not null), `passwordHash` (text, not null), `createdAt` (timestamp, default now())
- [ ] Export the table as `usersTable`
- [ ] Add the barrel export to `libs/db/src/schema/index.ts`

# Bad steps:

- [ ] Create the user schema (too vague — what fields? what types?)
- [ ] Set up everything for users (way too broad)
```

### Step Rules

1. **Start with a verb.** Create, Add, Update, Remove, Install, Run, Configure.
2. **Include the target.** File path, function name, package name.
3. **Include the specifics.** Column types, config values, route paths.
4. **One action per step.** Don't combine "create file and add to index".

---

## 6. Writing Context That AI Can Parse

### Do

- Use exact file paths: `apps/web/src/app/login/page.tsx`
- Use exact package names: `drizzle-orm@0.38`
- Use exact values: `NEXT_PUBLIC_API_URL`, `users`, `email`
- Use code blocks for any config, schema, or code snippet the AI should reproduce exactly
- Reference specific versions when they matter

### Don't

- Use pronouns without clear antecedents: "update it" (update what?)
- Use vague locations: "in the shared lib" (which file?)
- Assume knowledge: "use our standard pattern" (what pattern? show it or link to CONVENTIONS.md)
- Mix concerns: don't put API design decisions inside a database task

### Inline Code Blocks

When the AI must produce specific code (config files, schemas, exact type signatures), include it directly in the step:

````markdown
- [ ] Create `drizzle.config.ts` in `libs/db/` with:

```typescript
import { defineConfig } from "drizzle-kit";

export default defineConfig({
  schema: "./src/schema/index.ts",
  out: "./drizzle",
  dialect: "postgresql",
  dbCredentials: {
    url: process.env.DATABASE_URL!,
  },
});
```
````

This removes all ambiguity about what the file should contain.

---

## 7. Sprint Delivery

Every sprint ends with a pull request. The AI agent must follow this sequence:

**Before starting work:**

1. **Checkout `main`** and pull latest (`git checkout main && git pull`).
2. **Create branch** from `main` (`git checkout -b sprint/S001-short-name`).
3. **Update sprint status** — set the sprint status in SPRINT.md to `in-progress`.

**During execution (after each task):**

1. **Update task status** — change the task heading from `pending` to `done`, `partial`, `skipped`, or `blocked`.
2. **Fill in Feedback** — write what was done, what wasn't, problems, decisions.
3. **Check off steps** — mark completed step checkboxes in the task.

**After all tasks are complete:**

1. **Verify** — run all checks (`pnpm lint`, `pnpm typecheck`, `pnpm test`).
2. **Update sprint status** — set to `in-review` in SPRINT.md.
3. **Commit** — all changes on the sprint branch with clean, atomic commits.
4. **Push** — push the branch to origin.
5. **Open PR** — create a pull request targeting `main` with:
   - Title: `sprint(SXXX): Short description`
   - Body: summary of what changed, list of tasks completed with their statuses, any deviations from plan.
6. **Create DONE.md** — log what happened (see below).
7. **Stop** — wait for human review. Do not start the next sprint.

### DONE.md Template

When a sprint is finished, create a `DONE.md` in the sprint directory:

```markdown
# S001: Sprint Title — Completed

**Date:** YYYY-MM-DD
**PR:** #<number> (link to pull request)
**Sprint status:** completed | partial | abandoned

## Task Summary

| Task | Title                | Status  | Notes                  |
| ---- | -------------------- | ------- | ---------------------- |
| T1   | Task title           | done    |                        |
| T2   | Task title           | done    |                        |
| T3   | Task title           | partial | See details below      |
| T4   | Task title           | skipped | Blocked by X           |

## What Was Done

One paragraph summarizing the actual work completed.

## What Was NOT Done

List anything planned but not delivered, with reasons:
- T3 partial: explanation of what's missing and why
- T4 skipped: explanation of the blocker

## Deviations From Plan

Any changes from the original sprint definition and why they happened:
- Changed X because Y
- Added unplanned task Z because it was required by T2

## Problems Encountered

Technical issues, bugs, or unexpected behavior found during execution:
- Description of problem, how it was handled (or not)

## Decisions Made

Any judgment calls the AI had to make that were not covered by the plan:
- Decision and reasoning

## Recommendations for Next Sprint

Actionable items the planner should consider:
- Carry over T3 remaining work
- T4 blocker needs to be resolved first
- Consider refactoring X before adding Y

## Files Changed

- `path/to/file.ts` — description of change
- `path/to/other.ts` — description of change
```

This log is the primary input for planning the next sprint. Read it carefully before writing the next sprint file.

---

## 8. The Iterative Planning Workflow

This is the process you follow throughout the project lifecycle:

### First Time

1. Assess the current state of the codebase.
2. Define 1–3 epics at a high level.
3. Write detailed sprint files for the first 1–3 sprints only.
4. Hand sprint S001 to the AI.

### After Each Sprint

1. Review the PR. Merge or request changes.
2. If changes requested: update sprint status to `changes-requested`. AI fixes on the same branch.
3. If approved: merge PR, update sprint status to `completed` in SPRINT.md, update the epic's sprint table.
4. Read the DONE.md. Note any deviations, partial tasks, or issues.
5. Re-assess: has the current state changed what you planned next?
6. Carry over any `partial`, `skipped`, or `blocked` tasks into the next sprint.
7. Update or create the next sprint file, accounting for:
   - What actually got built (not what was planned)
   - New information discovered during the sprint
   - Recommendations from DONE.md
   - Any priority changes
8. Hand the next sprint to the AI.

### Planning Rules

- **Plan from reality, not from plans.** Always check the actual codebase state before writing the next sprint.
- **3-sprint horizon.** Have at most 3 detailed sprints ahead. Beyond that, keep it at the epic level.
- **Sprints are sequential.** Never run two sprints in parallel. Sprint N+1 starts from the merged state of sprint N.
- **Epics can be re-ordered.** If discoveries during sprint execution change priorities, update the epic order.
- **The backlog is living.** Move items in and out of `backlog.md` as understanding grows.

---

## 9. Checklist: Before Handing a Sprint to AI

Use this checklist before marking a sprint as ready:

- [ ] Every task has a clear, single goal
- [ ] Every step references exact file paths
- [ ] No step requires the AI to make an architectural decision
- [ ] All dependencies between tasks are reflected in task ordering
- [ ] The Context section covers everything the AI needs to know
- [ ] Code blocks are included for any non-trivial config or schema
- [ ] Acceptance criteria are verifiable with commands or specific checks
- [ ] The sprint has 3–8 tasks
- [ ] No single task will take more than 30 minutes
- [ ] The Verification section has a complete checklist
- [ ] The Delivery section specifies the branch name and PR target
- [ ] The sprint builds on the actual current state of `main`, not on assumed state
