# Feature Work Skill

## Goal
Implement feature or task correctly per planning_log specifications

## Context
- Read: planning_log (source of truth, read-only)
- Read: change_log (execution history)
- Write: change_log (log implementation)

## Steps
1. **Identify Task** → locate from input or logs; find corresponding plan in planning_log
2. **Extract Plan** → read CURRENT_STEP or full flow; understand expected behavior and scope
3. **Map Implementation** → identify target files, modules, and dependencies
4. **Implement** → apply changes step-by-step; keep changes minimal and scoped
5. **Validate** → ensure behavior matches plan (logic, edge cases, integration)
6. **Log Changes** → update change_log with same task name (no duplicates)

## File-Aware Rules
- Read planning_log first before implementation
- Always update existing change_log (never recreate)
- Use exact task name for consistency