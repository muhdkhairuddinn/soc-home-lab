---
title: "Day 6: The ossec.conf tour"
parent: "Week 1: Foundations"
grand_parent: 30-Day Plan
nav_order: 6
---

# Day 6: The ossec.conf tour

**Goal:** Know the main sections of the config and how to edit it safely.

## Read (15 minutes)

- [ossec.conf reference](https://documentation.wazuh.com/current/user-manual/reference/ossec-conf/index.html)

## Do

Always back up before editing:

```bash
sudo cp /var/ossec/etc/ossec.conf /var/ossec/etc/ossec.conf.bak
sudo grep -nE '^\s*<(global|alerts|remote|syscheck|rootcheck|sca|localfile|active-response|vulnerability-detection)' /var/ossec/etc/ossec.conf
```

Find these and note what each does: `<global>`, `<alerts>` (`log_alert_level`), `<remote>`, `<syscheck>`, `<sca>`, `<localfile>`, `<active-response>`.

After any manager config change, restart and check it came back:

```bash
sudo systemctl restart wazuh-manager
sudo systemctl status wazuh-manager --no-pager
```

## Check yourself

- Which setting decides the lowest alert level that gets stored?
- Where would you tell the server to read an extra log file?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
