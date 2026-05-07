---
agent: 'sherlock'
description: 'Debug a specific bug and identify root cause'
---
Task:
Debug: ${input:task:bug name or ticket}

Mode:
- Debugging

Instructions:
- Identify root cause
- Trace execution flow
- Explain how the issue happens
- Map affected components

- THEN:
  If the fix is clear and safe:
  - Implement minimal fix in code

Rules:
- Prefer analysis first, implementation second
- DO NOT modify:
  .github/utility/linking/planning_log/
- planning_log = READ ONLY

Output:
- Root cause
- Execution flow
- Affected areas
- Fix (if applied)

Stop after completion.