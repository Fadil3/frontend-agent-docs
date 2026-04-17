---
tags:
  - architecture
  - devops
  - migration
---

# Migration & Deployment Guide (New Machine)

To replicate this entire Frontend Automation infrastructure on a new machine, follow this systematic migration guide.

## 1. Prerequisites (Target Machine)
Ensure the following are installed on the new system:
- **Hermes Agent**: Primary CLI installation.
- **Node.js & npm**: Required for `npx` (MCP servers).
- **Docker**: Required if using containerized execution for subagents.
- **Git**: For pulling the Obsidian vault and managing the codebase.

## 2. Backup Current Machine
Run these commands to package your custom logic and configurations:
```bash
# Archive the core Hermes config and local skills
tar -czvf hermes_backup.tar.gz ~/.hermes/config.yaml ~/.hermes/skills/

# Sync your Obsidian vault (ensure all documentation is pushed to git)
cd "[VAULT_ROOT]/"
git add .
git commit -m "Backup architecture and automation skills"
git push
```

## 3. Deployment on New Machine
1. **Clone the documentation**:
   ```bash
   git clone [YOUR_OBSIDIAN_VAULT_REPO] ~/Documents/vault/second\ brain/
   ```
2. **Restore Hermes Logic**:
   ```bash
   tar -xzvf hermes_backup.tar.gz -C ~/
   ```
3. **Re-populate Secrets**:
   Edit `~/.hermes/config.yaml` to re-insert your Personal Access Tokens (Figma, Notion, GitLab) into the `env` blocks. **Do not commit these to Git.**

## 4. Verification Flow
Run these commands to ensure the system is operational:
```bash
# Check if skills are discoverable
hermes skills-list

# Run a test drift-detection audit (Manual trigger)
hermes run "drift-detector"
```

## 5. Portability Note
The `sync-notion-to-gitlab` and `subagent-driven-dev` skills rely on the `~/.hermes/skills/` path. Keeping this directory backed up ensures your custom "brain" remains intact across hardware migrations.
