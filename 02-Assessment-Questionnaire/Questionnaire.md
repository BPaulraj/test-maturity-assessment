# Test Maturity Assessment Questionnaire

**How to use:** Score every applicable question 0–4 using the anchors below. Do not accept a score without evidence (see [Evidence-Checklist.md](Evidence-Checklist.md)). Mark questions N/A when the practice genuinely does not apply (e.g., mobile device matrix for a backend-only service) — N/A items are excluded from the denominator, never scored as 0. See [Scoring-and-Weighting-Guide.md](Scoring-and-Weighting-Guide.md) for how section scores roll up.

**Universal rating anchors:**

| Score | Meaning |
|---|---|
| 0 | Not present / purely reactive / no awareness |
| 1 | Initial — done inconsistently, person-dependent, undocumented |
| 2 | Defined — documented/repeatable but largely manual, not measured |
| 3 | Standardized & Measured — consistent, tool-supported, tracked on a dashboard |
| 4 | Optimizing — continuously improved using data, benchmarked, is a source of org best practice |

---

## A. Test Strategy & Planning

1. Is there a documented test strategy per product/service, reviewed at least yearly?
2. Is test scope/depth explicitly risk-based (tiered), rather than uniform across all features?
3. Are non-functional requirements (perf, security, a11y) captured at planning time, not discovered late?
4. Is testability considered during requirements/design review (shift-left)?
5. Are test estimates/effort tracked against actuals to improve future planning?
6. Is there a defined process for scoping regression impact when a change is made?
7. Are non-functional requirements (perf, security, a11y) captured as quantified, testable thresholds rather than qualitative statements ("should be fast")?
8. Is there a defined approval matrix specifying which stakeholders must sign off which test artefacts (strategy, compliance-critical test cases, UAT scenarios, NFT plans)? See [Test-Artefact-Approval-and-Signoff-Standard.md](../01-Policy-and-Standards/Test-Artefact-Approval-and-Signoff-Standard.md).

## B. Test Design & Documentation

*(Organisation, tagging, and lifecycle standard: [Test-Case-Management-and-Risk-Based-Design.md](../01-Policy-and-Standards/Test-Case-Management-and-Risk-Based-Design.md). Tooling/artefact taxonomy: [Test-Artefact-and-Tooling-Standard.md](../01-Policy-and-Standards/Test-Artefact-and-Tooling-Standard.md).)*

1. Are test cases derived from documented, traceable requirements/acceptance criteria?
2. Is there a living test case repository (not scattered docs/spreadsheets), organised by module/component with a consistent naming and tagging scheme?
3. Are test design techniques (equivalence partitioning, boundary value, state transition, etc.) applied deliberately for complex logic, not just ad hoc?
4. Is requirements-to-test traceability tracked and reportable (% coverage), generated from the tool rather than hand-maintained?
5. Are test cases reviewed by a peer before being trusted as regression coverage?
6. Is test case priority risk-based (P0–P3, driven by business criticality, defect hotspots, and usage data) rather than uniform or unassigned?
7. Is there a scheduled test case health audit (staleness, duplication, re-prioritisation), not a write-once-forget-forever suite?
8. Can traceability be navigated in **both directions** — story → test case → defect, and defect → test case → story — for coverage/impact analysis and root-cause analysis respectively?
9. Is there a reuse-first rule enforced before authoring new test cases (search and extend Master Test Pack coverage before cloning), per [Master-Test-Pack-Maintenance-Standard.md](../01-Policy-and-Standards/Master-Test-Pack-Maintenance-Standard.md)?

## C. Test Execution & Reporting

1. Is test execution status visible on a live dashboard (not a manually compiled status email)?
2. Are entry/exit criteria (per [Entry-Exit-Criteria-and-DoD.md](../01-Policy-and-Standards/Entry-Exit-Criteria-and-DoD.md)) enforced, not just documented?
3. Is defect triage a scheduled, cross-functional ritual (not ad hoc pings)?
4. Are release sign-off decisions based on objective exit-criteria data?
5. Is there a retrospective after every release/major defect escape to capture lessons?
6. Are sprint-package and release-package sign-offs documented records — named approver, role, date, specific version, any conditions — rather than a verbal or chat-based approval? See [Test-Artefact-Approval-and-Signoff-Standard.md](../01-Policy-and-Standards/Test-Artefact-Approval-and-Signoff-Standard.md).

