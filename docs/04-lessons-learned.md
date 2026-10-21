---
title: Part 4 - Lessons learned
---

# Part 4: Lessons learned

What this lab taught me about security monitoring.

## 1. Look at what the tool already detects

I wrote four detection rules. Wazuh already shipped rules for two of them
([Part 2](02-detection-rules.md)). Before writing a rule, search the existing ruleset.
Only fill real gaps, because duplicate rules just add noise.

## 2. Alert level is not the same as "attack"

`whoami` is level 5 on purpose. Attackers run it, but so do admins. A SOC needs
low-level clues that become interesting only when combined with other events. A level-12
alert for every `whoami` would train analysts to ignore the dashboard.

## 3. Logs only help if the right ones are on

Windows does not log process creation in detail by default. Sysmon fixed that. Without it,
rules 100100 and 100102 could not exist. Check what telemetry you collect before
promising any detection.

## 4. Test every rule, then clean up

A rule you never triggered is a guess. I fired each rule with a harmless built-in command,
confirmed the alert, then removed the test artifacts (the scheduled task, the test
registry value). The two rules that never fired showed me the built-in ones were already
catching those events.

## 5. Map detections to MITRE ATT&CK

Tagging rules with technique IDs (T1033, T1053.005) makes alerts easier to explain and
shows which attacker behaviors are covered and which are not.

## 6. Context decides whether an alert is bad

A failed login followed by a success from the same user and machine is usually a typo.
Fifty failures from one IP is a brute-force attempt. The same event type, very different
meaning. See [Part 3](03-investigations.md).

## 7. Isolate the lab

Each VM has an internet card and a second card on a private lab-only network. Anything
risky I test later stays off the home Wi-Fi.

## 8. Protect the monitoring system itself

The Wazuh dashboard holds every log from every machine. Its admin password stays out of
screenshots and out of the repo, and I check every image for secrets before publishing.
