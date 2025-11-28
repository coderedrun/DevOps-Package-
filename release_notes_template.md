# Release Notes Template

## Release: <project/name> — Version x.y.z
**Date:** YYYY-MM-DD

### Overview
A one-paragraph summary of the release purpose.

### New Features
- Feature A — short description
- Feature B — short description

### Improvements
- Performance improvement for X (describe)

### Bug Fixes
- Fixed: issue with Y causing Z

### Deployment Notes
- Pre-requisites (DB migrations, feature flags)
- Rollout strategy (canary → 10% → 50% → 100%)
- Downtime expected: none / 5 minutes

### Rollback Steps
- Command / link to ArgoCD rollback
- Database rollback notes (if any)

### Verification Steps (Post-deploy)
- Health endpoint check
- Key transactions (purchase flow) smoke test

### Known Issues
- Issue1 — workaround

### Contacts
- On-call team, owner, Slack channel

