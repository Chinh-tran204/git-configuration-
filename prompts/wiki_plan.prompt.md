---
agent: 'wiki'
description: 'Create or replan tasks based on new input or reviewer feedback'
---

## Task
Create or update a plan for a ticket/problem using PLANNING_TEMPLATE.md
- If task provided: locate existing plan or create new
- If not provided: scan planning_log for entries with ##missing fields or reviewer updates

## Context Boundaries
- If input: use provided task directly
- If not: read planning_log (entries with missing info), no missing info found, STOP and ask for task details
- Scope: planning layer only (no code implementation)

## Constraints
- do NOT create new plans if fixing missing/incorrect info in existing ones
- Update ONLY missing or incorrect fields
- do NOT remove valid existing content
- do NOT overwrite complete sections unnecessarily
- do NOT implement code or modify source files

## Output
- PLAN (structured steps)
- CURRENT_STEP
