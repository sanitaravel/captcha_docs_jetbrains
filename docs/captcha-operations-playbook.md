# CAPTCHA Operations Playbook

## Playbook Goal

This playbook describes what support and operations teams should do when CAPTCHA activity increases or when users report unexpected CAPTCHA prompts.

For trigger definitions, see [CAPTCHA Trigger Rules](./captcha-trigger-rules.md).

## Fast Triage Checklist

Use this checklist first:

1. Identify active reason codes (R1-R5) in monitoring/logs.
2. Check whether the spike is localized (single IP/payload) or broad (hourly anomaly).
3. Validate whether known business events explain traffic changes.
4. Assess potential user impact (volume of complaints, conversion drops, region/account concentration).
5. Decide whether to maintain, narrow, or remove manual controls.

## Rule-By-Rule Response Guidance

### If R1 (High Requests From One IP) Is Dominant

- Confirm whether the source IP belongs to trusted infrastructure.
- If trusted, open an investigation for rate-control or retry misconfiguration.
- If untrusted, maintain CAPTCHA and monitor for spread to new IPs.

### If R2 (Blacklisted IP) Is Dominant

- Verify blacklist accuracy and recency.
- If legitimate traffic is affected, open a blacklist review ticket.
- Document temporary mitigations for support handling.

### If R3 (Hourly Spike) Is Dominant

- Check release calendar, campaigns, and external traffic drivers.
- Correlate with error rates and latency.
- Escalate to incident response if abuse indicators are confirmed.

### If R4 (Repeated Payload) Is Dominant

- Review payload fingerprints and request patterns.
- Distinguish bot replay from legitimate client retries.
- Coordinate with application team if duplicate submission defects are possible.

### If R5 (Manual Enablement) Is Active

- Confirm owner and incident context.
- Define review timebox and exit criteria.
- Keep support teams informed while control is active.

## Manual Enablement Workflow

1. Confirm incident criteria and scope (endpoint, route, region, or segment).
2. Enable CAPTCHA from admin panel for the minimum required scope.
3. Log activation details: owner, time, reason, expected duration.
4. Monitor impact for both abuse reduction and user friction.
5. Review at predefined checkpoints and disable when criteria are met.

## Placeholder: Admin Panel Screenshot

> Image placeholder: "Manual CAPTCHA enablement in admin panel"
>
> Description for screenshot:
> Show admin controls where CAPTCHA is toggled, including scope selector, reason field, and save/confirm action.

## Escalation Matrix

| Scenario                    | Primary Team | Escalate To          | Action Timeframe  |
|-----------------------------|--------------|----------------------|-------------------|
| Suspected large-scale abuse | Operations   | Incident Response    | Immediate         |
| Confirmed false positives   | Support      | Product + Operations | Same business day |
| Blacklist dispute           | Support      | Security/Trust team  | Same business day |
| Repeated payload anomalies  | Operations   | Application team     | Within 4 hours    |

## Communications Template (Internal)

```text
Subject: CAPTCHA Increase Observed - [Rule ID]

Summary:
- Start time:
- Dominant rule(s):
- Scope affected:
- User impact estimate:

Actions Taken:
- [Action 1]
- [Action 2]

Next Review Time:
- [Timestamp]
```

## Related References

- [CAPTCHA Trigger Rules](./captcha-trigger-rules.md)
- [Glossary](./glossary-of-terms.md)
- [Index](./index.md)

## Change Log

| Date       | Change                   | Author             |
|------------|--------------------------|--------------------|
| 2026-03-14 | Initial glossary created | Documentation Team |
