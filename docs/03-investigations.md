---
title: Part 3 - Investigation write-ups
---

# Part 3: Investigation write-ups

**Status: planned. No cases have been written yet; the outlines below are the plan.**

Each write-up follows one alert the lab produces by itself, using the same template.

## Template

1. **Summary:** one line with the verdict, either "Benign: expected user activity" or "Finding: needs hardening".
2. **Alert:** rule ID, level, description, time, agent, and a screenshot.
3. **Key fields:** a table of field, value, and what it means.
4. **Triage questions:** who, what, when, from where, and was it expected?
5. **Evidence checked:** related events within five minutes, parent process or logon type.
6. **Verdict and confidence.**
7. **Response and tuning:** what I would change (threshold, allow-list, level).
8. **ATT&CK mapping**, only where it applies.

## Case 1 (planned): a failed Windows logon followed by a success

- Alerts: Security event 4625 (default Wazuh rule 60122, failed logon), then 4624 (default rule 60106).
- Trigger: one mistyped password at the lock screen of my own lab VM, then a correct login. A single attempt, never repeated.
- Fields to explain: `logonType` (2 = interactive), `status` and `subStatus` (0xC000006A = wrong password), the target user (replaced with a demo value), and the source address (local).
- Expected verdict: benign, a typo. Tuning note: the rule for repeated failures is the one that matters at scale.

## Case 2 (planned): a failed configuration check on the endpoint

- Alert: a failed check from the Security Configuration Assessment (SCA) scan that Wazuh runs automatically against the endpoint.
- Pick one clear check, such as an account lockout policy or SMB signing.
- Angle: a configuration-risk finding, not an incident. Cover why the setting matters, the risk, the fix, and whether to accept it in a lab.
- Fallback: one of the [Part 2](02-detection-rules.md) alerts, triaged with its parent process chain.
