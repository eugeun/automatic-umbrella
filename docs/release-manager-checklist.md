# Release Manager Checklist

A practical, step-by-step checklist for planning and executing a production release. The Release Manager owns this checklist; however, PM, Dev leads, QA, and Support should all be familiar with it.

---

## 1. Release Planning & Scheduling

- [ ] Confirm release date and time window with PM, Dev lead, and DevOps
- [ ] Identify all stories, fixes, and features targeted for this release
- [ ] Verify that all targeted items have passed code review and are merged to the release branch
- [ ] Check for any open blockers or P0/P1 bugs that would delay the release
- [ ] Publish the release plan and communicate it to QA, Support, and key stakeholders
- [ ] Ensure rollback window is scheduled (e.g., team is on-call for N hours post-deploy)

---

## 2. Pre-Release Gating

### CI & Automated Tests
- [ ] All CI pipeline stages are green on the release branch
- [ ] Automated unit, integration, and E2E test suites pass with no unexpected failures
- [ ] Flaky-test failures have been investigated and ruled non-blocking (documented)
- [ ] Code coverage meets or exceeds the agreed threshold

### Security & Compliance
- [ ] Security scan (SAST/dependency audit) completed with no new critical/high findings
- [ ] Any known vulnerabilities have an accepted risk decision documented
- [ ] Compliance checks (licensing, data handling) passed

### Quality Sign-Off
- [ ] QA lead has signed off on regression results
- [ ] Acceptance criteria for all in-scope features verified
- [ ] No open P0 or P1 defects without a documented exception

### Release Notes & Communications
- [ ] Release notes drafted, reviewed, and approved
- [ ] Known issues and workarounds documented and shared with Support
- [ ] Feature flag configuration reviewed; flags set correctly for target audience

---

## 3. Deployment Steps

- [ ] Confirm deployment runbook is up to date and accessible
- [ ] Notify stakeholders and Support that deployment is starting
- [ ] Take a pre-deploy snapshot/backup of critical data stores (if applicable)
- [ ] Deploy to staging/pre-production and verify environment health
- [ ] Run smoke tests on staging; confirm all critical paths are functional
- [ ] Obtain final go/no-go from QA lead and Dev lead
- [ ] Execute production deployment following the runbook
- [ ] Monitor deployment progress; watch for pipeline errors or timeout alerts

---

## 4. Smoke Tests (Post-Deploy)

- [ ] Verify application is reachable and returns expected health-check response
- [ ] Confirm core user flows work end-to-end (login, main feature, data write/read)
- [ ] Check error rate and latency dashboards — no anomalous spikes
- [ ] Confirm new features or fixes are active for the target audience
- [ ] Validate feature flags are set as intended in production

---

## 5. Rollback Plan

- [ ] Rollback procedure is documented and rehearsed before go-live
- [ ] Rollback trigger criteria are agreed (e.g., error rate > X%, critical flow broken)
- [ ] DevOps is standing by and has access to execute rollback
- [ ] Decision authority is clear (who can call a rollback without escalation)
- [ ] Post-rollback verification steps documented

---

## 6. Communications

- [ ] Pre-release notification sent to stakeholders (timing, what's changing, any user impact)
- [ ] Support team briefed with release notes and known issues
- [ ] Deployment start and completion communicated to team channel
- [ ] Any user-facing downtime or degradation communicated via status page or in-app notice
- [ ] Post-deploy "all clear" message sent once smoke tests pass

---

## 7. Post-Release Review

- [ ] Schedule a brief post-release review within 48–72 hours
- [ ] Review any incidents or anomalies that occurred during or after deploy
- [ ] Collect feedback from Support on customer-reported issues
- [ ] Document lessons learned and action items in the retrospective log
- [ ] Update runbook and checklist with any process improvements identified
- [ ] Close the release milestone/epic in the project tracker

---

## Quick Reference: Roles & Responsibilities

| Step | Owner | Collaborators |
|---|---|---|
| Planning & scheduling | Release Manager | PM, Dev lead, DevOps |
| CI & test gating | QA Automation Engineer | QA lead, Release Manager |
| Security sign-off | Security / DevOps | Release Manager |
| Deployment execution | DevOps Engineer | Release Manager |
| Smoke tests | QA / Release Manager | Developers |
| Communications | Release Manager | PM, Support Specialist |
| Post-release review | Release Manager | PM, QA, Support, Dev lead |

---

*For role definitions, see [docs/octoacme-roles-and-personas.md](octoacme-roles-and-personas.md).*
