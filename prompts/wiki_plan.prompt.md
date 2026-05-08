---
agent: 'wiki'
description: 'Create or replan tasks based on new input or reviewer feedback'
---
Task:
Create or update a plan for a ticket/problem.

Context:
- If task is provided:
  → locate matching plan (if exists)
  → otherwise create new

- If NOT provided:
  → scan:
    .github/utility/linking/planning_log/
  → find entries that contain missing fields or reviewer updates

---

Actions:
1. Identify target task:
  - from input OR
  - from planning_log (entries with missing info)

2. If NEW task:
  - create a fresh plan

3. If EXISTING task:
  - replan based on reviewer feedback
  - expand missing fields
  - improve structure and coverage

4. Update plan to:
  - include missing steps
  - clarify unclear steps
  - cover edge cases and full scenario

---

Output:
- PLAN
- CURRENT_STEP

---

Log result in:
.github/utility/linking/planning_log/

Rules:

- NEW task → create new file

- EXISTING task → update ONLY:
  - missing fields
  - incorrect or incomplete steps

- DO NOT remove or overwrite valid existing content

File name:
<task-name>-<YYYYMMDD>.md

Content:

# Plan: <task name>

Date: <YYYY-MM-DD>

## Summary
<short description>

## Plan
1.
2.
3.
---

Stop after logging.
