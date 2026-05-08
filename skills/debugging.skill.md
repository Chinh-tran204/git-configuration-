# Debugging Skill

## Goal
Identify root cause, explain system behavior, and apply a correct fix when safe.

---

## Context

Use:

- `.github/utility/linking/change_log/` → what was implemented
- `.github/utility/linking/planning_log/` → intended behavior (read-only)

---

## Steps

1. Identify Context
- Locate relevant files and functions from change_log
- Understand expected behavior from planning_log

2. Trace Execution Flow
- Follow how data moves through the system
- Identify where actual behavior deviates from expected

3. Locate Failure Point
- Pinpoint exact logic or step causing issue
- Verify using observed behavior

4. Validate Root Cause
- Confirm reproducibility
- Check:
  - null / empty inputs
  - boundary conditions
  - incorrect assumptions

5. Expand Scope
- Check related modules and dependencies
- Identify possible side effects and hidden issues

6. Fix Decision

- If issue is clear and safe:
  → apply minimal code fix

- If unclear or risky:
  → provide fix plan only (no implementation)

---

## Rules

- Analyze before fixing
- Use change_log as execution truth
- Use planning_log only for validation (do NOT modify)
- Prefer minimal, targeted fixes
- Avoid breaking existing behavior
- Always consider edge cases before applying changes