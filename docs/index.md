---
title: Home SOC Lab
---

# Home SOC Lab

A small, isolated security-monitoring lab: a Wazuh SIEM, a Windows endpoint with
Sysmon, and a Kali VM, all on one PC with Oracle VirtualBox.

![Lab network](images/network-diagram.svg)

## Parts

1. [Lab setup](01-lab-setup.md): architecture, install, and verification
2. [Detection rules](02-detection-rules.md): custom Wazuh rules mapped to MITRE ATT&CK (2 rules tested)
3. [Investigation write-ups](03-investigations.md): triaging real alerts from the lab (planned)
4. [Lessons learned](04-lessons-learned.md): problems hit while building it

## Goal

Show the full loop of a SOC analyst's basics: collect endpoint logs, see them in
a SIEM, write detections, and explain what an alert means.
