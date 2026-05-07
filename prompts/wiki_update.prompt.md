---
agent: 'wiki'
description: 'Update structure, workflow, and linking based on completed change logs'
---
Task:
Update project tracking files based on completed changes.
Context:
- Scan: .github/utility/linking/change_log/
- Identify new or completed entries (reviewed and marked done)
---
Actions:
- Extract relevant structural or workflow changes
- Apply updates to:
  - structure.md
  - workflow.md
  - linking.md
---
Rules:
- Only apply confirmed changes (completed/reviewed)
- Do not guess missing information
- Keep updates consistent with current project state
- Do not modify unrelated parts
---
Output:
- Summary of updates made to the chat only, do not log any things or any file.
---
Stop after updating files.
