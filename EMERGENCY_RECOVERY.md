---
tags:
  - safety
  - recovery
---

# Emergency Recovery (Safety Valve)

In the event of agent malfunction, corrupted code, or deployment errors, follow these steps immediately.

## 1. Stop Agent Activity
- Immediately delete the current task thread in Discord.
- Hermes responds to thread context; deleting the thread halts the current agent session.

## 2. Revert Changes
If Hermes pushed bad code to a branch:
```bash
# Hard reset to last known good commit
git checkout [branch_name]
git reset --hard HEAD~1
git push --force origin [branch_name]
```

## 3. Clear Agent State
If the agent is in a "loop" or acting erratically:
1. Restart Hermes: `pm2 restart hermes-agent` (or your service manager).
2. Manually verify the state of `~/.hermes/`.

## 4. Report to Lead
- Post the error trace and branch state in `#frontend-dev`.
- Open an emergency issue in GitLab with the label `bug::agent`.
