# War-Room Simulation — Real Outage Practice

## Scenario Overview
- **Time:** 02:10 AM
- **Service:** Orders API (orders.example.com)
- **Symptoms:** 5xx spike, user checkouts failing (~70% errors), ~2000 requests/minute
- **Recent change:** New deployment 20 minutes ago (image: orders:v3.2.0)

## Incident Channel
- Create Slack channel: `#inc-orders-p0`
- IC: You (assign)
- Scribe: teammate A
- Resolvers: You + backend dev

## Initial Triage (First 10 minutes)
1. Acknowledge in PagerDuty.
2. Freeze deployments.
3. Collect evidence:
   - Grafana error rate graph
   - `kubectl get pods -n prod -l app=orders`
   - `kubectl logs -l app=orders --tail=200`
4. Quick hypothesis:
   - Bad code change, DB connection leak, or config/secret mismatch.

## Decision Point 1
**Option A:** Rollback to orders:v3.1.9 (fast action)  
**Option B:** Scale out pods and continue investigating (mitigate load)

**If you choose A (Rollback)**:
- Command: `kubectl set image deployment/orders orders=repo/orders:v3.1.9 -n prod`
- Verify: `kubectl rollout status deploy/orders -n prod`
- Check error rate; if back to normal, proceed with RCA on commit diff.

**If you choose B (Scale out)**:
- Command: `kubectl scale deployment orders --replicas=10 -n prod`
- Watch CPU/memory; if issues persist, rollback.

## Deep Debug (10–30 min)
- Check DB connection pool exhaustion: `kubectl exec -it pod -- netstat -anp | grep ESTABLISHED`
- Check for increased GC or memory: `kubectl top pod -n prod`
- Check recent config: compare ConfigMap and secrets with previous version.

## Decision Point 2
If rollback fixed: prepare PR for patch, add guardrails (config check), and promote hotfix process.

If rollback didn't fix: Check downstream (DB), network (NLB), and ingress.

## Communication
- Update status every 10 minutes in Slack and to stakeholders:
  - "Mitigating: rolling back to v3.1.9. Expected recovery in 5–10 mins."
- Share post-mortem ETA.

## Post Incident Tasks
- Run full test suite on canary environment
- Create feature-flag for new functionality
- Add pre-deploy canary and health checks
- Add synthetic transactions for checkout flow

## Learning Objectives for Simulation
- Practice coordination and role orchestration
- Practice safe rollback and verification
- Practice writing quick RCAs under pressure

