---
agent: 'sherlock'
description: 'Re-implement task based on updated plan after review failure'
---
Task:
Recheck: ${input:task:ticket or feature name (optional)}

Mode:
- Re-implementation

Context:
- If task is provided → use it
- If not → scan:
  .github/utility/linking/change_log/
  → find entries with:
    status: recheck

---

Actions:

1. Identify target task (from input or change_log)

2. Locate corresponding plan in:
  .github/utility/linking/planning_log/

3. Use updated plan as source of truth

4. Re-implement the task:
  - fix issues from previous version
  - follow updated plan strictly
  - replace incorrect logic with corrected version

5. Log changes into:
  .github/utility/linking/change_log/

---

Rules:
- planning_log = READ ONLY (do not modify)
- use ONLY updated plan as guidance
- do not reuse flawed implementation blindly
- ensure issues flagged by review are resolved

---

Output:
- Summary of fixes applied
- Files modified
- Notes on resolved issues

---

Stop after re-implementation.