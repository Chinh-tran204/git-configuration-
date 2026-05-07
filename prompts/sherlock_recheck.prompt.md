---
agent: 'sherlock'
description: 'Recheck implementation for bugs, edge cases, and quality'
---
Task:
Recheck: ${input:task:Feature or bug name}
Mode:
- Validation / second-pass review
Instructions:
- Check for:
  - logic errors
  - edge cases
  - unsafe behavior
  - missing validations
- Review full scope of changes
- Identify anything missed
- DO NOT change or modify any file in `./github/utility/linking/planning_log/`
- Implement to the code base step by step
---
Output:
- Issues found (if any)
- Risk level
- Suggested corrections

---
Stop after review.