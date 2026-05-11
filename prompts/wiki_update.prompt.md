---
agent: 'wiki'
description: 'Update structure, workflow, and linking based on completed change logs'
---

## Task
Update project tracking files based on completed changes
Scan change_log for reviewed entries and apply relevant updates to SOT files

## Context Boundaries
- Read: change_log (scan for **status** : REVIEWED)
- Read: planning_log (matching task records)
- Modify: structure.json, workflow.json, linking.json (only **status** : REVIEWED in change_log)
- Scope: only changes not yet reflected

## Constraints
- do NOT apply unreviewed changes
- do NOT guess missing information
- do NOT modify unrelated parts
- do NOT assume beyond current state
- do NOT change **status** field in change_log

## Output
- Summary of updates made (chat only)
- Cleanup: Remove planning_log entry only if corresponding change_log **status** == REVIEWED
- Stop after updating and cleanup