## D. Levels & Types of Testing Coverage

*Score each applicable row from [Testing-Types-Standards.md](../01-Policy-and-Standards/Testing-Types-Standards.md) against its stated minimum expectation:* Unit, Component/Integration, API, System/E2E, Regression, Performance, Security, Accessibility, Usability/UAT, Exploratory, Contract, Chaos/Resilience, Data/ETL, Mobile, Compatibility, Localization, Visual Regression.

## E. Defect & Quality Management

*(Full standard: [Defect-Management-Standard.md](../01-Policy-and-Standards/Defect-Management-Standard.md).)*

1. Is there a single defect-tracking source of truth used consistently (no shadow spreadsheets)?
2. Does defect handling distinguish discovery stage (in-sprint / later-sprint-regression / UAT / production), rather than treating every bug identically regardless of when and where it surfaced?
3. Are severity and priority tracked as two distinct axes, each with a clear owner (severity by tester/SDET, priority jointly with Product)?
4. Is there an expedited hotfix path for production-Critical defects, distinct from normal sprint-planning flow?
5. Are defects root-caused, with recurring patterns analysed (not just closed and forgotten)?
6. Is escaped-defect analysis fed back into test design (closing the loop) — with a concrete resulting change, not just a documented root cause?
7. Are defect SLAs (by severity) defined and tracked?
8. Are non-functional defects (security/DAST, performance, accessibility) classified on their domain-specific scale (CVSS, WCAG level, NFR threshold breached) and routed to the correct owning team, with security findings access-restricted until remediated?
9. Are known issues that Product risk-accepts for release added to the product backlog (not left only in the defect tracker) and reviewed on a defined cadence rather than aging indefinitely? See [Defect-Management-Standard.md §9](../01-Policy-and-Standards/Defect-Management-Standard.md).

## F. Test Environment & Data Management

*(Full standards: [Test-Environment-Strategy.md](../01-Policy-and-Standards/Test-Environment-Strategy.md), [Test-Data-Management-Standard.md](../01-Policy-and-Standards/Test-Data-Management-Standard.md).)*

1. Are test environments provisioned via self-service/IaC rather than manual ticketing?
2. Is environment-to-production parity tracked and drift alerted?
3. Is there a dedicated performance environment, isolated from functional SIT/UAT, with a documented prod-parity or scaling-extrapolation model (load balancer, topology, node count) that is periodically re-validated against real production behaviour?
4. Does recurring environment instability trigger a formal root-cause investigation rather than being absorbed as normal?
5. Is test data synthetic/masked, with no raw PII in non-prod (non-negotiable — see policy), and is the masking pipeline itself validated by an automated scan on every refresh?
6. Is sanitized production data refreshed into non-prod on a defined, followed cadence (not ad hoc or stale)?
7. Is test data refresh/reset self-service and fast enough to not block testers?

## G. Test Automation — Capability

*(Full deep-dive lives in [04-Automation-Maturity](../04-Automation-Maturity/); summary questions here for the base assessment.)*

1. Is there a standardised automation framework (not a different ad hoc script style per engineer)?
2. Is automated test code version-controlled and code-reviewed like production code?
3. Is flaky-test management a full lifecycle (detect → quarantine → SLA-bound root-cause → re-admission), not an ignore-and-rerun habit? See [In-Sprint-Automation-and-Flaky-Test-Management.md](../04-Automation-Maturity/In-Sprint-Automation-and-Flaky-Test-Management.md).
4. Is the automation pyramid respected (majority unit/API, thin E2E layer) rather than E2E-heavy?
5. Is there a documented, agreed set of criteria for what must be automated in-sprint vs. what may be deferred, rather than an ad hoc per-engineer call? See [Automation-Coverage-Decisioning-and-Technical-Debt.md](../04-Automation-Maturity/Automation-Coverage-Decisioning-and-Technical-Debt.md).

## H. Test Automation — Capacity & CI/CD Integration

