---
title: Part 1 - Lab setup
---

# Part 1: Lab setup

## Architecture

![Lab network](images/network-diagram.svg)

| VM | Role | Resources |
|---|---|---|
| Ubuntu 22.04 Desktop | Wazuh 4.14.9 (manager, indexer, dashboard) | 8 GB RAM, 4 vCPU, 60 GB disk |
| Windows | Monitored endpoint: Sysmon and Wazuh agent | 6-8 GB RAM, 4 vCPU |
| Kali Linux | Third machine on the lab network | 4 GB RAM, 2 vCPU |

Each VM has two adapters: **Adapter 1 NAT** for internet through the host, and
**Adapter 2 NAT Network `SOCLab`** (`10.10.10.0/24`) for isolated lab traffic.

## 1. Network

```powershell
VBoxManage natnetwork add --netname SOCLab --network "10.10.10.0/24" --enable --dhcp on
VBoxManage modifyvm "<vm>" --nic1 nat --nic2 natnetwork --nat-network2 SOCLab
```

## 2. Wazuh server

```bash
sudo apt install -y curl
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

The installer runs the indexer, manager, Filebeat and dashboard in sequence:

![Wazuh install progress](images/wazuh-install-progress.png)

## 3. Windows endpoint

Sysmon with the SwiftOnSecurity configuration:

![Sysmon running and connectivity to Wazuh](images/windows-sysmon-running.png)

Wazuh agent pointed at the manager, installed from the MSI:

![Wazuh agent installed](images/windows-agent-installed.png)

The agent is told to read the Sysmon event channel by adding a `localfile`
block to `ossec.conf`:

```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

![Sysmon log collection in ossec.conf](images/windows-sysmon-log-config.png)

## 4. Verification

On the Wazuh server:

```bash
sudo /var/ossec/bin/agent_control -l
```

![Agent list showing the Windows agent as Active](images/wazuh-agents-active.png)

The Windows agent (`win10`) reports `Active`.

From the Kali VM, the Wazuh server is reachable on the lab network:

![Kali pinging Wazuh](images/kali-ping-wazuh.png)

## Next

[Part 2: Detection rules](02-detection-rules.md) (2 rules tested).
