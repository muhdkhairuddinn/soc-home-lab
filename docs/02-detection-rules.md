---
title: Part 2 - Detection rules
---

# Part 2: Detection rules

**Status: deployed and tested (2026-10-21).** Two custom rules fire on benign activity
generated on my own lab VM. Two other candidates turned out to be redundant with rules
that Wazuh already ships, so I dropped them. That finding is described below.

The deployed file is [`rules/soclab_rules.xml`](https://github.com/muhdkhairuddinn/soc-home-lab/blob/main/rules/soclab_rules.xml)
(`/var/ossec/etc/rules/soclab_rules.xml`, loaded after `wazuh-analysisd -t` passed and
`wazuh-manager` was restarted).

## Design

- Rules chain off the default Wazuh Sysmon rule for process creation (Sysmon event 1,
  parent rule `61603`, confirmed in `/var/ossec/ruleset/rules/0595-win-sysmon_rules.xml`).
- Matching uses `originalFileName`, so a renamed binary is still caught.
- Each trigger is a built-in Windows command on my own lab VM. Nothing touches another
  machine, downloads anything, or changes privileges, and each change was undone right after.

## Results

| Rule ID | Level | Detects | ATT&CK | Result |
|---|---|---|---|---|
| 100100 | 5 | `whoami.exe` execution | T1033 System Owner/User Discovery | Fired |
| 100102 | 7 | Scheduled task created with `schtasks.exe /create` | T1053.005 Scheduled Task | Fired |
| (100101) | - | PowerShell started with an encoded command | T1059.001, T1027 | Dropped: default rule 92057 already fires (level 12) |
| (100103) | - | Value written under a `Run` registry key | T1547.001 | Dropped: default rules 92302 (level 6) and 92041 (level 10) already fire |

### 100100: whoami.exe

```xml
<rule id="100100" level="5">
  <if_sid>61603</if_sid>
  <field name="win.eventdata.originalFileName" type="pcre2">(?i)^whoami\.exe$</field>
  <description>Sysmon 1: whoami.exe executed by $(win.eventdata.user)</description>
  <mitre><id>T1033</id></mitre>
</rule>
```

Why: user discovery is one of the first things run on a new host. On its own it is
common admin activity, so the level is low and it is mainly context.

Trigger: `whoami /all`

Alert (user redacted): `level 5, "Sysmon 1: whoami.exe executed by <host>\<user>", id 100100`

### 100102: scheduled task creation

```xml
<rule id="100102" level="7">
  <if_sid>61603</if_sid>
  <field name="win.eventdata.originalFileName" type="pcre2">(?i)^schtasks\.exe$</field>
  <field name="win.eventdata.commandLine" type="pcre2">(?i)/create</field>
  <description>Sysmon 1: scheduled task created with schtasks.exe</description>
  <mitre><id>T1053.005</id></mitre>
</rule>
```

Why: scheduled tasks are a common way to keep something running after a reboot.

Trigger, then clean up:

```powershell
schtasks /create /tn LabDemoTask /tr notepad.exe /sc once /st 23:59 /f
schtasks /delete /tn LabDemoTask /f
```

Alert: `level 7, "Sysmon 1: scheduled task created with schtasks.exe", id 100102`

## What I learned: check the default ruleset first

I drafted four rules. After deploying them and triggering each behaviour, only two fired.
For the other two, the alert list showed a **default** rule had already matched:

| Behaviour | Default Wazuh rule that fired |
|---|---|
| Encoded PowerShell command | 92057, level 12, "Powershell.exe spawned a powershell process which executed a base64 encoded command" |
| Value written to a Run key | 92302, level 6, "Registry entry to be executed on next logon was modified using command line application reg.exe"; 92041, level 10, "Value added to registry key has Base64-like pattern" |

A custom rule that duplicates a default one adds noise without adding coverage, so I
removed both. I found this by searching the default ruleset for the same patterns
(`0800-sysmon_id_1.xml` already matches `-encodedcommand`) and then confirming with real
alerts.

**Takeaway:** before writing a detection, look for what the platform already covers, then
add rules only for the gaps. Both surviving rules fill gaps: the default ruleset has no
alert for plain `whoami` or for `schtasks /create`.

## Validation

- [x] Parent rule ID confirmed on the server (`61603`).
- [x] `wazuh-analysisd -t` passed; `wazuh-manager` restarted and `active`; agent still `Active`.
- [x] Each remaining rule fired once on its trigger.
- [x] Test artifacts removed (scheduled task deleted; Run values deleted).
- [ ] Dashboard screenshots of the two alerts (to add).
- [ ] `wazuh-logtest` output for each rule (to add).

## Next

[Part 3: Investigation write-ups](03-investigations.md)
