---
agent: 'sherlock'
description: 'Deep investigation and analysis of a topic/module'
---
Task:
Investigate: ${input:task:Topic or component}
Mode:
- Deep analysis
Instructions:
- Explore related files/modules
- Map relationships and dependencies
- Identify usage patterns
- Highlight risks, complexity, and key behaviors
- DO NOT change or modify any file in `./github/utility/linking/planning_log/`
- Implement to the code base step by step
---
Output:
- Overview
- Key components
- Relationship map
- Observations
---
Stop after analysis