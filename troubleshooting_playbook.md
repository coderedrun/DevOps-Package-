# Troubleshooting Playbook — Real-World DevOps

## Purpose
A practical, step-by-step playbook for diagnosing and resolving production issues quickly and safely. Use as a single source-of-truth during incidents.

---

## Incident Response Roles
- **Incident Commander (IC)** — Owns coordination, communicates status.
- **Scribe** — Records timeline, actions, commands, and results.
- **Resolver(s)** — Engineers doing the debugging and fixes.
- **Communications** — Updates stakeholders/customers.
- **Postmortem Owner** — Ensures RCA and preventive actions.

---

## Runbook: Quick Triage (0–5 minutes)
1. **Acknowledge the alert.** IC takes ownership.
2. **Initial assessment:** Identify scope (region, service, user impact).
3. **Severity & priority:** Map to incident severity (P0/P1/P2).
4. **Stop changes:** Pause deployments and CI runs.
5. **Collect evidence:** Dashboard links, logs, recent deploy commit IDs, error messages.
6. **Communicate:** Open incident channel (Slack/MS Teams + PagerDuty).

---

## Common First Commands
- Kubernetes: `kubectl get pods -A`, `kubectl describe pod <pod> -n <ns>`, `kubectl logs -f <pod>`
- Linux: `top`, `dmesg`, `journalctl -u <service> -n 200`
- Docker: `docker ps`, `docker logs <container>`
- Cloud: `aws cloudwatch get-metric-statistics ...` (use console links when faster)

---

## Diagnosis Patterns
- **Resource exhaustion** — Check CPU/memory/disk. Metrics + `kubectl top nodes/pods`.
- **Networking** — DNS failures, routing, firewall; `nslookup`, `curl --resolve`, security groups.
- **Config error** — Missing env var, wrong secret; compare deployed config with expected.
- **Dependency failure** — Downstream DB/queue; test connectivity and health endpoints.
- **Traffic surge** — Autoscale limits; throttle or scale up.
- **Code bug/regression** — Find recent deploys, run canary diff, revert.

---

## Safe Remediation Steps
1. **If unknown cause & major impact:** Rollback to last known good.
2. **If resource constrained:** Scale out or increase resource limits temporarily.
3. **If config issue:** Patch config with a small change; restart relevant pods/services.
4. **If dependency failure:** Circuit-break or disable feature flag.
5. **If DB issue:** Promote read-replica, increase DB resources, rollback queries.

---

## Post-Incident
- Write timeline (minute-by-minute)
- Root cause & contributing factors
- Action items (owner + due date)
- Blameless RCA and follow-up verification
- Update runbooks and monitoring

---

## Playbook Annex: Examples
- High CPU: `kubectl top pods -n prod | sort -nrk3 | head`
- Pod CrashLoop: `kubectl describe pod <pod>` -> check events -> `kubectl logs --previous`
- Disk full: `ssh node && sudo du -sh /var/* | sort -rh | head`
- DB connection refused: `telnet db-host 5432` / `psql` test

---

## Checklist to Improve Preparedness
- Automated deploy freeze on incidents
- Canary and feature flags set up
- Synthetic monitoring for critical flows
- Runbooks for common outages
- Quarterly DR drill and postmortem review

