---
agent: 'wiki'
description: 'Create plan and log it to planning.md'
---
Task:
Create a plan for the given ticket/problem.
Output:
- PLAN
- CURRENT_STEP 
Log the result as .md file as new entry in:
.github/utility/linking/planning_log/
Format:
File name:
<task-name>-<YYYYMMDD>.md
Content:
# Plan: <task name>
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
- Append new files only (do not overwrite existing logs)
Stop after logging.