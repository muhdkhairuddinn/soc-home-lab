---
title: "Day 2: Dashboard tour"
parent: "Week 1: Foundations"
grand_parent: 30-Day Plan
nav_order: 2
---

# Day 2: Dashboard tour

**Goal:** Know where to click for events, agents, rules and decoders.

## Read (15 minutes)

- [Wazuh dashboard](https://documentation.wazuh.com/current/user-manual/wazuh-dashboard/index.html)

## Do

1. Log in to `https://10.10.10.5`.
2. Visit each: **Endpoints Summary**, **Threat Hunting** (Dashboard and Events tabs), **File Integrity Monitoring**, **Configuration Assessment**, **MITRE ATT&CK**, **Server management** (Rules, Decoders).
3. In Threat Hunting, change the time range and pick agent `win10`.
4. In **Server management**, open **Rules** and search for `60122`.

Tip from my lab: the plain **Discover** page sometimes shows "Start searching" and never loads. The **Events** tab in Threat Hunting worked fine.

## Check yourself

- Where do you see every alert for one agent?
- Which page shows the XML of a rule?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
