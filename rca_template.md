# RCA (Root Cause Analysis) Template

## Title
A short descriptive title for the incident.

## Incident ID
Unique identifier (e.g., INC-2025-00123)

## Date & Time
- **Start:** YYYY-MM-DD HH:MM (UTC+5:30)
- **End:** YYYY-MM-DD HH:MM (UTC+5:30)
- **Duration:** hh:mm

## Impact
- Services affected
- Customers impacted
- Pages / errors / financial impact (if known)

## Summary (1–2 lines)
Concise summary of what happened.

## Timeline
Minute-by-minute timeline with timestamps, actors, and actions.

Example:
- 01:23 — Alert fired: high 5xx rate on /api/orders (PagerDuty)
- 01:25 — IC opened incident channel; deployments frozen
- 01:30 — Identified bad deploy (commit abc123)
- 01:35 — Rolled back to previous image (image:v1.4.2)

## Root Cause
Explain the underlying technical reason.

## Contributing Factors
List process/people/tools that contributed (e.g., missing test, lack of validation).

## Corrective Actions Taken
Short-term fixes applied (who, when).

## Preventive Actions / Long-term Fixes
- Action description — Owner — Due date — Verification steps

## Severity & Lessons Learned
- Severity (P0/P1/P2) and reasoning
- What we learned

## Verification/Monitoring
How we'll verify the fix works (synthetic tests, dashboards).

## Attachments
Links to dashboards, logs, PRs, change requests.

