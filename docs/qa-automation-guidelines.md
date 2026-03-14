# QA Automation Guidelines

Guidelines for QA Automation Engineers and the broader team on how to integrate automated testing into the CI pipeline effectively. Following these practices keeps the pipeline fast, reliable, and trustworthy.

---

## 1. Test Ownership

- **Every team owns its tests.** Developers write unit and integration tests alongside their code; QA Automation Engineers own the E2E suite and shared test utilities.
- Tests for a feature are committed in the same PR as the feature code. A PR without adequate tests should not be merged.
- QA Automation Engineers review test coverage during PR review and flag gaps before merge.
- The QA lead maintains a coverage dashboard and reviews it weekly with the team.

---

## 2. When to Write Which Test Type

| Test Type | Purpose | Owned By | When to Write |
|---|---|---|---|
| **Unit tests** | Test a single function or class in isolation | Developers | Alongside every code change |
| **Integration tests** | Test interactions between components or services | Developers + QA Automation | When a new service boundary or data flow is introduced |
| **Contract tests** | Verify API contracts between producer and consumer | Developers + QA Automation | When a shared API is added or changed |
| **E2E tests** | Validate complete user journeys in a real environment | QA Automation Engineer | For critical, high-risk, or regression-prone flows |
| **Performance/load tests** | Validate system behaviour under expected load | QA Automation + DevOps | Before major releases or after significant architecture changes |

**Guideline:** Prefer unit and integration tests over E2E tests where possible. E2E tests are slower, harder to maintain, and more likely to become flaky. Reserve them for flows that cannot be adequately covered at a lower level.

---

## 3. Flaky-Test Handling

Flaky tests erode trust in the pipeline and slow down delivery. Treat flakiness as a bug.

- **Detection:** Any test that fails intermittently (passes on re-run without a code change) is considered flaky.
- **Quarantine:** Flaky tests are immediately quarantined (moved to a non-blocking suite) and a bug is filed.
- **Target:** Flaky-test rate should stay below **2%** of the total test suite at all times.
- **Resolution SLA:** Quarantined tests must be fixed or deleted within **5 business days**.
- **Root cause:** Investigate whether flakiness is caused by test design (e.g., timing, shared state) or by an underlying product defect.
- **Escalation:** If a flaky test cannot be resolved within the SLA, escalate to the QA lead and Dev lead.

---

## 4. Coverage Expectations

- **Unit test coverage:** Minimum **80%** line coverage for all new code. Coverage reports are generated on every CI run.
- **Integration coverage:** All new service integrations must have at least one happy-path and one failure-path integration test.
- **E2E coverage:** All P0 (critical) user journeys must have an E2E test. P1 journeys are covered where E2E provides meaningful additional confidence.
- Coverage thresholds are enforced in CI — a build that drops below thresholds fails.
- Coverage is a floor, not a goal. High coverage with poor assertions is not acceptable.

---

## 5. PR Practices

- Include tests in every PR that changes application behaviour. PRs without tests require explicit justification in the PR description.
- Add the `needs-tests` label to any PR where tests are deferred and tracked in a follow-up issue.
- QA Automation Engineers are required reviewers on PRs that touch shared test utilities or the E2E suite.
- Test code is reviewed with the same rigour as production code — avoid duplicated logic, magic strings, and unclear assertions.
- Keep test names descriptive: `should return 404 when user does not exist` is better than `test_user`.

---

## 6. CI Pipeline Integration

### Pipeline Stages (in order)
1. **Build** — compile and package the application
2. **Unit tests** — fast; must pass before proceeding
3. **Integration tests** — run against test doubles or a local environment
4. **Security scan** — SAST and dependency audit
5. **E2E tests** — run against a deployed staging environment
6. **Performance tests** — run on demand or as part of release gates (not every PR)

### Pipeline Principles
- **Fail fast:** Unit tests run first so developers get quick feedback.
- **Parallelise:** Run independent test suites in parallel to minimise total pipeline time.
- **Isolate environments:** E2E tests run against a dedicated, stable staging environment — not shared with manual QA.
- **Artefact retention:** Keep test reports and coverage artefacts for at least 30 days for audit and trend analysis.
- **Branch protection:** The main branch requires a green pipeline before merging.

---

## 7. Handoffs with Developers

- **Story kickoff:** QA Automation Engineer joins to review acceptance criteria for testability. If a story cannot be tested automatically, flag it early.
- **During development:** Developers implement unit/integration tests. QA Automation is available for pairing on test design.
- **PR review:** QA Automation Engineer reviews test coverage and quality. Developer resolves any feedback before merge.
- **Post-merge:** QA Automation monitors CI results for any regressions introduced by the change.

---

## 8. Handoffs with DevOps

- **Environment provisioning:** QA Automation Engineer specifies test-environment requirements (data, config, services). DevOps provisions and maintains those environments.
- **Pipeline changes:** Any change to CI configuration that affects test stages requires a joint review by QA Automation and DevOps.
- **Flaky infrastructure:** If test failures are caused by environment instability (not test or code issues), DevOps owns remediation.
- **Release gating:** QA Automation provides the go/no-go signal on automated test results; DevOps executes the deployment once gates are met.

---

## 9. Quick Reference: Roles in Test Automation

| Activity | Primary Owner | Collaborators |
|---|---|---|
| Unit & integration tests | Developers | QA Automation (review) |
| E2E test suite | QA Automation Engineer | Developers, DevOps |
| CI pipeline test stages | DevOps Engineer | QA Automation, Developers |
| Coverage reporting | QA Automation Engineer | QA lead, PM |
| Flaky-test triage | QA Automation Engineer | Developers, DevOps |
| Release go/no-go (tests) | QA Automation Engineer | Release Manager, QA lead |

---

*For role definitions, see [docs/octoacme-roles-and-personas.md](octoacme-roles-and-personas.md).*  
*For the release process, see [docs/release-manager-checklist.md](release-manager-checklist.md).*
