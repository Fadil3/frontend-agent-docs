---
tags:
  - architecture
  - mermaid
  - deepdive
  - hardened
---

# Hermes Frontend Automation - Detailed Architecture

## High-Level Workflow
```mermaid
graph TD
    Inputs --> Hub
    Hub --> Outputs

    subgraph Inputs ["Data Ingest Layer"]
        N[Notion MCP]
        F[Figma MCP]
    end

    subgraph Hub ["Hermes Agent Orchestrator"]
        H[Hermes Hub]
        H --- S1[Skill: sync-notion-to-gitlab]
        H --- S2[Skill: subagent-driven-dev]
        H --- S3[Skill: drift-detector]
    end

    subgraph Outputs ["Execution Layer"]
        G[GitLab CI/CD]
        C[Local Codebase]
        T[Test Suite]
    end
```

---

## The Hardened Infrastructure
```mermaid
graph LR
    subgraph Hardening ["Safety & Audit Layers"]
        Cron[Weekly Drift Detector Cron] -->|Audit| Repo
        Repo -->|Compare vs Notion| H[Hermes Hub]
        H -->|Notify Discrepancies| Discord[Discord #frontend-dev]
        
        GitLabMR[Merge Request] -->|Circuit Breaker| Human[Lead Engineer Approval]
        Human -->|Merge| Production[Production]
    end
```

---

## Node Deep-Dives

### 1. Inputs (MCP Layer)
```mermaid
graph LR
    subgraph Notion_MCP ["Notion MCP Server (@notionhq)"]
        N1[Query Database]
        N2[Read Page: PRD]
        N3[Read Page: TSD]
        N4[Update Task Status]
    end
    subgraph Figma_MCP ["Figma MCP Server (figma-developer-mcp)"]
        F1[Get Node Properties]
        F2[Extract Styles/CSS]
        F3[Download Image Assets]
    end
```

### 2. Hermes Hub (Orchestrator Layer)
```mermaid
graph TD
    subgraph Sync_Skill ["sync-notion-to-gitlab"]
        S1_1[Fetch Notion: PRD + TSD]
        S1_2[Format Markdown Template]
        S1_3[Push to GitLab API]
        S1_4[Initialize Git Branch]
    end
    subgraph Dev_Skill ["subagent-driven-dev"]
        S2_1[Parsing Implementation Plan]
        S2_2[Dispatch Implementer Subagent]
        S2_3[Dispatch Spec Compliance Subagent]
        S2_4[Dispatch Quality Assurance Subagent]
    end
```

### 3. Outputs (Execution Layer)
```mermaid
graph TD
    subgraph GitLab ["GitLab Integration"]
        G1[Issue Tracking]
        G2[Branch/Merge Request]
    end
    subgraph Codebase ["Development"]
        C1[UI Slicing]
        C2[Component Injection]
    end
    subgraph Verification ["Quality Gate"]
        T1[Typecheck & Lint]
        T2[TDD/Unit Tests]
        T3[A11y/Best Practice Scan]
    end
```

---

## Orchestration Sequence
```mermaid
sequenceDiagram
    participant U as User
    participant H as Hermes Hub
    participant N as Notion MCP
    participant G as GitLab MCP
    participant S as Subagents

    U->>H: "Sync this Notion task"
    H->>N: Fetch PRD + TSD details
    N-->>H: Return Task Data
    H->>G: Create Issue + Branch
    U->>H: "Implement this issue"
    H->>S: Dispatch Implementer (TDD)
    S-->>H: Implementation complete
    H->>S: Dispatch Compliance Reviewer
    S-->>H: Approved
    H->>S: Dispatch Quality Reviewer
    S-->>H: Approved
```
