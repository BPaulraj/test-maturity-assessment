# Organisation Test Policy

## 1. Purpose

This policy defines the mandatory quality bar for how software is tested across the organisation. It exists so that:

- Leadership can trust a release regardless of which team shipped it.
- Teams know unambiguously what "good testing" means before an assessment ever happens.
- Investment in tooling, automation, and AI is guided by a shared standard instead of per-team preference.

This policy is the **target state**. The [Assessment Questionnaire](../02-Assessment-Questionnaire/Questionnaire.md) and [Maturity Model](../03-Maturity-Model/Maturity-Model-Framework.md) measure distance from it.

## 2. Scope

Applies to every team that ships code to production or to an external customer: product engineering, platform/infra, data engineering, and vendor/outsourced delivery teams. Risk tiering (Section 4) determines *how much* of this policy is mandatory vs. recommended for a given team.

## 3. Guiding Principles

1. **Quality is a whole-team responsibility**, not a phase owned solely by a "QA" role. Developers own unit/component testing; dedicated testers own risk-based design, exploratory testing, and quality advocacy.
2. **Risk-based, not exhaustive.** Test effort and depth are proportional to business/technical risk, not applied uniformly.
3. **Shift-left and shift-right.** Quality gates start at requirements (testability review) and continue into production (observability, synthetic monitoring, feature-flag rollback).
4. **Automate anything repeated more than twice**, and automate at the lowest viable layer (test pyramid: unit > component/API > E2E UI).
5. **Everything is measured.** Coverage, defect leakage, flakiness, and cycle time are tracked on dashboards, not reported anecdotally.
6. **Tooling is standardised at the category level, not the vendor level.** Teams may choose a specific tool within an approved category (see [Testing-Types-Standards.md](Testing-Types-Standards.md)) but must not fragment on categories that block org-wide reporting (e.g., test management, CI orchestration).
7. **AI augments, it does not replace, accountability.** Any AI-generated test artefact (test case, script, data) must pass through the same human review and CI gates as human-authored work — see [AI-in-Testing governance](../05-AI-in-Testing/AI-in-Testing-Maturity-Model-and-Governance.md).
8. **Continuous improvement is scheduled, not aspirational.** Every team runs a quality retrospective at least every release cycle and re-assesses maturity quarterly.

## 4. Risk Tiering (drives how strictly this policy applies)

| Tier | Definition | Examples | Policy stringency |
|---|---|---|---|
| **Tier 1 — Critical** | Revenue-bearing, regulated, safety/compliance-impacting, or high blast-radius (auth, payments, core platform APIs) | Payments, identity, core ledger | Full policy mandatory. No exceptions without CTO/Head of Engineering sign-off. |
| **Tier 2 — Important** | Customer-facing, moderate blast radius, has SLAs | Most product features | Full policy mandatory; exceptions allowed via COE with documented compensating control. |
| **Tier 3 — Standard** | Internal tools, low blast radius, easily reversible | Internal dashboards, admin tools | Core non-negotiables mandatory (Section 5); rest is recommended. |
| **Tier 4 — Experimental** | Prototypes, spikes, pre-PMF features | POCs, hackathon output | Non-negotiables reduced to: no destructive testing in prod, basic smoke test before demo. |

## 5. Non-Negotiables (apply to Tier 1–3 regardless of maturity level)

These are the floor, not the ceiling. A team scoring "ad hoc" on the maturity model but violating a non-negotiable is treated as a **risk escalation**, not just a low score.

1. No production release without a documented test execution record (pass/fail evidence), even if execution was manual.
2. No merge to the main/release branch without the automated regression suite for that service passing (or a documented, time-boxed waiver).
3. Every Tier 1/2 defect classified as Critical/High must have a root-cause note and a regression test added before closure.
4. Test environments and production must never share credentials or PII-bearing datasets without masking/synthetic substitution.
5. Every Tier 1 service has a defined rollback/kill-switch mechanism validated in a non-prod environment.
6. Security and accessibility testing (per [Testing-Types-Standards.md](Testing-Types-Standards.md)) are never skipped for Tier 1/2 customer-facing releases — they may be reduced in depth, never omitted entirely.
7. Any AI tool used on test artefacts is from the org's approved list (see AI governance doc) — no ungoverned "shadow AI" use on code, test data, or logs that may contain confidential/PII data.

