---
name: Project Workflow Generator
type: Operational Mapping Skill
skill_id: project_workflow_01
output_file: workflow.json
---

# Project Workflow Generator

## Goal
Generate a deterministic `workflow.json` mapping the functional logic, user interactions, system state transitions, and feature scope.

---

## Context
- **Primary Source:** Functional requirements and high-level logic.
- **Source of Truth:** Intended operational design.
- **Excluded Scope:** Physical file locations (`structure.json`) and low-level code dependencies (`linking.json`).

---

## Steps
1. **Entry Point Identification**
   - Catalog all triggers (User actions, API calls, System events).
2. **Sequence Mapping**
   - Define step-by-step operational flows for every feature.
3. **State Transition Recording**
   - Document how the system state changes at each step.
4. **Feature Anchoring**
   - Assign every feature to a specific "Work Scope" or "Job" node.
5. **Flow Connectivity**
   - Map how separate workflows interlock or exchange data.
6. **JSON Assembly**
   - Construct a logic-first graph representing the project's behavior.

---

## Rules
- **Operational Focus Only:** Map the "how it runs" (Behavior), not the "where it is" (Structure).
- **Work Scope Definition:** Every feature must include a `purpose` and `workScope` identifier.
- **Node Categories:** Trigger, Action, Decision, State, SuccessOutcome, ErrorOutcome.
- **Link Types:** LeadsTo, Triggers, Validates, RequiresState, Terminates.
- **Integration Points:** Each flow node must reference a logical module ID compatible with `structure.json`.
- **Format:** Output must be strictly valid JSON.
- **Metadata Requirements:** Include `flowID`, `triggerSource`, `expectedState`, and `terminalCondition`.

---

## Behavior Constraints
- Use machine-friendly, non-conversational keys.
- Ignore code-level variables or pointer logic.
- Omit UI/UX design aesthetics; focus on interaction logic.
- STOP and ask if a system state or user interaction path is ambiguous.