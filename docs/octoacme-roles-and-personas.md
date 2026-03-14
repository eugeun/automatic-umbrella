# OctoAcme Personas

This document defines typical roles and responsibilities used in OctoAcme project docs and exercises.

---

## Developers

### Role Summary
Developers design, build, test, and deliver software components. They collaborate with product and project leads to implement features that meet acceptance criteria and quality standards.

### Responsibilities
- Implement features and fixes to meet acceptance criteria
- Write and maintain tests and documentation
- Participate in design and code reviews
- Assist in estimating and planning work
- Help identify technical risks and propose mitigations

### Goals
- Deliver reliable, maintainable code
- Reduce cycle time from idea to production
- Maintain high test coverage and observability

### Typical Communication
- Daily standups and sprint planning
- PR descriptions and code review comments
- Technical design docs when needed

---

## Product Managers

### Role Summary
Product Managers define what should be built to deliver customer and business value. They own the product vision, prioritize the backlog, and measure outcomes.

### Responsibilities
- Define problem statements and success metrics
- Prioritize the roadmap and backlog
- Collaborate with stakeholders and engineering on trade-offs
- Validate solutions through user research and metrics

### Goals
- Maximize customer value and impact
- Make clear, data-driven prioritization decisions
- Ensure product-market fit and usability

### Typical Communication
- Weekly alignment with PM and engineering leads
- Roadmap updates and stakeholder briefings
- Acceptance criteria and feature specs

---

## Project Managers

### Role Summary
Project Managers coordinate delivery activities, manage schedules, risks, and communications. They enable the team to deliver on commitments efficiently.

### Responsibilities
- Create and maintain project plans and timelines
- Manage risks, dependencies, and resource constraints
- Facilitate meetings (kickoff, planning, retrospectives)
- Ensure consistent project documentation and status reporting
- Coordinate cross-team and stakeholder communication

### Goals
- Deliver projects on time and within scope
- Minimize unplanned work and escalations
- Maintain transparency and alignment across stakeholders

### Typical Communication
- Weekly status updates and stakeholder reports
- Risk registers and decision logs
- Coordination via project boards and meeting facilitation

---

---

## Release Manager

### Role Summary
Release Managers plan, coordinate, and oversee production releases. They own the end-to-end release process — from scheduling and gating to deployment and post-release review — ensuring that every release is safe, repeatable, and well-communicated.

### Responsibilities
- Define and maintain the release schedule in coordination with PM and development leads
- Gate releases on passing CI, automated tests, and security scans
- Coordinate deployment activities with DevOps and ensure rollback plans are in place
- Run smoke tests and confirm release health before closing a deploy
- Communicate release status to stakeholders, Support, and QA
- Lead post-release reviews and document lessons learned

### Interaction Matrix
| Collaborator | How they interact |
|---|---|
| Project Manager | Align on release windows and scope; escalate blockers |
| Developers | Review release readiness; coordinate hotfix windows |
| QA/Testing & QA Automation Engineer | Confirm test gates are met before promoting builds |
| DevOps Engineer | Coordinate deployment pipelines and rollback procedures |
| Support Specialist | Brief Support ahead of release; receive early post-release issue reports |
| Product Manager (PdM) | Align on feature flags and staged rollout decisions |

### Goals
- Ship reliably and predictably with minimal production incidents
- Make release status visible and easy to understand for all stakeholders
- Reduce mean time to recovery (MTTR) when issues occur

### Suggested Handoff Points
- **Start of sprint**: confirm which stories are targeted for the upcoming release
- **Feature freeze**: verify all items are merged and CI is green
- **Pre-deploy**: run the release checklist; get sign-off from QA and Dev leads
- **Post-deploy**: confirm smoke tests pass; hand off to Support for monitoring

---

## QA Automation Engineer

### Role Summary
QA Automation Engineers build and maintain the automated test infrastructure that enables fast, reliable CI pipelines. They partner closely with Developers and DevOps to ensure test coverage is adequate, tests are stable, and the pipeline provides a trustworthy quality gate.

### Responsibilities
- Design, implement, and maintain automated test suites (unit, integration, E2E)
- Define test coverage standards and ensure high-risk areas are well-covered
- Triage and resolve flaky tests promptly to keep the pipeline reliable
- Review PRs for testability and adequate test additions
- Collaborate with DevOps to integrate tests into the CI/CD pipeline
- Report test health metrics and escalate coverage gaps to leads

### Interaction Matrix
| Collaborator | How they interact |
|---|---|
| Developers | Review PRs for test coverage; pair on testability design |
| QA/Testing | Share automation results; align on what needs manual verification |
| DevOps Engineer | Integrate test stages into pipeline; coordinate environment requirements |
| Release Manager | Confirm automated gates are met before release promotion |
| Project Manager | Report test health and flag risks that affect release readiness |

### Goals
- Maintain a fast, reliable, and trustworthy CI pipeline
- Increase automated coverage to reduce reliance on manual regression
- Keep flaky-test rate below agreed threshold (e.g., < 2%)

