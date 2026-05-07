---
agent: 'wiki'
description: 'Update structure, workflow, and linking based on completed change logs'
---
Task:
Update project tracking files based on completed changes.
Context:
- Scan: .github/utility/linking/change_log/
- Identify new or completed entries (reviewed and marked done)
Actions:
- Extract relevant structural or workflow changes
- Apply updates to:
  - .github/utility/SOT/structure.md
  - .github/utility/SOT/workflow.md
  - .github/utility/SOT/linking.md
Rules:
- Only apply confirmed changes (completed/reviewed)
- Only apply changes not yet reflected
- Do not guess missing information
- Keep updates consistent with current project state
- Do not modify unrelated parts
Output:
- Summary of updates made to the chat only, do not log anything

Stop after updating files.
