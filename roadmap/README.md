# Roadmap

This directory contains the full project roadmap, organized into sprints.
An AI agent executes each sprint by reading its definition file and working through tasks sequentially.

## How It Works

1. **You plan** — define epics, break them into sprints, break sprints into tasks
2. **AI executes** — each sprint file is a self-contained instruction set an AI can follow without external context
3. **You review** — after each sprint, verify the output before moving to the next

## Directory Structure

```
roadmap/
├── README.md              # This file
├── PLANNING.md            # How to plan sprints and write tasks (the methodology)
├── CONVENTIONS.md         # Project-specific conventions the AI must follow
├── epics/                 # High-level feature descriptions
│   ├── E001-auth.md
│   └── E002-billing.md
├── sprints/               # Sprint definitions (the executable units)
│   ├── S001-project-setup/
│   │   ├── SPRINT.md      # Sprint definition file
│   │   └── DONE.md        # Completion log (created after sprint is done)
│   ├── S002-auth-core/
│   │   ├── SPRINT.md
│   │   └── DONE.md
│   └── ...
└── backlog.md             # Unscheduled tasks and ideas
```

## Current Status

### Completed

_None yet._

### In Progress

_None yet._

### Planned

_None yet._

### Backlog

See [backlog.md](./backlog.md).