## 6. Roles and Governance

| Role | Responsibility |
|---|---|
| **Head of Quality Engineering / Test COE** | Owns this policy, the maturity model, and the assessment cadence. Approves risk-tier exceptions. Chairs the quarterly maturity review with leadership. |
| **Team QE Lead / SDET Lead** | Owns the team's maturity score, evidence, and improvement plan. Primary point of contact for assessments. |
| **Engineering Manager / Delivery Lead** | Resources the improvement plan; accountable for non-negotiable compliance. |
| **Product Owner** | Confirms risk tiering for their product area; sponsors testability requirements in the backlog. |
| **Test COE Enablement Function** | Runs the shared automation framework(s), tooling standardisation, training academy, and AI governance review board. |

## 7. Exceptions Process

A team may request a temporary exception to any standard (not a non-negotiable) by submitting: (a) the specific clause, (b) business justification, (c) compensating control, (d) expiry date (max 2 quarters), to the Test COE. Exceptions are logged and reviewed at every quarterly maturity review — they are visible to leadership, never silently tolerated.

## 8. Policy Review Cadence

This policy is reviewed twice yearly by the Test COE with input from Engineering leadership, and whenever a major incident's root-cause analysis implicates a testing gap.

## 9. Related Documents

- [Testing-Types-Standards.md](Testing-Types-Standards.md) — the standard per level/type of testing.
- [Entry-Exit-Criteria-and-DoD.md](Entry-Exit-Criteria-and-DoD.md) — phase gates and Definition of Done (story, feature, and release levels).
- [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md) — what gets measured and reported org-wide.
- [Test-Artefact-and-Tooling-Standard.md](Test-Artefact-and-Tooling-Standard.md) — what a test management tool must support, and what artefact lives where.
- [Test-Case-Management-and-Risk-Based-Design.md](Test-Case-Management-and-Risk-Based-Design.md) — test case organisation, tagging, and risk-based prioritisation.
- [Defect-Management-Standard.md](Defect-Management-Standard.md) — defect handling by discovery stage, severity vs. priority, and the hotfix path.
- [Test-Data-Management-Standard.md](Test-Data-Management-Standard.md) — synthetic vs. sanitized-production-copy data supply and refresh cadence.
- [Test-Environment-Strategy.md](Test-Environment-Strategy.md) — environment topology and the dedicated performance environment's prod-parity model.
- [08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md](../08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md) — shift-left across ceremonies, story/feature/release testing levels, and the release cadence / pre-production gate.
- [08-Agile-Scrum-Practices/NFR-and-Specialized-Testing-Placement-in-STLC.md](../08-Agile-Scrum-Practices/NFR-and-Specialized-Testing-Placement-in-STLC.md) — where DAST, accessibility, and performance testing sit in the STLC and sprint cycle.
- [04-Automation-Maturity/In-Sprint-Automation-and-Flaky-Test-Management.md](../04-Automation-Maturity/In-Sprint-Automation-and-Flaky-Test-Management.md) — in-sprint automation as the target, and the flaky-test lifecycle.
- [04-Automation-Maturity/Automation-Coverage-Decisioning-and-Technical-Debt.md](../04-Automation-Maturity/Automation-Coverage-Decisioning-and-Technical-Debt.md) — what to automate now vs. defer, and protected tech-debt/upskilling capacity.
- [Test-Artefact-Approval-and-Signoff-Standard.md](Test-Artefact-Approval-and-Signoff-Standard.md) — which artefacts need whose sign-off, and what makes a sign-off a documented record.
- [Master-Test-Pack-Maintenance-Standard.md](Master-Test-Pack-Maintenance-Standard.md) — the canonical regression suite's sprint-end sync and reuse-first rule.
- [Tester-Competency-Assessment-and-Upskilling-Standard.md](Tester-Competency-Assessment-and-Upskilling-Standard.md) — the 6-month competency assessment cadence and rubric.
- [04-Automation-Maturity/Automation-Execution-Model-Environments-and-Pipelines.md](../04-Automation-Maturity/Automation-Execution-Model-Environments-and-Pipelines.md) — suite tier, frequency, environment, and pipeline-stage matrix.
