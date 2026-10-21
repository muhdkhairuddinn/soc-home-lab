---
title: "Day 11: Correlation: many failures in a short time"
parent: "Week 2: Detection"
grand_parent: 30-Day Plan
nav_order: 11
---

# Day 11: Correlation: many failures in a short time

**Goal:** Alert on a pattern, not on a single event.

## Read (15 minutes)

- [Rules XML syntax](https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/rules.html)

## Do

One failed login is noise. Several in a row is worth a look. Wazuh can count matches of an earlier rule:

```xml
<rule id="100130" level="10" frequency="3" timeframe="120">
  <if_matched_sid>60122</if_matched_sid>
  <same_field>win.eventdata.targetUserName</same_field>
  <description>3 failed logons for the same account within 2 minutes</description>
</rule>
```

Deploy it like Day 9. To test, make 4 wrong-password attempts against your own lab account from the Windows VM, spaced a few seconds apart.

Careful: Windows can lock an account after too many bad attempts. Four is safe on a default setup, but do not spam it.

## Check yourself

- Did your rule fire at the 3rd failure or the 4th?
- Compare with the built-in rules in the same family. Which one would you rely on?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
