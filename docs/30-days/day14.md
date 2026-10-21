---
title: "Day 14: Tuning noise"
parent: "Week 2: Detection"
grand_parent: 30-Day Plan
nav_order: 14
---

# Day 14: Tuning noise

**Goal:** Make a noisy alert quieter without going blind.

## Read (15 minutes)

- [Rules XML syntax](https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/rules.html)

## Do

1. In Threat Hunting, find the rule that fires most often on `win10`.
2. Decide whether it is useful, too noisy, or both.
3. To lower a rule for one specific, known-good case, add a child rule with a lower level, keeping the original untouched:

```xml
<rule id="100140" level="0">
  <if_sid>RULE_ID_HERE</if_sid>
  <field name="win.eventdata.image" type="pcre2">(?i)known_good_program\.exe$</field>
  <description>Ignore known-good program</description>
</rule>
```

Replace `RULE_ID_HERE` and the image name. Level 0 means "match but do not alert".

## Check yourself

- What is the risk of suppressing too much?
- How would you know a suppression is still correct six months from now?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
