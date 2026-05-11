# Debugging Skill

## Goal
Identify root cause, trace execution flow, validate, and apply safe fix when possible

## Context
- Read: planning_log (what to do, read-only)
- Read: change_log (execution history)
- Focus: existing context only

## Steps
1. **Locate Issue** → find relevant files/functions from change_log and planning_log
2. **Trace Flow** → follow data and execution path to identify deviation from expected behavior
3. **Pinpoint Failure** → locate exact logic/step causing issue
4. **Validate Root Cause** → confirm with edge cases (null, boundaries, invalid assumptions)
5. **Expand Scope** → check related modules for side effects
6. **Decide Fix** → if clear and safe, apply minimal fix; else provide plan only

## File-Aware Rules
- Read before fixing
- Apply minimal code changes only
- Update change_log with fix applied