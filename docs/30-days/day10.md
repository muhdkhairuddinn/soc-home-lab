---
title: "Day 10: Write a decoder"
parent: "Week 2: Detection"
grand_parent: 30-Day Plan
nav_order: 10
---

# Day 10: Write a decoder

**Goal:** Teach Wazuh to read a log format it has never seen.

## Read (15 minutes)

- [Decoders XML syntax](https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/decoders.html)

## Do

Pretend you have an app that writes this line:

```text
2026-10-21 14:00:00 myapp: login failed for user=khai from=10.10.10.50
```

Add to `/var/ossec/etc/decoders/local_decoder.xml`:

```xml
<decoder name="myapp">
  <prematch>^\d+-\d+-\d+ \d+:\d+:\d+ myapp: </prematch>
</decoder>
<decoder name="myapp-login">
  <parent>myapp</parent>
  <regex>login failed for user=(\S+) from=(\S+)</regex>
  <order>user,srcip</order>
</decoder>
```

Add a rule that uses it:

```xml
<rule id="100120" level="5">
  <decoded_as>myapp</decoded_as>
  <match>login failed</match>
  <description>myapp: login failed for $(user)</description>
</rule>
```

Paste the line into `wazuh-logtest` and check that `user` and `srcip` are filled in.

## Check yourself

- Which phase of logtest showed your fields?
- What would break if the log format changed slightly?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
