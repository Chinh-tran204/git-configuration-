---
agent: 'sherlock'
description: 'Re-implement task based on updated plan after review failure'
---

Use recheck.skill.md

Task:
Recheck: ${input:task:ticket or feature name (optional)}

Mode:
- Re-implementation

Context:
- If task provided → use it
- If not → scan:
  .github/utility/linking/change_log/
  → find status: recheck

Rules:
- ALWAYS use updated plan from:
  .github/utility/linking/planning_log/
- planning_log = read-only
- ALWAYS update existing change_log file (no recreate)
- Use exact task name

Output:
- summary of fixes
- files modified
- resolved issues