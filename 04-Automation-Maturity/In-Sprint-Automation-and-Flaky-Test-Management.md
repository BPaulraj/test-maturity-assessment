# In-Sprint Automation & Flaky Test Management

Purpose: automation written "later" has a strong tendency to never get written — deferred automation backlog items decay while feature work keeps moving. This document sets in-sprint automation as the target operating model, and gives flaky tests — the inevitable byproduct of a growing automated suite — a real lifecycle instead of an ignore-and-rerun habit.

## 1. In-Sprint Automation as the Target

For any P0/P1 test case (per [Test-Case-Management-and-Risk-Based-Design.md](../01-Policy-and-Standards/Test-Case-Management-and-Risk-Based-Design.md)) tied to a story, the automated script is authored, reviewed, and merged **within the same sprint** as the story, becoming part of the regression suite before the story is marked Done — this is already implied by [Entry-Exit-Criteria-and-DoD.md §5.3](../01-Policy-and-Standards/Entry-Exit-Criteria-and-DoD.md) ("regression suite updated") and is stated here explicitly as the default expectation, not an aspiration.

When a case genuinely cannot be automated in-sprint, it does not get silently dropped — it follows the deviation path in [Automation-Coverage-Decisioning-and-Technical-Debt.md](Automation-Coverage-Decisioning-and-Technical-Debt.md).

## 2. Flaky Test Lifecycle

A test suite that grows without an active flaky-test process degrades into "just re-run it until it's green," which quietly destroys the value of automated gating. The lifecycle:

| Stage | Trigger | Action |
|---|---|---|
| **Detection** | A test fails intermittently without a corresponding code change — tracked automatically via rerun-and-compare in CI, not noticed anecdotally | Flagged after a threshold (e.g., 2 intermittent failures in a rolling 2-week window) |
| **Quarantine** | Flagged as flaky | Pulled out of the merge-blocking gate immediately (so it stops blocking unrelated work), but stays **visible** on a quarantine dashboard — never deleted or silently skipped |
| **Root-cause window** | Entered quarantine | An SLA applies (e.g., fixed or retired within 2 sprints), owned by the module owner defined in [Test-Case-Management-and-Risk-Based-Design.md §6](../01-Policy-and-Standards/Test-Case-Management-and-Risk-Based-Design.md) |
| **Re-admission** | Fix applied | Test must run stable across N consecutive runs before re-entering the gating suite |
| **Escalation** | Quarantine list only grows, never shrinks | Triggers a resourcing conversation with the Engineering Manager, not just more tickets |

If a flaky test's root cause turns out to be a genuine product bug (not a test issue), it graduates into the normal [Defect-Management-Standard.md](../01-Policy-and-Standards/Defect-Management-Standard.md) flow rather than staying in the automation-only track.

## 3. Automation Suite Health Cadence

A recurring **automation health review**, at least weekly, distinct from the general defect triage ritual ([Defect-Management-Standard.md §6](../01-Policy-and-Standards/Defect-Management-Standard.md)) because this reviews the suite itself, not the product:

- New failures since the last review.
- Current quarantine list and how long each item has been there against its SLA.
- Suite execution time trend.
- Coverage trend by priority tier (§4).
- Status of any deferred-automation tech-debt items due this sprint (per [Automation-Coverage-Decisioning-and-Technical-Debt.md](Automation-Coverage-Decisioning-and-Technical-Debt.md)).

Owned by the SDET/automation lead for the team.

## 4. Suite Coverage Tracking

Track **% of P0/P1 test cases automated, by module** — not a single blended org-wide automation percentage, which hides exactly which module is actually weak. Reviewed at the same cadence as suite health, and feeds [Metrics-and-KPI-Standard.md](../01-Policy-and-Standards/Metrics-and-KPI-Standard.md) (Automation Coverage %, In-Sprint Automation Completion Rate).

## 5. Assessment Hook

Scored under [Questionnaire.md](../02-Assessment-Questionnaire/Questionnaire.md) sections G/H and the [Automation-Capability-Assessment.md](Automation-Capability-Assessment.md) deep-dive (Part 2, item 4 — flaky test management).
