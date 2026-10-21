---
title: "Day 4: Where Wazuh keeps its logs"
parent: "Week 1: Foundations"
grand_parent: 30-Day Plan
nav_order: 4
---

# Day 4: Where Wazuh keeps its logs

**Goal:** Find the alert file and read one raw alert.

## Read (15 minutes)

- [Log data collection](https://documentation.wazuh.com/current/user-manual/capabilities/log-data-collection/index.html)

## Do

On the Wazuh VM:

```bash
sudo ls /var/ossec/logs
sudo tail -n 1 /var/ossec/logs/alerts/alerts.json | python3 -m json.tool
sudo tail -n 20 /var/ossec/logs/ossec.log
```

- `alerts/alerts.json` has alerts only (events that matched a rule).
- `ossec.log` is Wazuh's own log. Look here when something is broken.
- Every event, even ones that matched nothing, is stored only if you turn on `<logall>`. That fills the disk fast, so turn it on briefly, look, and turn it off again.

## Check yourself

- What is the difference between an event and an alert?
- Which file do you check first if the agent shows Disconnected?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
