---
name: Project Structure Generator
type: Architectural Mapping Skill
skill_id: project_structure_01
output_file: structure.json
---

# Project Structure Generator

## Goal
Generate a deterministic `structure.json` mapping the physical and logical hierarchy of the project, including folders, files, and function locations.

---

## Context
- **Primary Source:** File system and directory tree.
- **Source of Truth:** Current codebase architecture.
- **Excluded Scope:** Logic dependencies (`linking.json`) and user-facing data flows (`workflow.md`).

---

## Steps
1. **Directory Crawl**
   - Map all top-level and nested directories.
   - Define parent-child relationships for every folder.
2. **File Inventory**
   - Catalog all files within their respective parent directories.
   - Identify file types (Source, Header, Script, Config).
3. **Function Localization**
   - Index all function names and map them to their specific parent file.
   - Record exact start/end line numbers for every function.
4. **Architectural Summary**
   - Extract a 1-sentence "purpose" for each directory, file, and module.
5. **JSON Assembly**
   - Construct a nested tree structure representing the full project map.

---

## Rules
- **Structural Focus Only:** Map the "where" (locations), not the "how" (logic) or "why" (UI).
- **Hierarchical Integrity:** Every node must explicitly state its `parent` or `path`.
- **Function Mapping:** Functions must be listed as children of the file node they inhabit.
- **Categorization:** Group files into logical "Modules" (e.g., Backend, UI, Utils).
- **Format:** Output must be strictly valid JSON.
- **Metadata Requirements:** Include `name`, `type`, `path`, `lineNumbers`, and `description` for all nodes.
- **Stop-and-Ask:** If a directory is inaccessible or a file cannot be parsed, HALT and ask for permission/info.

---

## Behavior Constraints
- Use machine-friendly, concise terminology.
- Omit all UI/UX or workflow descriptions.
- Do not analyze code logic or cross-file data links.
- Strictly follow the physical organization of the repository.