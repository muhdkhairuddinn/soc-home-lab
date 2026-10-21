---
title: "Day 26: Secure the SIEM itself"
parent: "Week 4: SOC work"
grand_parent: 30-Day Plan
nav_order: 26
---

# Day 26: Secure the SIEM itself

**Goal:** Treat Wazuh as the most sensitive machine in the lab.

## Do

1. Change the default admin password using Wazuh's password tool (search the docs for "password management") and store the new one in a password manager.
2. Check who can reach the dashboard: it should only be reachable from the lab network.
3. List what an attacker could learn if they got into Wazuh: every log from every machine.

## Check yourself

- What is the first thing an attacker would try to turn off?
- Is your admin password anywhere in this repo? (It must never be.)

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
