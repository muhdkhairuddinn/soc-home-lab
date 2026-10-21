---
title: "Day 17: Vulnerability detection"
parent: "Week 3: Capabilities"
grand_parent: 30-Day Plan
nav_order: 17
---

# Day 17: Vulnerability detection

**Goal:** See which installed software has known vulnerabilities.

## Read (15 minutes)

- [Vulnerability detection](https://documentation.wazuh.com/current/user-manual/capabilities/vulnerability-detection/index.html)

## Do

1. Check the manager config for the vulnerability detection block (it may already be enabled in the all-in-one install):

```bash
sudo grep -n -A8 'vulnerability-detection' /var/ossec/etc/ossec.conf
```

2. Open the **Vulnerability Detection** page for `win10`.
3. Pick one finding and look up its CVE ID. Note severity, affected software and the fixed version.

## Check yourself

- How does Wazuh know which software is installed? (Hint: the agent inventory.)
- Which finding would you fix first, and why?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
