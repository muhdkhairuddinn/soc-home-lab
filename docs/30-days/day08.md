---
title: "Day 8: Rules and decoders, and testing with logtest"
parent: "Week 2: Detection"
grand_parent: 30-Day Plan
nav_order: 8
---

# Day 8: Rules and decoders, and testing with logtest

**Goal:** Run a log line through Wazuh by hand and see which decoder and rule match.

## Read (15 minutes)

- [Ruleset](https://documentation.wazuh.com/current/user-manual/ruleset/index.html)
- [Testing rules and decoders](https://documentation.wazuh.com/current/user-manual/ruleset/testing.html)

## Do

Built-in rules live in `/var/ossec/ruleset/rules/`. Never edit them. Your own rules go in `/var/ossec/etc/rules/` and use IDs from 100000 upward.

Start the test tool and paste a sample log line (this one is made up, it is not a real login):

```bash
sudo /var/ossec/bin/wazuh-logtest
```

```text
Oct 21 14:00:01 Admin sshd[1234]: Failed password for invalid user test from 10.10.10.99 port 5555 ssh2
```

Read the three phases it prints: pre-decoding, decoding, filtering (the rule that matched). Press Ctrl+C to exit.

## Check yourself

- Which decoder and which rule matched?
- What fields did the decoder pull out of the line?

Screenshot this output. It is the `wazuh-logtest` proof that Part 2 of the lab still needs.

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
