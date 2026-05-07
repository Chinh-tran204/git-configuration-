---
agent: 'sherlock'
description: 'Implement a feature or task from a ticket'
---
Task:
Work on: ${input:task:ticket or feature name}

Mode:
- Feature implementation

Instructions:
- Read relevant context (wiki outputs, logs)
- Plan execution internally if needed
- Implement to the code base step by step
- Log all actions in:
  .github/utility/linking/change_log/

Rules:
- DO NOT write to:
  .github/utility/linking/planning_log/
- Use planning_log as read-only context
- planning_log = READ ONLY
Output:
- Summary of actions taken
- Files modified
- Notes

Stop when current progress is complete.