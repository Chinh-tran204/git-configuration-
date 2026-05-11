---
agent: 'sherlock'
description: 'Implement a feature or task from a ticket'
---
Use feature_work.skill.md

## Task
Work on: ${input:task:ticket or feature name}
Implement feature per planning_log specifications

## Context Boundaries
- If input provided: use it directly, if not, ask for specific task details
- Read: planning_log/ (source of truth)
- Read: change_log/ (execution history)
- if file or things in planning_log exit in change_log then passed
- Scope: task-specific files and dependencies
- set file **status**: COMPLETED in change_log when done

## Constraints
- do NOT change task name
- do NOT modify `.github/utility/linking/planning_log/` and `.github/utility/linking/SOT/` (READ-ONLY)

## Output
- **status**: COMPLETED in change_log when done
- print out STATUS: <state> | NEXT_ACTION: <step>