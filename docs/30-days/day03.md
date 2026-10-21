---
title: "Day 3: Agents"
parent: "Week 1: Foundations"
grand_parent: 30-Day Plan
nav_order: 3
---

# Day 3: Agents

**Goal:** List, inspect and restart an agent from both sides.

## Read (15 minutes)

- [Wazuh agent](https://documentation.wazuh.com/current/user-manual/agent/index.html)

## Do

On the Wazuh VM:

```bash
sudo /var/ossec/bin/agent_control -l
sudo /var/ossec/bin/agent_control -i 001
```

On the Windows VM (PowerShell as Administrator):

```powershell
Get-Service WazuhSvc
Get-Content "C:\Program Files (x86)\ossec-agent\ossec.log" -Tail 15
```

Restart the agent from Windows and watch it go Disconnected and then Active again in the dashboard:

```powershell
Restart-Service WazuhSvc
```

## Check yourself

- What does the agent log say when it connects to the server?
- How long did it take to show Active again?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
