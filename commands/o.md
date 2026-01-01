---
name: o
description: Enter orchestrate mode for feature development
---

# /o Command

Enter orchestrate mode. Claude becomes engineer manager, delegates to agents.

## Usage

| Command | Action |
|---------|--------|
| `/o status` | Show current session state |
| `/o proceed` | Execute next task |
| `/o verify` | Quality check |
| `/o end` | End Orchestrate session |

## On Trigger
1. Follow Orchestrate Mode workflow from CLAUDE.md
2. All subsequent messages route through orchestrator until `/o end`

## Context Structure
```
.context/{session_name}/
├── meta.md          # session info (all read)
├── requirements.md  # what user wants
├── research.md      # codebase findings
├── architecture.md  # design decisions
├── plan.md          # tasks
├── implementation.md # changes made
├── verification.md  # review results
└── history.md       # action log
```

## Invalid/Empty Command
```
Usage: /o <command>

Commands:
  status      Current session state
  proceed     Execute next task
  verify      Quality check
  end         Finish session
```
