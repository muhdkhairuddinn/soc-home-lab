---
title: "Day 21: Week 3 review"
parent: "Week 3: Capabilities"
grand_parent: 30-Day Plan
nav_order: 21
---

# Day 21: Week 3 review

**Goal:** List what Wazuh can see in your lab, and what it can't.

## Do

Make a table: log source, what it covers, how it reaches Wazuh.

| Source | Covers | How |
|---|---|---|
| Windows Security log | Logons | Agent, `Security` channel |
| Sysmon | Process, registry, network | Agent, Sysmon channel |
| FIM | File changes | Agent, syscheck |
| SCA | Hardening | Agent |

Add one column: what attack would slip past each one.

## Check yourself

- Which gaps surprised you?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
