---
tags:
  - skills
  - development
  - orchestration
---

# Skill: subagent-driven-development

## Overview
Execute implementation plans by dispatching fresh subagents per task with systematic two-stage review (spec compliance then code quality).

## Workflow
1. **Parse Plan**: Read the plan file and extract all tasks.
2. **Per-Task Iteration**:
   - **Implement**: Dispatch subagent to code and test.
   - **Review Stage 1 (Spec Compliance)**: Check if implementation matches original requirements.
   - **Review Stage 2 (Code Quality)**: Check for style, bugs, and performance.
3. **Loop**: Re-run reviews and fixes until the task is APPROVED.
4. **Final Review**: Integration review for consistency across the whole plan.

## Principles
- **Fresh Context**: No confusion from prior tasks' state.
- **TDD Enforcement**: Always write failing tests first.
- **Ordering**: Spec Compliance MUST be approved before Code Quality.

---
*Related: [[sync-notion-to-gitlab]]*
