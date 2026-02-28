# Roadmap Planning Protocol Reference

Detailed reference for the roadmap planner agent.

## Epic Template

Every epic file must follow this structure. Save to `roadmap/epics/EXXX-short-name.md`:

```markdown
# EXXX: Epic Title

## Goal

One sentence describing the end-user outcome.

## Why

Why this epic matters. What problem it solves. Who benefits.

## Success Criteria

- [ ] Criterion 1 (observable, testable — describes what a user can do)
- [ ] Criterion 2
- [ ] Criterion 3

## Sprints

| Sprint | Title              | Status  | PR   |
| ------ | ------------------ | ------- | ---- |
| S001   | Sprint title here  | planned |      |
| S002   | Sprint title here  | planned |      |

## Open Questions

Things that must be decided before sprint work begins.

## Out of Scope

What this epic explicitly does NOT include. This prevents scope creep.
```

## Epic Rules

- Keep them short — a few paragraphs, not pages
- Success criteria must be **observable**: "the user can log in with email/password", not "auth works"
- List sprints in dependency order — earlier sprints must not depend on later ones
- 2-6 sprints per epic. More than 6? Split into two epics
- Number epics sequentially: E001, E002, E003...
- Include "Out of Scope" — this is critical for preventing feature creep

## Prioritization Framework

When deciding what to build next, score each potential epic:

### 1. User Value (High / Medium / Low)

- **High:** Core functionality users expect. The product is broken without it.
- **Medium:** Enhances the experience. Users would appreciate it but can work around it.
- **Low:** Nice to have. Polishes edges.

### 2. Technical Foundation (Blocker / Enabler / Independent)

- **Blocker:** Must exist before other epics can start. Database, auth, core infra.
- **Enabler:** Makes future work faster or better. Shared libraries, CI/CD, testing infra.
- **Independent:** Can be built in any order.

### 3. Effort (Small / Medium / Large)

- **Small:** 1-2 sprints. Can be done in a day.
- **Medium:** 3-4 sprints. A week of work.
- **Large:** 5-6 sprints. Multiple weeks.

### Priority Order

1. High value + Blocker → do first, always
2. High value + Small effort → quick wins, do early
3. Medium value + Enabler → invest early for compound returns
4. High value + Large effort → plan carefully, break into phases
5. Low value + anything → backlog until higher-priority work is done

## Roadmap README Update

When updating `roadmap/README.md`, maintain this structure in the Current Status section:

```markdown
## Current Status

### Completed

| Epic | Title | Sprints |
|------|-------|---------|
| E001 | Title | S001-S003 |

### In Progress

| Epic | Title | Current Sprint |
|------|-------|----------------|
| E002 | Title | S004 |

### Planned

| Epic | Title | Priority | Est. Sprints |
|------|-------|----------|--------------|
| E003 | Title | High | 3 |
| E004 | Title | Medium | 2 |

### Backlog

See [backlog.md](./backlog.md).
```

## Backlog Management

The backlog (`roadmap/backlog.md`) is a living document. When planning:

- **Promote:** Move items from backlog into epics when they're ready to be shaped
- **Add:** New ideas discovered during analysis go into the backlog
- **Remove:** Items that are no longer relevant get deleted
- **Clarify:** Vague items should be refined or split

Structure the backlog with sections:

```markdown
# Backlog

## Ideas

Rough ideas that need more thought before becoming epics.

- Idea description

## Unscheduled Tasks

Concrete tasks that don't belong to any epic yet.

- Task description
```

## Anti-patterns

Avoid these common roadmap mistakes:

- **Everything is high priority** — if everything is important, nothing is. Force-rank.
- **Epics without success criteria** — "improve performance" is not an epic. What does the user see?
- **Too many epics at once** — 2-4 active/planned epics max. Beyond that is fiction.
- **Planning implementation in epics** — epics say WHAT and WHY. Sprints say HOW.
- **Ignoring what exists** — always start from the actual codebase, not from wishes.
- **Scope creep via "while we're at it"** — the Out of Scope section exists for a reason.
