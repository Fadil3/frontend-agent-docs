---
tags:
  - skills
  - automation
  - notion
  - gitlab
---

# Skill: sync-notion-to-gitlab

## Overview
Automates the synchronization of PRDs/Tasks from Notion to GitLab issues and branch management.

## Trigger
- "Hermes, move this task to GitLab"
- "Sync this Notion PRD to an issue"

## Workflow
1. **Fetch**: Use Notion MCP to get the PRD/task details.
2. **Format**: Structure the data into a standard GitLab issue template.
3. **Push**: Use GitLab MCP to create a new issue.
4. **Initialize**: Use GitLab MCP to create a dedicated branch linked to the issue.

## Configuration Requirements
This workflow requires the Notion and GitLab MCP servers configured in `~/.hermes/config.yaml`.

---
*Related: [[subagent-driven-dev]]*
