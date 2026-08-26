# ROADMAP
 
Build order: **phase00 first** (everything else depends on it) → phases
01–08 in any order → **phase09 last** (needs real tools from earlier phases
to assemble into one capstone flow).
 
Status legend: `not started` / `in progress` / `done`.
5-artifact = break, fix, harden, test-log.md, postmortem.md all present for
that implementation.
 
## phase00 — Toolkit Meta (build first)
 
| Component | Language | Status |
|---|---|---|
| tool-template | bash | not started |
| self-test-harness | bash | not started |
| cli-framework | python | not started |
| logging-config | python | not started |
| test-harness | python | not started |
| packaging (pyproject entry_points) | python | not started |
| ci-pipeline (ruff+mypy+pytest) | python | not started |
 
## phase01 — Monitoring and Alerting *(read-only phase — no security review required)*
 
| Tool | Bash | Python | 5-artifact | Review required? |
|---|---|---|---|---|
| disk-usage-monitor | planned | planned | not started | no |
| service-health-check | planned | planned | not started | no |
| log-error-watcher | planned | planned | not started | no |
| cert-expiry-checker | — | planned | not started | no |
| multi-host-check-runner | — | planned | not started | no (README must address credential handling) |
 
## phase02 — Backup and Recovery
 
| Tool | Bash | Python | 5-artifact | Review required? |
|---|---|---|---|---|
| config-backup | planned | planned | not started | no |
| database-dump-rotate | planned | planned | not started | **yes** |
| restore-verification | planned | planned | not started | **yes** |
| backup-manifest-tracker | — | planned | not started | no |
 
## phase03 — User and Access Management
 
| Tool | Bash | Python | 5-artifact | Review required? |
|---|---|---|---|---|
| bulk-user-provision | planned | planned | not started | **yes** |
| access-review-report | planned | planned | not started | no |
| offboarding-lockdown | planned | planned | not started | **yes** |
| ssh-key-audit | planned | planned | not started | no |
 
## phase04 — Log Analysis and Forensics *(read-only phase — no security review required)*
 
| Tool | Bash | Python | 5-artifact | Review required? |
|---|---|---|---|---|
| auth-log-anomaly-scan | planned | planned | not started | no |
| log-normalizer | — | planned | not started | no |
| timeline-builder | planned | planned | not started | no |
| log-integrity-check | planned | planned | not started | no |
 
## phase05 — System Audit and Compliance
 
| Tool | Bash | Python | 5-artifact | Review required? |
|---|---|---|---|---|
| baseline-drift-detector | planned | planned | not started | no |
| package-inventory-diff | planned | planned | not started | no |
| cis-benchmark-subset | planned | planned | not started | no (yes if auto-remediate mode added) |
| config-compliance-check | planned | planned | not started | no (yes if fix/rewrite mode added) |
 
## phase06 — Deployment and Automation
 
| Tool | Bash | Python | 5-artifact | Review required? |
|---|---|---|---|---|
| idempotent-service-deploy | planned | planned | not started | **yes** |
| rolling-restart | planned | planned | not started | **yes** |
| pre-flight-check | planned | planned | not started | no |
| rollback-wrapper | planned | planned | not started | **yes** |
 
## phase07 — Incident Response Tooling
 
| Tool | Bash | Python | 5-artifact | Review required? |
|---|---|---|---|---|
| evidence-collector | planned | planned | not started | no (explicitly read-only by design) |
| isolate-host | planned | planned | not started | **yes** |
| quick-triage | planned | planned | not started | no |
| postmortem-scaffold-generator | — | planned | not started | no |
 
## phase08 — Performance and Capacity *(read-only phase — no security review required)*
 
| Tool | Bash | Python | 5-artifact | Review required? |
|---|---|---|---|---|
| resource-baseline-capture | planned | planned | not started | no |
| anomaly/slow-query-flagger | planned | planned | not started | no |
| capacity-trend-report | — | planned | not started | no |
 
## phase09 — Capstone (build last)
 
| Component | Notes | Status |
|---|---|---|
| Integrated incident-response flow | bash evidence-collector → python quick-triage/isolate-host → python postmortem-scaffold-generator | not started |
 
---
 
**Total flagged for mandatory security review: 8 tools**
(database-dump-rotate, restore-verification, bulk-user-provision,
offboarding-lockdown, idempotent-service-deploy, rolling-restart,
rollback-wrapper, isolate-host) — reviewed independently per implementation,
both bash and python.
 
**Conditionally flagged: 2 tools** (cis-benchmark-subset,
config-compliance-check) — becomes mandatory only if a
remediation/fix-writing mode is added to either.
