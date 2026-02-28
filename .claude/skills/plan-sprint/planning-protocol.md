# Sprint Planning Protocol Reference

Detailed reference for the sprint planner agent.

## SPRINT.md Template

Every sprint file must follow this exact structure:

```markdown
# SXXX: Sprint Title

> Parent epic: [EXXX: Epic Title](../epics/EXXX-name.md)
> Status: `planned`

## Objective

One sentence. What is shippable after this sprint is done.

## Prerequisites

- SXXX must be completed (if applicable)
- List any external dependencies (APIs, credentials, services)

## Context

Brief technical context the AI needs. Include:
- Which packages/frameworks are already set up
- Relevant file paths and their purpose
- Architectural decisions that constrain this work
- Links to docs if a specific library version matters

Keep this to 5-15 lines. If you need more, the sprint is too big.

## Tasks

### T1: Task Title — `pending`

**Goal:** What this task produces (a file, a behavior, a passing test).

**Steps:**

- [ ] Step 1: Concrete action with exact file path.
- [ ] Step 2: Another concrete action.

**Acceptance:**

- Describe how to verify this task is done.
- Prefer commands: `pnpm test`, `pnpm typecheck`, `pnpm lint`.

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

- Branch: `sprint/SXXX-short-name`
- PR target: `main`
- PR title: `sprint(SXXX): Short description of what this sprint delivers`

## Notes

Any edge cases, gotchas, or decisions that are not obvious.
```

## Pre-flight Checklist

Before finalizing the sprint, verify all items:

- [ ] Every task has a clear, single goal
- [ ] Every step references exact file paths
- [ ] No step requires the AI to make an architectural decision
- [ ] All dependencies between tasks are reflected in task ordering
- [ ] The Context section covers everything the AI needs to know
- [ ] Code blocks are included for any non-trivial config or schema
- [ ] Acceptance criteria are verifiable with commands or specific checks
- [ ] The sprint has 3-8 tasks
- [ ] No single task will take more than 30 minutes
- [ ] The Verification section has a complete checklist
- [ ] The Delivery section specifies the branch name and PR target
- [ ] The sprint builds on the actual current state of `main`, not on assumed state

## Good vs Bad Tasks

### Good Tasks

| Task | Why it's good |
|---|---|
| "Create `libs/db/src/schema/user.ts` with a users table" | Specific file, specific artifact |
| "Add POST `/api/auth/login` that accepts email and password" | Exact route, exact behavior |
| "Write tests for the `createUser` function in `libs/db`" | Specific function, specific package |
| "Install `drizzle-orm` and `drizzle-kit` as dependencies of `libs/db`" | Exact packages, exact target |

### Bad Tasks

| Task | Why it's bad |
|---|---|
| "Set up the database" | Too vague — what tables? What config? |
| "Implement login" | No specifics — what endpoint? What validation? |
| "Add tests" | For what? Where? What behavior? |
| "Set up ORM" | Which ORM? What configuration? |

## Good vs Bad Steps

### Good Steps

```markdown
- [ ] Create file `libs/db/src/schema/user.ts`
- [ ] Define the `users` table with columns: `id` (uuid, pk, default gen_random_uuid()), `email` (text, unique, not null), `passwordHash` (text, not null), `createdAt` (timestamp, default now())
- [ ] Export the table as `usersTable`
- [ ] Add the barrel export to `libs/db/src/schema/index.ts`
```

### Bad Steps

```markdown
- [ ] Create the user schema (what fields? what types?)
- [ ] Set up everything for users (way too broad)
- [ ] Update the config (which config? what values?)
```

### Step Rules

1. Start with a verb: Create, Add, Update, Remove, Install, Run, Configure
2. Include the target: file path, function name, package name
3. Include the specifics: column types, config values, route paths
4. One action per step: don't combine "create file and add to index"

## Sprint Sizing

- 3-8 tasks per sprint
- Total work: 1-3 hours of AI execution
- Each task: 5-30 minutes
- If more than 8 tasks, split into two sprints
- If a task takes more than 30 minutes, split into multiple tasks

## Carry-over Tasks

When the previous sprint's DONE.md has `partial`, `skipped`, or `blocked` tasks:

1. Read the Feedback section of each incomplete task
2. Include carry-over tasks as the first tasks in the new sprint
3. Update the task description to account for what was already done
4. Address any blockers noted in the previous DONE.md
