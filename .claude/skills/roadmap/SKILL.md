---
context: fork
agent: roadmap-planner
disable-model-invocation: true
argument-hint: [product direction or feature idea]
---

# /roadmap — Plan the Product Roadmap

Think strategically about what to build, define epics, and set product direction.

## User Input

$ARGUMENTS

## Instructions

Act as a product strategist. Analyze the current state of the codebase and roadmap, then define or update the product direction:

1. **Understand** — read the README, existing epics, backlog, completed sprints, and survey the codebase
2. **Assess** — what exists, what's planned, what's missing, what's in the backlog
3. **Strategize** — prioritize by user value, technical foundation, effort vs impact, dependencies, and risk
4. **Define epics** — create or update epic files in `roadmap/epics/` following the template
5. **Update roadmap** — update `roadmap/backlog.md` and `roadmap/README.md`
6. **Present** — output a summary of the product direction, epics, and execution order

If the user provided input above, use it as the primary direction. Otherwise, determine the best path forward based on what you find.

Refer to `roadmap-protocol.md` in this skill directory for the epic template, prioritization framework, and examples.
