# Home SOC Lab: Wazuh, Sysmon and VirtualBox

A small, isolated security-monitoring lab built on one PC. A Wazuh SIEM collects
logs from a Windows endpoint running Sysmon, and a Kali VM sits on the same
isolated network.

![Lab network](docs/images/network-diagram.svg)

## Status

| Part | Topic | Status |
|---|---|---|
| 1 | [Lab setup](docs/01-lab-setup.md) | Working and documented |
| 2 | [Detection rules](docs/02-detection-rules.md) | In progress: 2 rules tested, evidence (screenshots, logtest) still to add |
| 3 | [Investigation write-ups](docs/03-investigations.md) | Planned |
| 4 | [Lessons learned](docs/04-lessons-learned.md) | Written, will grow as the lab does |

## What works today

- Wazuh 4.14.9 all-in-one (manager, indexer, dashboard) on Ubuntu 22.04.
- Windows endpoint with Sysmon and a Wazuh agent reporting as `Active`.
- Sysmon events forwarded to Wazuh through the agent `ossec.conf`.
- Two network adapters per VM: NAT for internet, and an isolated NAT Network
  (`10.10.10.0/24`) for lab traffic.

## Detection rules (deployed and tested)

Two custom rules for Sysmon events, each mapped to MITRE ATT&CK, both fired on benign
activity from my own lab VM. Two other candidates were dropped after testing showed the
default Wazuh ruleset already alerts on them.

| Rule | Detects | ATT&CK | Result |
|---|---|---|---|
| 100100 | `whoami.exe` execution | T1033 | Fired |
| 100102 | Scheduled task created with `schtasks.exe` | T1053.005 | Fired |

File: [`rules/soclab_rules.xml`](rules/soclab_rules.xml). Details and the redundancy finding: [Part 2](docs/02-detection-rules.md).

## Skills shown

Wazuh (SIEM) deployment, Sysmon, log collection and forwarding, network segmentation
in VirtualBox, Linux and Windows administration, troubleshooting, MITRE ATT&CK
mapping, and writing custom detection rules.

## Tech

Oracle VirtualBox 7.2.6, Ubuntu 22.04.5, Wazuh 4.14.9, Sysmon 15.22 with the
SwiftOnSecurity configuration, Kali Linux 2026.2.

## Notes

Passwords and keys are not stored in this repo. Lab addresses are private
(`10.10.10.0/24`) and only exist inside the host PC.
