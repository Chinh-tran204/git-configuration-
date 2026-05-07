---
agent: 'sherlock'
description: 'Implement a feature or task from a ticket'
---
Task:
Work on: ${input:task:Feature name or ticket ID}
Mode:
- Feature implementation
Instructions:
- Read relevant context (wiki outputs, logs)
- Plan execution internally
- Implement to the code base step by step
- Log all actions and changes under this task name in `./github/utility/linking/change_log/`
- DO NOT change or modify any file in `./github/utility/linking/planning_log/`
---
Output:
- Summary of actions taken
- Files modified
- Notes (if any)
---
Stop when current progress is complete.