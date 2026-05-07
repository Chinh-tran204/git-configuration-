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
1. Scan the project file tree
2. Identify:
   - main folders and their purpose
   - key modules/components
   - relationships between modules
3. Generate 3 documentation files if not exist: structure.md, workflow.md, linking.md. if they exist but empty or incomplete, fill them in.
End State:
After creating these files, STOP.
Do not proceed further.
Wait for the next instruction.
