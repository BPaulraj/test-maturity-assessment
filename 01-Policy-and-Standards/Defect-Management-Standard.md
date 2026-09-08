# Defect Management Standard

Purpose: a bug found by a tester mid-sprint, one found in regression two sprints later, one found in UAT, and one found in production all look similar on the surface but carry very different urgency and process implications. This standard gives each stage its own handling so the org isn't either over-reacting to healthy in-sprint catches or under-reacting to a live production issue.

## 1. Defect Handling by Discovery Stage

| Stage | Handling | Counts toward org defect-density KPI? |
|---|---|---|
| **In-Sprint** (found while testing a story, before it's marked Done) | Fixed within the sprint as part of normal story completion; logged as a task/sub-task, not a formal "defect" | **No** — this is healthy testing doing its job, not an escape. Counting it would penalise teams for catching things early. |
| **Later-Sprint / Regression-found** (found after the story was marked Done, in a subsequent regression pass) | Logged as a formal defect against the original story/feature; root-cause required if Critical/High | Yes |
| **UAT-found** | Logged, business-severity co-assessed with Product; triaged before release exit criteria are signed off | Yes |
| **Production-found** | Highest urgency; hotfix path (§4) if Critical; always root-caused; always triggers escape analysis (§5) | Yes — and separately tracked as Production Incident Rate per [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md) |

This distinction matters for reporting integrity: a team that tests thoroughly mid-sprint will surface *more* in-sprint issues, and a naive metric would make them look worse than a team that tests superficially and pushes everything into "later-found." Excluding in-sprint catches from the escape-rate metric removes that perverse incentive.

## 2. Severity vs. Priority (two different axes — never conflate them)

- **Severity** = technical/functional impact if unfixed: Critical / High / Medium / Low.
- **Priority** = business urgency to fix now: P1 (immediate) / P2 (this sprint) / P3 (backlog) / P4 (won't fix / accepted risk).

| Example | Severity | Priority | Why they diverge |
|---|---|---|---|
| Crash on a rarely-used admin report | Critical (crashes the app) | P3 | Low usage means low business urgency despite technical severity |
| Wrong label text on the checkout button | Low (cosmetic) | P1 | High-visibility, high-traffic page — business wants it fixed now |

Severity is set by the tester/SDET based on technical impact; Priority is set jointly with Product based on business context. Neither role unilaterally overrides the other's axis.

## 3. SLA by Severity (aligned to [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md) "Critical/High Defect Aging")

| Severity | Non-production SLA | Production SLA |
|---|---|---|
| Critical | Fixed before release exit | Hotfix within hours (see §4) |
| High | Fixed within the sprint | Fixed within 1–2 business days |
| Medium | Fixed within 2 sprints | Fixed within the next planned release |
| Low | Backlog, prioritised opportunistically | Backlog |

## 4. Production Hotfix Path (Critical severity only)

1. Expedited triage — bypasses normal sprint planning, pulled in immediately.
2. Minimal viable fix scoped as tightly as possible (no opportunistic refactoring bundled in).
3. Risk-based regression subset run (P0 test cases for the affected module, per [Test-Case-Management-and-Risk-Based-Design.md](Test-Case-Management-and-Risk-Based-Design.md)) — not the full suite, to keep the fix fast, but never zero regression.
4. Expedited approval per the risk tier's exception path.
5. Full regression pass scheduled in the next normal cycle to backfill anything the subset run couldn't cover.
6. Mandatory root-cause entry and retrospective note (§5) — a hotfix is never closed without this step.

## 5. Escape Analysis — Closing the Loop

Every later-sprint, UAT, or production defect gets a root-cause classification (requirement gap, missed edge case, environment/data issue, automation gap, regression from unrelated change, etc.). Recurring categories are reviewed at the quarterly [maturity review](../06-Improvement-Planning/RACI-and-Operating-Model.md) and converted into either new regression coverage, a process fix, or a tooling investment — an escape analysis that doesn't change anything concrete next cycle has not actually closed the loop.

## 6. Triage Cadence

- **Production / Critical:** immediate, ad hoc — no waiting for a scheduled ritual.
- **Everything else:** a standing, scheduled cross-functional triage ritual at least weekly (see [Questionnaire.md §C.3](../02-Assessment-Questionnaire/Questionnaire.md)), not ad hoc pings.

## 7. Roles

| Role | Responsibility |
|---|---|
| Tester / SDET | Sets severity, verifies fix, assesses regression impact |
| Developer | Fixes the defect, flags any root-cause insight to test design |
| Product Owner | Sets/confirms priority for business-facing defects |
| Test COE | Aggregates escape-analysis trends org-wide, feeds systemic patterns into policy updates |

## 8. Defects from Non-Functional Testing

Defects found during performance, DAST, and accessibility testing (per [NFR-and-Specialized-Testing-Placement-in-STLC.md](../08-Agile-Scrum-Practices/NFR-and-Specialized-Testing-Placement-in-STLC.md)) are logged in the same single defect-tracking source of truth (§1 above), but each carries a domain-specific classification before it's translated into the org's Critical/High/Medium/Low scale for SLA purposes:

| Type | Domain-specific classification | Owner | Visibility |
|---|---|---|---|
| Security (DAST) | CVSS score or equivalent | Security team fixes; tester verifies | **Access-restricted** until patched or formally disclosed — never posted on a broadly-visible board while an exploitable vulnerability is open |
| Accessibility | WCAG conformance level (A/AA/AAA) + violation severity | Feature team (not a separate a11y silo) | Standard visibility |
| Performance | The specific NFR threshold breached (e.g., "p95 latency 420ms vs. 300ms target") | Joint Dev + Platform/SRE — fixes are often architectural/infrastructure, not a simple code change | Standard visibility |

All three still feed the same escape-analysis loop (§5) and SLA table (§3) as any other defect — the domain-specific classification determines routing and initial severity judgment, it does not exempt the defect from the standard lifecycle.

## 9. Known Issues Released to Production

A defect that Product explicitly risk-accepts for release (per the Release Package Sign-off in [Test-Artefact-Approval-and-Signoff-Standard.md §3](Test-Artefact-Approval-and-Signoff-Standard.md)) is never simply closed or left to age quietly in the defect tracker. It is:

1. **Tagged** "Known Issue — Released," recorded against the release version it shipped in.
2. **Added to the product backlog** (not only the defect tracker) with a priority, so it competes for prioritisation like any other backlog item instead of living somewhere the backlog grooming process never sees.
3. **Included in release notes'** known-issues section with the risk-acceptance decision-maker recorded.
4. **Reviewed on a defined cadence** (at minimum, every quarter or at every subsequent release planning) — a known issue is never allowed to sit indefinitely un-reviewed. Each review either schedules it, re-assesses the risk, or renews the risk-acceptance sign-off; it is never simply carried forward by default.

**Metric:** Known Issues Backlog Age (median age of open known issues) — tracked in [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md).
