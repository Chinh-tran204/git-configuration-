---
agent: 'sherlock'
description: 'Deep investigation and analysis of a topic/module'
---
Use investigate.skill.md

## Task
Investigate: ${input:task:topic or module}
Analyze structure, relationships, and implementation details

## Context Boundaries
- have to have context of what to investigate (topic/module), if not, STOP and ask for details
- Read: planning_log (source of truth)
- Read: change_log (execution history)
- Scope: task-specific files and dependencies only
- do NOT modify `.github/utility/linking/planning_log/` and `.github/utility/linking/SOT/` (READ-ONLY)

## Constraints
- do NOT modify planning_log
- do NOT scan entire repo unnecessarily
- do NOT go beyond relevant scope

print out STATUS: <state> | NEXT_ACTION: <step>