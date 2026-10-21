---
title: "Day 23: Investigate a process alert"
parent: "Week 4: SOC work"
grand_parent: 30-Day Plan
nav_order: 23
---

# Day 23: Investigate a process alert

**Goal:** Trace a process back to what started it.

## Do

Open your `whoami` alert (rule `100100`) and read:

- `image` and `commandLine`: what ran.
- `parentImage` and `parentCommandLine`: what started it.
- `user`: under which account.
- `hashes`: look the hash up on a public reputation site if it is unfamiliar. Never upload private files.

Then run `whoami` from a different parent (PowerShell, then `cmd`, then the Run box) and compare the parent fields.

## Check yourself

- Why does the parent process matter more than the command itself?

## My notes

_Fill this in after you do it: what worked, what broke, and a screenshot._