1. Does automation run on every PR/commit (not just nightly or on-demand)?
2. Can the automated suite gate a merge/deploy (i.e., is it trusted enough to block)?
3. Is execution parallelised/distributed to keep feedback time short?
4. Is there dedicated capacity (SDET role/time allocation) for automation maintenance, or is it "whoever has time"?
5. Is in-sprint automation the default target, with any deviation tracked as an explicit, prioritised technical-debt item (same priority tag as the original test case), not silently dropped?
6. Is there protected sprint/PI capacity (guideline 10–20%) reserved for automation maintenance, flaky-test fixes, and upskilling, with delivery against that allocation actually tracked?
7. Does each suite tier (smoke/sanity/regression/non-functional) run at a defined frequency, in a defined environment, and at a defined pipeline stage — with suite health judged from a stable, dedicated environment rather than a noisy ephemeral one? See [Automation-Execution-Model-Environments-and-Pipelines.md](../04-Automation-Maturity/Automation-Execution-Model-Environments-and-Pipelines.md).

## I. Tooling

*(Full standard: [Test-Artefact-and-Tooling-Standard.md](../01-Policy-and-Standards/Test-Artefact-and-Tooling-Standard.md).)*

1. Is the team's tool stack within the org's approved categories (test management, automation, CI, defect tracking, performance, security)?
2. Is tooling choice justified by need rather than individual preference/legacy inertia?
3. Is tool usage/licensing tracked for cost governance?
4. Is there integration between tools (e.g., test management ↔ CI ↔ defect tracker) rather than manual data re-entry?

## J. AI in Testing

*(Full deep-dive lives in [05-AI-in-Testing](../05-AI-in-Testing/); summary questions here.)*

1. Is AI used anywhere in the test lifecycle (design, script generation, data generation, triage, visual comparison)?
2. Is that AI usage through an org-approved/governed tool, with human review before artefacts are trusted?
3. Is the impact of AI usage measured (time saved, quality uplift), not just anecdotal?
4. Is there awareness/training on AI risks (hallucinated test cases, data leakage) among the team?

## K. Competency & Skills

1. Is there a defined skills/competency matrix for testers/SDETs (manual, automation, performance, security, AI-augmented testing)?
2. Are individual development plans tied to identified skill gaps?
3. Is there a career path for testers into SDET/QE leadership (not a dead-end role)?
4. Is knowledge-sharing (brown bags, internal wiki, community of practice) active?
5. Is tester competency reassessed on a defined cadence (e.g., every 6 months) against a documented rubric, with upskill plan progress tracked between assessments rather than only discovered at the next one? See [Tester-Competency-Assessment-and-Upskilling-Standard.md](../01-Policy-and-Standards/Tester-Competency-Assessment-and-Upskilling-Standard.md).

## L. Governance, Metrics & Continuous Improvement

1. Are the org-standard KPIs ([Metrics-and-KPI-Standard.md](../01-Policy-and-Standards/Metrics-and-KPI-Standard.md)) tracked for this team?
2. Is there a quarterly maturity self-assessment/re-assessment rhythm already in place?
3. Are improvement actions from the last assessment tracked to closure (not re-raised every cycle)?

## M. Culture & Stakeholder Collaboration

1. Is quality treated as a whole-team responsibility (developers engaged in testing), or siloed to a QA team?
2. Do Product/Business stakeholders participate in UAT/acceptance reviews?
3. Is there psychological safety to raise a quality concern and delay a release without retaliation?
4. Is testing represented in sprint/release planning as first-class work, not squeezed at the end?

## N. Agile Ceremony Integration & Release Aggregation

*(Full standard: [08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md](../08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md).)*

1. Does a tester participate in backlog refinement to review AC testability before a story enters a sprint?
2. Is test approach/estimate discussed alongside dev estimate at sprint planning, rather than assumed to fit inside it?
3. Do testers raise blockers (environment, data, AC ambiguity) in standup as first-class impediments?
4. Is there an explicit, scheduled feature-level aggregation test pass — beyond individual story AC verification — before a feature is declared Done?
5. Is there a feature-level demo/showcase to business stakeholders, distinct from the routine sprint-level demo, paired with feature-level test results?
6. Does the retrospective carry a standing quality question ("what escaped, why, what changes"), not just velocity/process topics?
7. Is release cadence explicitly declared, with every release passing through a pre-production gate (per [Sprint-and-Release-Testing-Cadence.md §4](../08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md)) rather than shipping straight from a sprint environment to production?
8. Does regression scope for a release scale with the number of sprints' worth of change actually batched into it, rather than running at a fixed size regardless of batch?
