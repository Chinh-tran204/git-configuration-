---
agent: 'sherlock'
description: 'Debug a specific bug and identify root cause'
---

Use debugging.skill.md

Task:
Debug: ${input:task}

Mode:
- Debugging

Rules:
- planning_log is read-only
- follow existing context only

Output:
- root cause
- execution flow
- affected areas
- fix (if applied)