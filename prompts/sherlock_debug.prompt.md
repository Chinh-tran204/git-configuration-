---
agent: 'sherlock'
description: 'Debug a specific bug and identify root cause'
---
Use debugging.skill.md
## Task
Debug: ${input:task} 
Identify root cause, execution flow, affected areas, and fix (if applicable)

## Context Boundaries
- If input provided: use it directly
- If not: ask for specific bug details
then:
- Read: planning_log (source of truth)
- Read: change_log (execution history)
- Scope: task-specific files and dependencies
- do NOT modify `.github/utility/linking/planning_log/` and `.github/utility/linking/SOT/` (READ-ONLY)

## Constraints
- do NOT modify planning_log
- do NOT speculate beyond available context
- follow existing trace only

## Output
- **status**: COMPLETED in change_log when done
- print out STATUS: <state> | NEXT_ACTION: <step>