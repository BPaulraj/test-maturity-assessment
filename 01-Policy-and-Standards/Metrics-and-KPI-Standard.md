# Metrics & KPI Standard

Purpose: a shared metric set so leadership can compare across teams without each team inventing its own definitions. Every metric below has an **owner**, a **source of truth**, and a **reporting cadence**. Metrics feed the [Leadership Summary](../07-Leadership-Summary/) dashboard.

## Quality Outcome Metrics (lagging indicators)

| Metric | Definition | Cadence | Good direction |
|---|---|---|---|
| Defect Escape Rate | % of defects found in production vs. total found (pre-prod + prod) | Monthly | ↓ |
| Defect Density | Defects per 1,000 lines of code changed, or per story point | Per release | ↓ |
| Critical/High Defect Aging | Median time from open to resolution for Critical/High defects | Monthly | ↓ |
| Production Incident Rate (test-attributable) | Incidents whose root cause was a testing gap | Monthly | ↓ |
| Customer-Reported Defect Rate | Defects reported by customers post-release | Monthly | ↓ |
| Known Issues Backlog Age | Median age of open "Known Issue — Released" items | Monthly | ↓ |

## Process Efficiency Metrics (leading indicators)

| Metric | Definition | Cadence | Good direction |
|---|---|---|---|
| Requirements Traceability % | % of acceptance criteria with at least one linked test case | Per release | ↑ |
| Test Execution Velocity | Planned vs. actual test cases executed per cycle | Per sprint/release | ↑ (toward 100%) |
| Test Cycle Time | Time from code-complete to test sign-off | Per release | ↓ |
| Environment Availability/Uptime | % of time test environments were usable vs. blocked | Monthly | ↑ |
| Environment Provisioning Lead Time | Time to stand up a usable test environment | Per request | ↓ |
| Sign-off Compliance Rate | % of sprints/releases with a properly documented sign-off record (per [Test-Artefact-Approval-and-Signoff-Standard.md](Test-Artefact-Approval-and-Signoff-Standard.md)) vs. shipped without one | Per sprint/release | ↑ (toward 100%) |

## Automation Metrics

| Metric | Definition | Cadence | Good direction |
|---|---|---|---|
| Automation Coverage % | % of regression test cases automated | Monthly | ↑ |
| Automation ROI | Manual hours saved vs. automation build/maintenance cost | Quarterly | ↑ |
| Flaky Test Rate | % of automated tests that fail intermittently without a code change | Weekly | ↓ |
| Suite Execution Time | Wall-clock time for full automated regression run | Weekly | ↓ (via parallelisation) |
| CI Pipeline Test Gate Pass Rate | % of PRs blocked by automated test gate vs. bypassed | Monthly | ↑ (gate honoured, not bypassed) |
| Automation Maintenance Ratio | Hours spent fixing/maintaining existing tests vs. writing new ones | Monthly | ↓ over time (indicates framework health) |
| In-Sprint Automation Completion Rate | % of agreed in-sprint automation targets (per [Automation-Coverage-Decisioning-and-Technical-Debt.md](../04-Automation-Maturity/Automation-Coverage-Decisioning-and-Technical-Debt.md)) actually completed within the sprint | Per sprint | ↑ |
| Flaky Test Time-to-Resolution | Median days a test spends in quarantine before fix or retirement | Monthly | ↓ |
| Tech-Debt/Enablement Capacity Delivered vs. Planned | Actual vs. planned sprint/PI capacity spent on automation maintenance, flaky fixes, and upskilling | Per sprint/PI | ↑ (toward 100% of plan) |
| Pre-Production Gate Pass Rate | % of release candidates passing the pre-production gate without an exception/waiver | Per release | ↑ |
| Test Case Reuse Rate | % of a sprint's test-coverage needs met by extending existing Master Test Pack cases vs. net-new authoring | Per sprint | ↑ |

## Competency Metrics

| Metric | Definition | Cadence | Good direction |
|---|---|---|---|
| Competency Assessment Completion Rate | % of testers assessed on the defined 6-month cadence (per [Tester-Competency-Assessment-and-Upskilling-Standard.md](Tester-Competency-Assessment-and-Upskilling-Standard.md)) | Semi-annual | ↑ (toward 100%) |
| Upskill Plan On-Time Rate | % of individual upskill plan milestones met by their target date | Quarterly | ↑ |

## AI-in-Testing Metrics

| Metric | Definition | Cadence | Good direction |
|---|---|---|---|
| AI-Assisted Artefact Volume | % of test cases/scripts with AI involvement in authoring | Monthly | Track trend, not a target |
| AI Artefact Acceptance Rate | % of AI-generated test artefacts accepted after human review without major rework | Monthly | ↑ |
| Time Saved via AI Assistance | Estimated hours saved on test design/authoring/triage | Quarterly | ↑ |
| AI Governance Compliance | % of AI tool usage through approved/governed tools vs. shadow AI | Quarterly | ↑ (toward 100%) |

## Reporting Standard

- Every metric has a single **source of truth system** (test management tool, CI system, defect tracker) — no metric is manually tallied in a spreadsheet once a team is Level 3+.
- Team-level dashboards refresh at least weekly; the org roll-up (Leadership Summary) refreshes at least monthly and at each quarterly maturity review.
- Metrics are always shown with **trend**, not just a snapshot — a single data point without trend context is not acceptable reporting per this standard.
