# Glossary of Terms

**Team:** CAPTCHA Documentation

## Core Security Terms

- CAPTCHA
	- A challenge shown to users to help distinguish legitimate human activity from automated traffic.
- Blacklist
	- A maintained list of IP addresses or sources previously identified as high risk.
- False Positive
	- A legitimate user flow that is mistakenly treated as suspicious and challenged by CAPTCHA.

## Traffic and Request Analysis Terms

- IP Address
	- A network address associated with the source of a request. Multiple users can sometimes share the same public IP.
- Payload
	- The request content sent to the service, such as form fields or JSON data.
- Hour Bucket
	- A one-hour time segment (for example, 14:00-14:59) used for traffic comparison and trend detection.
- Baseline Average (2 Weeks)
	- The average request volume observed over the previous two weeks, used as normal reference behavior.

## Operations and Reporting Terms

- Reason Code
	- A short identifier that maps CAPTCHA activation to a specific rule (for example, R1-R5).

## Related References

- [Index](./index.md)
- [CAPTCHA Trigger Rules](./captcha-trigger-rules.md)
- [CAPTCHA Operations Playbook](./captcha-operations-playbook.md)

## Change Log

| Date       | Change                   | Author             |
|------------|--------------------------|--------------------|
| 2026-03-14 | Initial glossary created | Documentation Team |
