---
title: "Day 9: Write a rule"
parent: "Week 2: Detection"
grand_parent: 30-Day Plan
nav_order: 9
---

# Day 9: Write a rule

**Goal:** Write, test and fire one new rule end to end.

## Read (15 minutes)

- [Rules XML syntax](https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/rules.html)

## Do

Idea: alert when someone lists local accounts with `net user` (MITRE T1087.001). Add this to `/var/ossec/etc/rules/soclab_rules.xml`, inside the existing `<group>`:

```xml
<rule id="100110" level="5">
  <if_sid>61603</if_sid>
  <field name="win.eventdata.originalFileName" type="pcre2">(?i)^net1?\.exe$</field>
  <field name="win.eventdata.commandLine" type="pcre2">(?i)\suser(\s|$)</field>
  <description>Sysmon 1: local accounts listed with net user</description>
  <mitre><id>T1087.001</id></mitre>
</rule>
```

Then:

```bash
sudo /var/ossec/bin/wazuh-analysisd -t
sudo systemctl restart wazuh-manager
```

On the Windows VM run `net user` (it only lists accounts, nothing changes) and look for rule `100110`.

## Check yourself

- Did it fire once or twice? (`net.exe` can start `net1.exe`.)
- Would you keep this rule, or is a built-in one already catching it? Check before you decide.

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
