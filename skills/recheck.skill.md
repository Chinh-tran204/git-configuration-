# Recheck Skill

## Goal
Re-implement and correct a task based on updated plan after review failure.

---

## Context

Use:

- `.github/utility/linking/planning_log/` → updated plan (source of truth, read-only)
- `.github/utility/linking/change_log/` → previous implementation

---

## Steps

1. Identify Task
- Locate task from input or change_log (status = recheck)

2. Load Updated Plan
- Find matching entry in planning_log
- Extract updated steps and corrections

3. Analyze Previous Implementation
- Read existing change_log entry
- Identify incorrect or incomplete parts

4. Re-Implement
- Replace flawed logic with updated plan
- Apply fixes step-by-step
- do NOT reuse incorrect implementation blindly

5. Validate
- Ensure behavior matches updated plan
- check:
  - logic correctness
  - edge cases
  - integration

6. Update Log

- Update existing file in:
  `.github/utility/linking/change_log/`
- do NOT create a new file

---

## Rules

- planning_log = read-only
- ALWAYS follow updated plan
- ALWAYS modify existing change_log (no recreate)
- Prefer clean re-implementation over patching
- Keep fixes minimal and correct