### Suggested Handoff Points
- **Story kickoff**: review acceptance criteria for testability; identify automation approach
- **PR review**: verify new tests accompany feature changes
- **Release gate**: run full regression suite and provide go/no-go signal to Release Manager
- **Post-release**: update tests to cover any defects found in production

---

## UX Designer

### Role Summary
UX Designers ensure that product features are intuitive, accessible, and aligned with user needs. They translate product requirements into user flows, wireframes, and prototypes, and collaborate with Developers to ensure designs are implemented faithfully.

### Responsibilities
- Conduct or synthesize user research to inform design decisions
- Create wireframes, prototypes, and high-fidelity designs for features
- Define UX standards, patterns, and accessibility requirements
- Participate in design reviews and usability testing
- Collaborate with PdM and Developers on scope trade-offs and feasibility
- Deliver design handoff assets and annotated specs to the development team

### Interaction Matrix
| Collaborator | How they interact |
|---|---|
| Product Manager (PdM) | Align on user goals and feature scope; validate designs against requirements |
| Developers | Provide design specs and answer implementation questions during build |
| QA/Testing | Support usability testing and confirm design fidelity in QA |
| Stakeholders | Present concepts for feedback and approval |
| Project Manager | Communicate design timeline and flag dependencies |

### Goals
- Deliver designs that meet user needs and business objectives
- Ensure consistency across the product using a shared design system
- Reduce rework by involving Design early in the feature lifecycle

### Suggested Handoff Points
- **Discovery/Planning**: participate in problem framing with PdM and PM
- **Before sprint starts**: deliver reviewed, approved design specs to developers
- **Mid-sprint**: available for implementation questions and minor design adjustments
- **QA**: review implementation against designs; sign off on visual/UX fidelity

---

## Support Specialist

### Role Summary
Support Specialists are the front line for customer issues. They resolve escalated problems, identify recurring patterns, and feed actionable learnings back to Product and Engineering so that systemic issues can be addressed upstream.

### Responsibilities
- Triage and resolve escalated customer issues within agreed SLA
- Document issue patterns and recurring pain points in a shared log
- Communicate known issues and workarounds to customers during incidents
- Partner with QA and Engineering on reproducing and prioritizing bugs
- Participate in post-release monitoring to catch customer-impacting regressions
- Provide feedback to PdM on usability gaps and feature requests

### Interaction Matrix
| Collaborator | How they interact |
|---|---|
| QA/Testing | Share bug reproductions and validate fixes before they reach customers |
| Product Manager (PdM) | Escalate recurring pain points; provide customer feedback input for roadmap |
| Release Manager | Receive release notes and known-issues briefs ahead of deploy |
| Developers | Report confirmed bugs with reproduction steps for triage |
| Project Manager | Flag SLA risks and escalate high-priority customer issues |

### Goals
- Resolve customer issues quickly and within SLA
- Surface product quality signals that drive backlog prioritization
- Reduce repeat contacts by feeding learnings back to Product and Engineering

### Suggested Handoff Points
- **Pre-release**: receive release notes and known issues from Release Manager
- **Post-release (first 48 h)**: monitor for spikes in customer contacts; escalate anomalies
- **Sprint planning**: share top support themes so PdM can consider them in prioritization
- **Bug triage**: provide reproduction details and customer severity context to Engineering

---

## DevOps Engineer

### Role Summary
DevOps Engineers design, build, and operate the CI/CD infrastructure that enables teams to deliver software safely and repeatedly. They own pipeline reliability, environment management, and the tooling that connects development to production.

### Responsibilities
- Build and maintain CI/CD pipelines for build, test, and deployment
- Manage environment configurations and ensure environment parity
- Implement and enforce infrastructure-as-code practices
- Monitor pipeline health and resolve build/deploy infrastructure failures
- Collaborate with QA Automation Engineers to integrate test stages
- Support Release Managers during production deployments and rollbacks

### Interaction Matrix
| Collaborator | How they interact |
|---|---|
| Developers | Provide pipeline tooling; troubleshoot build failures; review infra-related PRs |
| QA Automation Engineer | Integrate automated test stages; provision test environments |
| Release Manager | Execute and support production deployments; own rollback procedures |
| Project Manager | Communicate pipeline incidents that affect release timelines |
| Security/Compliance | Integrate security scans and compliance checks into the pipeline |

### Goals
- Maintain pipeline uptime and reliability (e.g., > 99% build success rate)
- Reduce deployment lead time and enable on-demand releases
- Ensure every release is auditable, repeatable, and reversible

### Suggested Handoff Points
- **Sprint start**: validate that environments and pipeline stages are ready for the sprint's work
- **Feature merge**: confirm CI passes end-to-end before promoting to staging
- **Pre-release**: run deployment dry-run or staging promotion; validate rollback procedure
- **Post-release**: monitor infrastructure health; hand off to Support if application-level issues arise

---

## How these personas are used in the exercise
- Use these persona definitions to frame scenarios and sample interactions in the Skills Exercise.
- Each persona can be used as a persona prompt for Copilot Spaces to shape role-specific guidance.

