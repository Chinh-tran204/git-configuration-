---
name: Technical Linkage Generator
type: Static Analysis Skill
skill_id: technical_linkage_01
output_file: linking.json
---

# Technical Linkage Generator

## Goal
Generate a deterministic `linking.json` mapping all technical code-level relationships, dependencies, and data bonds.

---

## Context
- **Primary Source:** Full project codebase (C, Headers, Scripts).
- **Architecture Baseline:** `structure.md` (read-only).
- **Excluded Scope:** UI/UX, user workflows, and high-level project descriptions (handled in `workflow.md`).

---

## Steps
1. **Symbol Inventory**
   - Extract all function signatures, global/static variables, and `struct`/`typedef` definitions.
2. **Relationship Mapping**
   - Trace caller-callee chains.
   - Map variable read/write access per function.
   - Identify data structure usage across different modules.
3. **Dependency Tracing**
   - Map header file exports to source implementations.
   - Trace return value consumption paths.
4. **Graph Construction**
   - Assemble data into a nodes/links relational structure.
5. **Validation**
   - Verify all file paths and line numbers.
   - Ensure JSON syntax is valid.

---

## Rules
- **Technical Focus Only:** Map variables, functions, and structs; ignore UI/UX and workflows.
- **Deterministic:** Do not assume links; use search to verify every connection.
- **Mandatory Metadata:** Every node must include `filePath` and `lineNumber`.
- **Node Categories:** Function, Variable, Struct, Macro, Enum.
- **Link Types:** Calls, Reads, Writes, ReturnsTo, Instantiates, DependsOn.
- **Format:** Output must be strictly valid JSON.
- **Stop-and-Ask:** If a symbol reference exists without a definition, HALT and ask for the missing file.
- **Scope:** Differentiate between local (file-level) and global (project-level) linkages.