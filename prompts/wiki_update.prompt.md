---
agent: 'wiki'
description: 'Update structure, workflow, and linking based on completed change logs'
---
Task:
Update project tracking files based on completed changes.

Context:
- Scan: .github/utility/linking/change_log/
- Identify new or completed entries (**status:** == reviewed)

Actions:
- Extract relevant structural or workflow changes
- Apply updates to:

  - .github/utility/SOT/structure.md
  - .github/utility/SOT/workflow.md
  - .github/utility/SOT/linking.md

---

Cleanup Step:

After successfully applying updates:

- Locate the corresponding entry in:
  .github/utility/linking/planning_log/

- Remove that entry if:
  - the task is completed and **status:** == reviewed only

---

Rules:
- Only apply confirmed changes (**status:** == reviewed)
- Only apply changes not yet reflected
- Do not guess missing information
- Keep updates consistent with current project state
- Do not modify unrelated parts

---

Output:
- Summary of updates made (chat only)

---

Stop after updating and cleanup.
``