# Dimension Rubrics — Level-by-Level Detail

Used by assessors to justify a dimension's level assignment with descriptive criteria, not just the arithmetic score. If the numeric score and the descriptive rubric disagree, the rubric wins — numbers are a guide, not the final word.

## Process (Planning, Design, Execution, Defect & Environment Management)

| Level | Criteria |
|---|---|
| L1 | No documented test strategy; test cases live in individuals' heads or scattered files; exit criteria are "whatever felt done." |
| L2 | A test plan exists per release but is often skipped under deadline pressure; test cases documented but not traced to requirements; defects tracked but not root-caused. |
| L3 | Risk-based test strategy followed consistently; traceability tracked; entry/exit criteria enforced; environments provisioned reliably; defect SLAs tracked. |
| L4 | Planning data (estimates, past defect patterns) actively shapes where testing effort goes; environment self-service; defect root-cause trends drive prevention work. |
| L5 | Predictive risk models suggest where to test based on code-churn/defect history; environments are ephemeral and on-demand; near-zero defect leakage from process gaps. |

## Coverage (Levels & Types of Testing)

| Level | Criteria |
|---|---|
| L1 | Only manual functional testing; no performance/security/a11y testing; pyramid inverted (all manual E2E). |
| L2 | Some automation exists at UI layer; non-functional testing is sporadic/pre-launch-only. |
| L3 | Pyramid respected (unit/API majority); security & a11y scans run every release; contract testing in place for microservices. |
| L4 | Full non-functional suite (perf, security, chaos) integrated into CI/CD gates; coverage metrics tracked and trending up. |
| L5 | Continuous testing in production (feature flags, canary, synthetic monitoring) supplements pre-release testing; coverage decisions are risk-model-driven, not checklist-driven. |

## Automation & Tooling

*(Cross-reference [04-Automation-Maturity/Automation-Maturity-Levels-and-Roadmap.md](../04-Automation-Maturity/Automation-Maturity-Levels-and-Roadmap.md) for the full deep-dive version of this rubric.)*

| Level | Criteria |
|---|---|
| L1 | No automation, or unmaintained record-and-playback scripts nobody trusts. |
| L2 | Basic scripted automation exists, siloed per engineer, inconsistent framework/style, runs manually/ad hoc. |
| L3 | Standardised framework, version-controlled and reviewed, integrated into CI, runs on a schedule with reasonable stability. |
| L4 | Automation gates merges/deploys; parallelised execution; flaky-test management is active; scaled consistently across services. |
| L5 | Self-healing locators, AI-assisted authoring/maintenance, predictive test selection (only run tests impacted by the change); automation is a competitive advantage, not overhead. |

## AI Adoption

*(Cross-reference [05-AI-in-Testing/AI-in-Testing-Maturity-Model-and-Governance.md](../05-AI-in-Testing/AI-in-Testing-Maturity-Model-and-Governance.md) for full detail.)*

| Level | Criteria |
|---|---|
| L1 | No AI usage in the test lifecycle. |
| L2 | Individuals use public AI tools ad hoc/ungoverned ("shadow AI") for test case ideas or debugging — no policy, no review gate. |
| L3 | Org-approved AI tools used for specific, bounded tasks (test case drafting, log summarisation) with a mandatory human review gate. |
| L4 | AI integrated across multiple lifecycle stages (design, script generation, defect triage, visual comparison) with measured impact and governance compliance tracked. |
| L5 | AI materially drives test prioritisation/selection and autonomous maintenance, with human oversight focused on exceptions; impact is quantified and reported as a KPI. |

## Competency, Governance & Culture

| Level | Criteria |
|---|---|
| L1 | No defined tester role expectations; quality is "QA's job"; no metrics reported to leadership. |
| L2 | Some skills tracking exists but informally; metrics collected but not consistently reviewed. |
| L3 | Skills matrix and development plans in place; KPIs reported on a standard cadence; whole-team quality ownership emerging. |
| L4 | Career paths for QE/SDET exist; KPIs actively reviewed and drive resourcing decisions; strong developer-tester collaboration. |
| L5 | The team is a training ground/benchmark for the org; culture treats a quality concern raised late as acceptable to act on (psychological safety); metrics are benchmarked externally. |

## Using this with the composite score

If a team's numeric composite lands at L3 but the rubric evidence clearly reads as L2 (e.g., a dashboard exists but nobody looks at it, so it's not actually driving decisions), the assessor documents the discrepancy and assigns the rubric-supported level. This prevents "dashboard theatre" from inflating a score.
