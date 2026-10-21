---
title: "Day 1: What a SIEM does and how Wazuh is built"
parent: "Week 1: Foundations"
grand_parent: 30-Day Plan
nav_order: 1
---

# Day 1: What a SIEM does and how Wazuh is built

**Goal:** Explain Wazuh's parts in your own words and find each one running in your lab.

## Read (15 minutes)

- [Wazuh architecture](https://documentation.wazuh.com/current/getting-started/architecture.html)

## Do

1. Read the architecture page. Draw the lab on paper: Windows agent, Wazuh server, indexer, dashboard.
2. On the Wazuh VM, check that the three services are running:

```bash
sudo systemctl status wazuh-manager wazuh-indexer wazuh-dashboard --no-pager
```

3. Find which ports are listening. 1514 is agents talking to the server, 1515 is enrolling new agents, 55000 is the API, 9200 is the indexer, 443 is the dashboard:

```bash
sudo ss -tlnp | grep -E '1514|1515|55000|9200|443'
```

## Check yourself

- What does the agent do, and what does the manager do?
- Which component stores alerts, and which one only shows them?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
