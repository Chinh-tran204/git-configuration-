---
agent: 'wiki'
description: 'Initialize project understanding and documentation'
---
Tasks:
Initialize project understanding and documentation.

Context:
- Explore the current repository structure (folders, files)
- Do NOT analyze internal code logic in detail
- Focus only on high-level architecture and relationships

Constraints:
- Do NOT write or modify or implement code
- Do NOT guess missing structure — only use what exists
- Keep everything high-level and structured

Actions:
- Scan the project file tree
- Identify:
  - main folders and their purpose
  - key modules/components
  - relationships between modules

- Generate or update these files:
  - .github/utility/SOT/structure.md
  - .github/utility/SOT/workflow.md
  - .github/utility/SOT/linking.md

Output:
- Write structured markdown content directly into the above files

End State:
   After creating these files, STOP.
   Do not proceed further.
   Wait for the next instruction.