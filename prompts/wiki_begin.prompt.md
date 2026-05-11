---
agent: 'wiki'
description: 'Initialize project SOT and deterministic maps'
---
Use structure.skill.md for structure.json, workflow.skill.md for workflow.json, and linking.skill.md for linking.json.

## Task
Initialize project understanding and deterministic documentation
Generate structure.json, workflow.json, and linking.json

## Context Boundaries
- Read: repository file tree
- Read: existing project configuration
- Scope: initial project structure only

## Constraints
- do NOT write functional code
- do NOT guess missing structures (use only existing repo data)
- do NOT modify beyond JSON output
- Stop after file generation

## Output
- `.github/utility/SOT/structure.json`
- `.github/utility/SOT/workflow.json`
- `.github/utility/SOT/linking.json`