---
title: "Day 13: Sysmon in more detail"
parent: "Week 2: Detection"
grand_parent: 30-Day Plan
nav_order: 13
---

# Day 13: Sysmon in more detail

**Goal:** Know which Sysmon events matter and how the config controls them.

## Read (15 minutes)

- [SwiftOnSecurity Sysmon config](https://github.com/SwiftOnSecurity/sysmon-config)

## Do

1. On the Windows VM, open Event Viewer, then Applications and Services Logs, Microsoft, Windows, Sysmon, Operational.
2. Look at one event of each type: 1 (process created), 3 (network connection), 11 (file created), 13 (registry value set), 22 (DNS query).
3. Open the SwiftOnSecurity config on GitHub and find the section for one of those event types. Notice that it filters, so Sysmon does not log everything.
4. Check which config is loaded now:

```powershell
sysmon64 -c
```

## Check yourself

- Which Sysmon event IDs turn into Wazuh alerts in your lab?
- Why is logging everything a bad idea?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
