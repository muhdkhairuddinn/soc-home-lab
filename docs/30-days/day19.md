---
title: "Day 19: Active response (read and trace)"
parent: "Week 3: Capabilities"
grand_parent: 30-Day Plan
nav_order: 19
---

# Day 19: Active response (read and trace)

**Goal:** Understand how Wazuh can react to an alert, without breaking your lab.

## Read (15 minutes)

- [Active response](https://documentation.wazuh.com/current/user-manual/capabilities/active-response/index.html)

## Do

Active response runs a script on an agent when a rule fires, for example blocking an IP.

1. Read the docs page.
2. Find the `<active-response>` and `<command>` blocks in the manager's `ossec.conf`.
3. On Windows, notice that the agent already reads `active-response\active-responses.log` (you saw it in the agent config).

Do not enable blocking on the machine you are using to run the lab. A block rule with the wrong match can cut off your own access.

## Check yourself

- What could go wrong if a rule blocks the wrong IP?
- Which alerts would you trust enough to auto-respond to?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
