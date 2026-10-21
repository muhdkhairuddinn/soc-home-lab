---
title: Cheat sheet
parent: My 30-Day Journey
nav_order: 1
---

# Cheat sheet

## Wazuh server (Ubuntu)

```bash
sudo systemctl status wazuh-manager wazuh-indexer wazuh-dashboard --no-pager
sudo systemctl restart wazuh-manager
sudo /var/ossec/bin/agent_control -l                  # list agents
sudo /var/ossec/bin/wazuh-analysisd -t                # test rules and decoders
sudo /var/ossec/bin/wazuh-logtest                     # try a log line
sudo tail -f /var/ossec/logs/ossec.log                # Wazuh's own log
sudo tail -n 1 /var/ossec/logs/alerts/alerts.json     # newest raw alert
```

## Where things live

| What | Path |
|---|---|
| Your rules | `/var/ossec/etc/rules/` |
| Your decoders | `/var/ossec/etc/decoders/` |
| Built-in rules (do not edit) | `/var/ossec/ruleset/rules/` |
| Manager config | `/var/ossec/etc/ossec.conf` |
| Windows agent config | `C:\Program Files (x86)\ossec-agent\ossec.conf` |

## Windows agent (PowerShell as Administrator)

```powershell
Get-Service WazuhSvc
Restart-Service WazuhSvc
Get-Content "C:\Program Files (x86)\ossec-agent\ossec.log" -Tail 20
```

## Useful numbers

| Number | Meaning |
|---|---|
| 1514 | Agents send events to the server |
| 1515 | Agents enroll |
| 55000 | Wazuh API |
| 4624 / 4625 | Windows logon success / failure |
| Rule 60122 | Windows logon failure |
| Rules 100000+ | Your custom rules |
| Level 0 | Match, but no alert |
