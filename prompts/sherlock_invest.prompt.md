---
agent: 'sherlock'
description: 'Deep investigation and analysis of a topic/module'
---

Use investigate.skill.md

Task:
Investigate: ${input:task:topic or module}

Mode:
- Deep analysis

Context:
- Use change_log for implementation reference
- Use planning_log for intended behavior (read-only)

Rules:
- Do NOT modify:
  .github/utility/linking/planning_log/
- Focus only on relevant modules/files
- Avoid unnecessary full-repo scanning

Output:
- overview
- key components
- relationship map
- observations