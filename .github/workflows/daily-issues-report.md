---
name: "Daily Issues Report"
description: "Generates a daily summary of open issues and recent activity as a GitHub issue"
tools:
  github:
    toolsets: [repos, issues]
    min-integrity: unapproved
on:
  schedule: daily on weekdays
permissions:
  contents: read
  issues: read
safe-outputs:
  create-issue:
    title-prefix: "[daily-report] "
    labels: [report]
source: github/awesome-copilot/workflows/daily-issues-report.md@ab7544d03d4c49fdd07f5958e1888ad39c4118e2
---

# Daily Issues Report

Create a daily summary of open issues for the team.

## What to Include

- New issues opened in the last 24 hours
- Issues closed or resolved
- Blocked issues that need attention identified as issues with the field `Progress`=`Blocked`.
- For each open milestone calculate the min/max anticipated work based on the `effort` fields T-shirt sizes distributeed across the different settings of the `priority` field. (The range for the sizes are defined in the field value descriptions, use 'one day'='7 hours').
