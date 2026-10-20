# My Home SOC Lab

I built a tiny security operations center on my own PC, broke a few things on the way,
fixed them, and wrote it all down so you don't have to suffer the same way.

![Lab network](docs/images/network-diagram.svg)

## What is it?

Three virtual machines in an isolated network:

- **Wazuh** (Ubuntu): the "brain" that collects logs and shouts when something looks odd.
- **Windows + Sysmon**: the machine being watched. Sysmon tells Wazuh everything it does.
- **Kali**: the third machine on the lab network.

I run harmless commands on the Windows VM and watch what Wazuh says about them.

## Proof it works

Two custom detection rules I wrote, firing in the Wazuh dashboard:

![My two custom rules firing](docs/images/wazuh-custom-rule-alerts.png)

| Rule | Catches | MITRE ATT&CK |
|---|---|---|
| 100100 | `whoami.exe` running | T1033 |
| 100102 | A scheduled task being created | T1053.005 |

## Plot twist

I wrote four rules. Only two were worth keeping. For the other two, Wazuh **already had
built-in rules** that fired first, so mine were just noise. I deleted them and wrote down
why. Lesson: check what the tool already does before reinventing it.

## The journey

| Part | What | Status |
|---|---|---|
| 1 | [Lab setup](docs/01-lab-setup.md) | Working and documented |
| 2 | [Detection rules](docs/02-detection-rules.md) | In progress: rules work, logtest output still to add |
| 3 | [Investigation write-ups](docs/03-investigations.md) | Coming soon |
| 4 | [Lessons learned (aka things that broke)](docs/04-lessons-learned.md) | Written, grows as I break more stuff |

## Built with

VirtualBox, Ubuntu 22.04, Wazuh 4.14.9, Sysmon with the SwiftOnSecurity config, Kali Linux.

No passwords or keys are in this repo. The lab network (`10.10.10.0/24`) only exists
inside my PC.
