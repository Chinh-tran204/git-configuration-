# Feature Work Skill

## Goal
Implement a feature or task correctly based on planning and logs.

---

## Context

Use:

- `.github/utility/linking/planning_log/` → plan / expected behavior (read-only)
- `.github/utility/linking/change_log/` → execution history

---

## Steps

1. Understand Task
- Identify task from input or logs
- Locate corresponding plan in planning_log

2. Interpret Plan
- Extract CURRENT_STEP or full flow if needed
- Understand expected behavior and scope

3. Prepare Implementation
- Identify target files and modules
- Map dependencies and affected areas

4. Implement Step-by-Step
- Apply changes based on plan
- Keep changes minimal and scoped
- Update or create required code

5. Validate Implementation
- Ensure behavior matches plan
- Check:
  - logic correctness
  - edge cases
  - integration with existing modules

6. Log Changes

- Write/update:
  `.github/utility/linking/change_log/`

- Ensure:
  - same task name used
  - existing file is updated (no duplicates)

---

## Rules

- Use planning_log as source of truth (read-only)
- Do NOT modify planning_log
- ALWAYS read existing files before modifying
- ALWAYS update existing change_log entry (no recreate)
- Prefer minimal, targeted changes
- Do not introduce unrelated changes