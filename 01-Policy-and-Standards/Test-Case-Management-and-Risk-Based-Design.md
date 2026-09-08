# Test Case Management & Risk-Based Design Standard

Purpose: as a regression suite grows into the hundreds or thousands of cases, findability and prioritisation become the actual bottleneck — not writing new tests. This standard defines how test cases are organised, tagged, prioritised, and retired so any tester can find "what covers module X" and "what must run before this release" without tribal knowledge.

## 1. Organisation Taxonomy

Test cases are organised in a strict hierarchy inside the test management tool (per [Test-Artefact-and-Tooling-Standard.md](Test-Artefact-and-Tooling-Standard.md)):

```
Application / Service
  └─ Module / Component
       └─ Feature
            └─ Scenario (the test case itself)
```

This mirrors the system's architecture, not the org chart or sprint structure — a test case's home doesn't change when a team gets reorganised or a story moves sprints.

## 2. Naming Convention

`[Module]_[Feature]_[ScenarioType]_[ShortDescription]`

Example: `Checkout_ApplyCoupon_Negative_ExpiredCode`

`ScenarioType` is one of: Positive, Negative, Boundary, Integration, Performance, Security, Accessibility.

## 3. Tagging Scheme (every test case carries all of these)

| Tag category | Values |
|---|---|
| Suite membership | Smoke, Sanity, Regression, Full |
| Priority (risk-based, see §4) | P0, P1, P2, P3 |
| Execution type | Automated, Manual, Automation-candidate |
| Platform/scope | Web, API, Mobile-iOS, Mobile-Android, Backend, Data |
| Risk tier of the feature it covers | Tier 1–4, per [Org-Test-Policy.md](Org-Test-Policy.md) |

## 4. Risk-Based Prioritisation

| Priority | Definition | Run cadence |
|---|---|---|
| **P0** | Business-critical path; failure blocks core functionality or revenue | Every release, every regression run — non-negotiable |
| **P1** | Important functionality; failure is high-impact but not core-path-blocking | Every sprint |
| **P2** | Moderate value; failure is noticeable but workaroundable | Periodic / on-demand, at least once per release |
| **P3** | Low-value or deep edge case | Pre-major-release only, or flagged as a retirement candidate |

Priority is assigned using, in order of weight:
1. **Business criticality** of the feature (from the risk tier).
2. **Defect/hotspot history** — modules with recurring defects or high code churn get bumped up regardless of "intended" criticality.
3. **Usage analytics** — features with low real-world usage get bumped down even if technically important, unless compliance-mandated.
4. **Regulatory/compliance requirement**, which can force P0 regardless of the above.

Re-prioritisation is not a one-time exercise — it is revisited at the quarterly test case health audit (§6) using the latest defect and usage data, not left as it was set at creation.

## 5. Test Case Lifecycle

| Stage | Trigger | Action |
|---|---|---|
| Creation | New AC/story | Drafted alongside story development (shift-left, see [08-Agile-Scrum-Practices](../08-Agile-Scrum-Practices/)), peer-reviewed before being trusted as regression coverage |
| Update | AC/behaviour changes | Test case updated in the **same** story/PR that changes the behaviour — never backlogged as "update tests later" |
| Deprecation | Feature removed/replaced | Archived (excluded from active runs, retained for traceability history) — never silently deleted |
| Health audit | Quarterly | Duplicate/obsolete cases merged or archived; priority tags re-validated against latest defect/usage data; staleness (not reviewed in 2+ quarters) flagged |

## 6. Ownership

Every module/suite has a **named owner** (a specific tester or SDET, not "the team") accountable for that area's test suite health — coverage gaps, staleness, and duplication in their module are their responsibility to flag and fix, giving every part of the system a clear point of contact.

## 7. Metrics (feed into [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md))

- Test case count by module and by priority tier.
- % automated, broken down by priority (P0 automation coverage matters far more than P3).
- Staleness — % of cases not reviewed in the last 2 quarters.
- Duplication rate found at each health audit.

## 8. Assessment Hook

This standard is scored under Questionnaire section B (Test Design & Documentation) — see [Questionnaire.md](../02-Assessment-Questionnaire/Questionnaire.md). A team with a large but untagged, unprioritised, flat test case list scores no higher than L2 regardless of raw case count, since findability and risk-targeting — not volume — are what this standard measures.
