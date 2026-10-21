---
title: "Day 15: File integrity monitoring (FIM)"
parent: "Week 3: Capabilities"
grand_parent: 30-Day Plan
nav_order: 15
---

# Day 15: File integrity monitoring (FIM)

**Goal:** Get an alert when a file in a watched folder changes.

## Read (15 minutes)

- [File integrity monitoring](https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html)

## Do

On the Windows VM, as Administrator, create a test folder and add it to the agent config (`C:\Program Files (x86)\ossec-agent\ossec.conf`, inside `<syscheck>`):

```xml
<directories check_all="yes" realtime="yes">C:\LabFim</directories>
```

```powershell
mkdir C:\LabFim
Restart-Service WazuhSvc
Set-Content C:\LabFim\note.txt 'hello'
Add-Content C:\LabFim\note.txt 'changed'
Remove-Item C:\LabFim\note.txt
```

Look in **File Integrity Monitoring** for added, modified and deleted events (rules 554, 550, 553).

## Check yourself

- What does FIM record about the change (hash, size, who)?
- Which real folders would you watch on a server?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
