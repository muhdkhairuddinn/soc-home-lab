---
title: "Day 7: Week 1 review"
parent: "Week 1: Foundations"
grand_parent: My 30-Day Journey
nav_order: 7
---

# Day 7: Week 1 review

## The path of one event

Take one `whoami` on the Windows VM:

| Step | Who | What happens | Where I saw it |
|---|---|---|---|
| 1 | Windows + Sysmon | Sysmon writes event 1 (process created) | Sysmon log |
| 2 | Agent (`WazuhSvc`) | Reads the log, sends it on port **1514** | `ossec.log` on Windows (Day 3) |
| 3 | Manager | Decodes it (`windows_eventchannel`), rule `61603` matches, then `100100` | Rules page (Day 2) |
| 4 | Manager | Writes the alert to `alerts.json` | `/var/ossec/logs/alerts` (Day 4) |
| 5 | Indexer (port 9200) | Stores it so it can be searched | Day 1 |
| 6 | Dashboard (port 443) | Shows it in Threat Hunting through the API (55000) | Day 2 |

## Ports and files to remember

| Port | Job |
|---|---|
| 1514 | Agents send events |
| 1515 | Agents enroll |
| 55000 | API |
| 9200 | Indexer (local only) |
| 443 | Dashboard |

| Where | What |
|---|---|
| `/var/ossec/logs/alerts/alerts.json` | Alerts |
| `/var/ossec/logs/ossec.log` | Wazuh's own log |
| `/var/ossec/etc/ossec.conf` | Main config |
| `/var/ossec/etc/rules/` | My own rules |

## Words I now know

- **Agent / manager / indexer / dashboard**: the four parts.
- **Event vs alert**: an event is any log line, an alert is an event that matched a rule at a high enough level.
- **Keep alive**: the agent's heartbeat.
- **Level**: 0 to 15. Below `log_alert_level` (3), nothing is stored.
- **Parent process**: what started the program.

## Week 1 in one sentence

Wazuh is four programs on four ports that turn log lines into alerts, and every step of that path leaves a file or a page I can look at.

Next week: writing my own rules, decoders and correlation.
