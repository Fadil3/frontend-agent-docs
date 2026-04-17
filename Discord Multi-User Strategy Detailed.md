---
tags:
  - architecture
  - discord
  - multi-user
  - technical
---

# Discord Multi-User & Role Orchestration (Technical Deep-Dive)

## 1. Multi-User Session Management
- **Group Sessions**: `group_sessions_per_user: true` enables collaborative context.
- **Threading**: `auto_thread: true` enforces context isolation via Discord threads. 
    - *Logic*: Task-specific threads prevent interleaving conversations from 10 users.
- **Mention Enforcement**: `require_mention: true` restricts Hermes to responding only when `@Hermes` is tagged.

## 2. Technical Infrastructure: MCP Orchestration
The hub connects three primary MCP servers for shared state across the 10-person team:
- **`figma_dev`**: (Local host:3845) Design source of truth.
- **`notion`**: (@notionhq) Task/PRD/TSD repository.
- **`gitlab`**: (@structured-world/gitlab-mcp) CI/CD and Version Control.

## 3. RBAC (Role-Based Access Control) Implementation
Hermes maintains a local permission map in `memory` keyed by Discord User ID:

| Role | Permissions | Verification |
| :--- | :--- | :--- |
| **Lead Engineer** | Merge, Delete, Global Config | ID Hash Match (Secret) |
| **Frontend Dev** | Create Branch, Commit, Review | Discord ID (General) |

## 4. Conflict Resolution & Concurrency
- **Concurrent Requests**: When multiple users trigger commands, Hermes handles them sequentially at the repository level (preventing git locking errors) but spawns independent **subagents** for actual implementation.
- **Context Pollution**: Each subagent receives only the task-specific PRD/TSD context + the global repository standards (`Frontend Engineering Standards.md`).

## 5. Security & Safety
- **Circuit Breaker**: Automation is explicitly blocked from `Merge` operations on `main`. 
- **Channel Locking**: Hermes uses `allowed_channels` list to ignore cross-talk from other Discord channels.
- **Drift Detection**: Weekly scheduled audit (`0 9 * * 1`) checks for documentation-code misalignment.
