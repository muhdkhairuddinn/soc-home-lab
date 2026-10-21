---
title: "Day 27: Backups and maintenance"
parent: "Week 4: SOC work"
grand_parent: 30-Day Plan
nav_order: 27
---

# Day 27: Backups and maintenance

**Goal:** Be able to rebuild the lab if it breaks.

## Do

1. Back up the files you changed:

```bash
sudo tar czf ~/wazuh-custom-backup.tar.gz /var/ossec/etc/rules /var/ossec/etc/decoders /var/ossec/etc/ossec.conf
```

2. Take a VM snapshot before risky changes (on the host):

```powershell
VBoxManage snapshot "Ubuntu Desktop" take "before-day-27"
```

3. Check how much disk the indexer uses: `df -h` and `sudo du -sh /var/lib/wazuh-indexer`.

## Check yourself

- Could you rebuild your rules from the backup alone?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
