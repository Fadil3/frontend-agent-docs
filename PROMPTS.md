---
tags:
  - communication
  - workflow
---

# Hermes Prompt Cheat Sheet

Use these standard commands to interact with Hermes in the `#frontend-dev` Discord channel.

## 🚀 Project Management
- **Sync Task**: `@Hermes sync this Notion task [URL]`
  - *Action*: Fetches PRD/TSD, creates GitLab issue, initializes git branch.
- **Audit Drift**: `@Hermes run drift-detector`
  - *Action*: Audits codebase against Notion technical specs.

## 💻 Development
- **Implement Task**: `@Hermes implement issue [Issue_ID] from [Figma_Node_ID]`
  - *Action*: Orchestrates subagents to slice UI, write code, and verify with tests.
- **Review Code**: `@Hermes request-code-review [Branch_Name]`
  - *Action*: Triggers automated quality gates, linting, and A11y scans.

## 🔄 Lifecycle
- **Status Report**: `@Hermes what is the status of [Issue_ID]?`
- **Help**: `@Hermes help`
