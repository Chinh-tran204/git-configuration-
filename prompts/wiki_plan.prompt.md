---
agent: 'wiki'
description: 'Create plan and log it to planning.md'
---
Task:
Create a plan for the given ticket/problem.
Output:
- PLAN
- CURRENT_STEP
---
Log the result as .md file as new entry in: .github/utility/linking/planning_log/
Format:
name:  <ticket-name-or-short-description>_<YYYY-MM-DD>.md
Content:
# Plan: <ticket-name-or-short-description>
Date: <YYYY-MM-DD>
## Summary
<short description>
## Plan
1.
2.
3.
## Current Step
<step number>
---
Rules:
- Append only (do not overwrite)
- Use clear, short name (ticket ID or summary)
- Keep entries separated by `---`
---
Stop after logging.
