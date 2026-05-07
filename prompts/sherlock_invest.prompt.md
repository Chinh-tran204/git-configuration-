---
agent: 'sherlock'
description: 'Deep investigation and analysis of a topic/module'
---
Task:
Investigate: ${input:task:topic or module}

Mode:
- Deep analysis

Instructions:
- Explore related files/modules
- Map relationships and dependencies
- Identify usage patterns
- Highlight risks and behavior

- OPTIONAL:
  If useful:
  - run small code-level exploration or test changes

Rules:
- Focus on understanding first
- DO NOT modify:
  .github/utility/linking/planning_log/
- planning_log = READ ONLY

Output:
- Overview
- Key components
- Relationship map
- Observations

Stop after analysis.