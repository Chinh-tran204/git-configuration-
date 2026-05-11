---
agent: 'sherlock'
description: 'Re-implement task based on updated plan after review failure'
---
Use recheck.skill.md

## Task
Recheck: ${input:task:ticket or feature name (optional)} 
Re-implement based on updated plan and resolve flagged issues

## Context Boundaries
- just scan change_log for entries with **status**: RECHECK if no input match STOP
- Read: planning_log/ (source of truth)
- Read: change_log/ (execution history) for better context of what to fix
- scope: task-specific files and dependencies only


## Constraints
- do NOT recreate change_log (update existing only)
- do NOT ignore updated plan
- do NOT use wrong task name
- do NOT modify `.github/utility/linking/planning_log/` and `.github/utility/linking/SOT/` (READ-ONLY)

## Output
- **status**: COMPLETED in change_log when done
- print out STATUS: <state> | NEXT_ACTION: <step>