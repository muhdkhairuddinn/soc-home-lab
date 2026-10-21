---
title: "Day 1: How Wazuh is built"
parent: "Week 1: Foundations"
grand_parent: My 30-Day Journey
nav_order: 1
---

# Day 1: How Wazuh is built

A SIEM collects logs from many machines in one place, checks them against rules, and shouts when something looks odd. Wazuh does that with four parts.

## The four parts

| Part | Job | In my lab |
|---|---|---|
| **Agent** | Reads logs on the watched machine and sends them on | Windows VM |
| **Manager** | Receives events, matches rules, makes alerts | Ubuntu VM |
| **Indexer** | Stores alerts so they can be searched | Ubuntu VM |
| **Dashboard** | Shows alerts in the browser | Ubuntu VM, opened from Windows |

## What I ran

On the Wazuh server, I listed the ports that are listening:

```bash
sudo ss -tlnp | grep -E '1514|1515|55000|9200|443'
```

```text
LISTEN 0.0.0.0:443      node             (dashboard)
LISTEN 0.0.0.0:1514     wazuh-remoted    (agents send events here)
LISTEN 0.0.0.0:1515     wazuh-authd      (agents enroll here)
LISTEN 0.0.0.0:55000    python3          (Wazuh API)
LISTEN 127.0.0.1:9200   java             (indexer)
```

## What I learned

- Every part is a program listening on a port. If something breaks, check the port, then the program.
- The **indexer only listens on 127.0.0.1**. Only the Ubuntu VM itself can reach my stored alerts. Nothing else on the network can talk to it directly, which is good for security.
- The path of one alert: Windows writes an event, the agent sends it to port **1514**, the manager matches it to a rule, the alert goes into the indexer on **9200**, and the dashboard on **443** reads it through the API on **55000**.
