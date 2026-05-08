---
agent: 'sherlock'
description: 'Implement a feature or task from a ticket'
---

Use feature_work.skill.md

Task:
Work on: ${input:task:ticket or feature name}

Mode:
- Feature implementation

Context:
- Use planning_log as source of truth
- Use change_log for history

Rules:
- planning_log is read-only
- Identify and reuse exact task name
- Always update existing change_log file (no recreate)

Output:
- Summary of actions taken
- Files modified