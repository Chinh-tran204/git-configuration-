# Recheck Skill

## Goal
Re-implement task correctly based on updated plan after review failure

## Context
- Read: planning_log (updated plan with corrections, read-only)
- Read: change_log (previous implementation and issues)
- Write: change_log (update existing entry, no recreate)

## Steps
1. **Identify Task** → locate from input or scan change_log for status: recheck
2. **Load Updated Plan** → find matching planning_log entry; extract corrections
3. **Analyze Previous** → read existing change_log entry; identify flawed parts
4. **Re-Implement** → replace flawed logic with updated plan; apply fixes step-by-step
5. **Validate** → ensure behavior matches updated plan (logic, edge cases, integration)
6. **Update Log** → update existing change_log file (never create new)

## File-Aware Rules
- Never recreate change_log (always update existing entry)
- Don't reuse incorrect implementation blindly
- Reference updated plan in every step