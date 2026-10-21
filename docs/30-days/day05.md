---
title: "Day 5: Anatomy of an alert"
parent: "Week 1: Foundations"
grand_parent: My 30-Day Journey
nav_order: 5
---

# Day 5: Anatomy of an alert

An alert is a pile of fields. Today I took one alert apart to see which fields answer which question.

## The alert I picked

My own rule `100100` (whoami). I pulled the newest one out of `alerts.json` and printed the interesting fields:

```text
rule 100100 5 Sysmon 1: whoami.exe executed by WINDOW\admin
mitre ['T1033'] ['Discovery']
agent win10 001
decoder windows_eventchannel
location EventChannel
image = C:\Windows\System32\whoami.exe
commandLine = "C:\WINDOWS\system32\whoami.exe" /groups
parentImage = C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
parentCommandLine = "C:\WINDOWS\system32\WindowsPowerShell\v1.0\PowerShell.exe"
user = WINDOW\admin
originalFileName = whoami.exe
```

## What each field answers

| Field | What it means | Question it answers |
|---|---|---|
| `rule.id`, `rule.level`, `rule.description` | Which rule fired, how serious, in words | What happened? |
| `rule.mitre.id` / `tactic` | Attacker technique (T1033) and its goal (Discovery) | What kind of behaviour is it? |
| `agent.name`, `agent.id` | Which machine | Where? |
| `decoder.name` | Which decoder read the raw log (`windows_eventchannel`) | How did Wazuh understand it? |
| `location` | Where the log came from (`EventChannel`) | Which log source? |
| `data.win.eventdata.image` | The program that ran | What ran? |
| `commandLine` | The exact command, with arguments (`/groups`) | How was it run? |
| `parentImage` | The program that started it (PowerShell) | What started it? |
| `user` | The account | Who? |
| `originalFileName` | Name inside the file, even if renamed | Is it really what it says? |

## What I learned

- Five questions a good alert can answer: **what, where, who, how, and what started it**.
- The **parent process** matters. `whoami` from a PowerShell I opened myself is normal. `whoami` spawned by a document or a web server would not be.
- **`originalFileName`** is why my rule matches on it instead of the file name: an attacker can rename `whoami.exe`, but not the name stored inside it.
- Windows alerts show backslashes doubled (`C:\\Windows`). It is JSON escaping, not a typo.
