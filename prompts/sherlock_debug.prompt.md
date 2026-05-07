---
agent: 'sherlock'
description: 'Debug a specific bug and identify root cause'
---
Task:
Debug: ${input:task:Bug name or ticket ID}
Mode:
- Debugging
Instructions:
- Identify root cause
- Trace execution flow
- Explain how the issue happens
- Map affected components
- Outline a step-by-step fix plan (NO implementation yet)
- DO NOT change or modify any file in `./github/utility/linking/planning_log/`
- Implement to the code base step by step
---
Output:
- Root cause
- Execution flow
- Affected areas
- Fix plan
---
Stop after analysis.