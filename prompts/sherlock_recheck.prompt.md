---
agent: 'sherlock'
description: 'Recheck implementation for bugs, edge cases, and quality'
---
Task:
Recheck: ${input:task:feature or bug name}

Mode:
- Validation / second-pass review

Instructions:
- Check for:

  ### Logic & Behavior
  - logic errors
  - incorrect assumptions
  - incomplete flows
  - unexpected behavior paths

  ### Edge Cases
  - empty / null inputs
  - boundary conditions
  - unusual or extreme inputs

  ### Safety & Stability
  - unsafe operations
  - crash risks
  - invalid state transitions
  - missing guards

  ### Data Handling
  - incorrect parsing
  - invalid format handling
  - missing validation for inputs/outputs

  ### Integration
  - broken interactions between modules
  - incorrect dependencies usage
  - mismatch with expected workflow

  ### Code Quality
  - redundant logic
  - overly complex code paths
  - unclear or inconsistent structure

  ### Consistency (IMPORTANT for your system)
  - matches planning_log intent
  - consistent with structure.md / workflow.md
  - respects existing design patterns

  ### Regression Check
  - old behavior accidentally broken
  - previously working paths affected

- Review full scope of changes
- Identify anything missed

- ONLY IF issues are found AND fix is clear and safe:
  - apply minimal corrections to the code

---

Rules:
- Prefer analysis first, correction second
- DO NOT modify:
  .github/utility/linking/planning_log/

---

Output:
- Issues found (if any)
- Risk level (low / medium / high)
- Suggested corrections (or fixes if applied)

---

Stop after review.