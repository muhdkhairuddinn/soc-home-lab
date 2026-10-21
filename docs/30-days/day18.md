---
title: "Day 18: Add a Linux agent"
parent: "Week 3: Capabilities"
grand_parent: 30-Day Plan
nav_order: 18
---

# Day 18: Add a Linux agent

**Goal:** Monitor a second kind of machine.

## Read (15 minutes)

- [Wazuh agent](https://documentation.wazuh.com/current/user-manual/agent/index.html)
- [Log data collection](https://documentation.wazuh.com/current/user-manual/capabilities/log-data-collection/index.html)

## Do

1. Install the Wazuh agent on the Kali VM using the deployment steps in the docs. Point it at `10.10.10.5`.
2. Confirm it shows Active:

```bash
sudo /var/ossec/bin/agent_control -l
```

3. Check which log it reads for logins (`/var/log/auth.log`, or journald on newer systems).
4. Make one wrong `sudo` password attempt on Kali and find the alert.

## Check yourself

- How do Windows and Linux login failures differ in the raw log?
- Which rule groups did the Linux alert belong to?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
