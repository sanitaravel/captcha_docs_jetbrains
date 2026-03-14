# CAPTCHA Trigger Rules

## Article Goal

This article explains when the service displays CAPTCHA and how to interpret each trigger in plain operational language.

For response procedures, see [CAPTCHA Operations Playbook](./captcha-operations-playbook.md).

## Why CAPTCHA Is Conditional

CAPTCHA helps protect the service from abusive traffic and automated attacks. Showing it on every request can reduce user satisfaction and completion rates, so the service applies CAPTCHA only when risk signals are detected.

## Trigger Summary Table

| Rule ID | Trigger Condition                                       | Time Window          | Trigger Interpretation                            |
|---------|---------------------------------------------------------|----------------------|---------------------------------------------------|
| R1      | More than 500 requests from the same IP                 | Less than 20 minutes | Possible rapid automated activity from one source |
| R2      | Request IP is on blacklist                              | Immediate            | Source is already known as high risk              |
| R3      | Current hour traffic is more than 2x the 2-week average | Current hour bucket  | Potential service-wide spike or coordinated abuse |
| R4      | Same payload sent more than 5 times                     | Last 30 seconds      | Potential replay or scripted repeated submission  |
| R5      | CAPTCHA manually enabled via admin panel                | Admin-defined        | Defensive control activated by operations/admin   |

## Rule Details

### R1. High Request Volume From One IP

#### Condition

CAPTCHA is shown when more than 500 requests are received from the same IP address in less than 20 minutes.

#### What this usually indicates

A single source may be sending traffic at machine speed, which can indicate bot activity or aggressive scraping.

#### Operational notes

- Validate whether the IP belongs to trusted infrastructure (for example, a known gateway).
- If trusted, investigate whether a misconfiguration is causing request bursts.
- If untrusted, keep enhanced monitoring active.

#### Example scenario
A support analyst sees that users behind one public network are getting frequent CAPTCHA prompts. Logs show 700 requests from one IP in 12 minutes.

---

### R2. Blacklisted IP Address

#### Condition

CAPTCHA is shown when the request IP address is found in the blacklist.

#### What this usually indicates

The source was previously associated with abuse, policy violations, or known malicious behavior.

#### Operational notes

- Confirm the blacklist entry is still valid.
- Review whether this may affect legitimate users sharing the same outbound IP.
- Escalate blacklist review if false positives are suspected.

#### Example scenario

A recurring attack source reappears using the same IP range. CAPTCHA is automatically enforced at request time.

---

### R3. Hourly Traffic Spike Above Baseline

#### Condition

CAPTCHA is shown when the current hour receives more than double the average request volume for the same hour bucket over the last 2 weeks.

#### What this usually indicates

Traffic behavior is significantly above normal baseline and may represent abuse, automated campaigns, or an unexpected traffic event.

#### Operational notes

- Confirm whether a planned campaign or release can explain the spike.
- If no expected cause exists, initiate abuse triage.
- Compare error rates and user reports before making broader policy adjustments.

#### Example scenario

Average traffic for 10:00-10:59 over two weeks is 30,000 requests. Current 10:00-10:59 traffic reaches 65,000 requests, so CAPTCHA is activated by this rule.

---

### R4. Repeated Identical Payload

#### Condition

CAPTCHA is shown when the same payload is sent more than 5 times in the last 30 seconds.

#### What this usually indicates

The pattern resembles replay attempts or scripted form submissions using repeated content.

#### Operational notes

- Check if the repeated payload matches known automation signatures.
- Verify whether a client retry bug could produce duplicate submissions.
- Coordinate with application teams if benign retries are suspected.

#### Example scenario

The same form content is submitted 8 times in 20 seconds from multiple sessions, indicating likely automation.

---

### R5. Manual CAPTCHA Enablement

#### Condition

CAPTCHA is shown when enabled manually via admin panel for certain requests.

#### What this usually indicates

An authorized operator activated a temporary or targeted defensive control.

#### Operational notes

- Record who enabled the rule, when, and why.
- Define planned review time for disabling or narrowing scope.
- Communicate impact to support teams while active.

#### Example scenario

During an incident, operations enables CAPTCHA for a sensitive endpoint until attack traffic stabilizes.

## Related References

- [CAPTCHA Operations Playbook](./captcha-operations-playbook.md)
- [Glossary Of Terms](./glossary-of-terms.md)
