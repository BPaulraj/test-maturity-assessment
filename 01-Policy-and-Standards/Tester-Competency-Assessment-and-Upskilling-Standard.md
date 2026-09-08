# Tester Competency Assessment & Upskilling Standard

Purpose: a skills matrix filled in once and never revisited is a document, not a system. This standard defines how often testers' capability is actually reassessed, against what rubric, and how upskilling progress is tracked between assessments rather than only discovered at the next one.

## 1. Assessment Cadence

- **Every 6 months** — a full reassessment across all dimensions (§2), aligned with but distinct from performance review cycles: this is a capability map, not a performance rating.
- **Quarterly check-in** — a lighter-weight progress check for anyone currently on an active upskill plan, folded into the quarterly maturity review.

## 2. Assessment Dimensions & Levels

Each tester is rated on every applicable dimension at one of four levels — **Novice / Practitioner / Proficient / Expert** — using a defined behavioural anchor per level, not a self-declared number:

| Dimension | Novice | Expert |
|---|---|---|
| Manual testing techniques | Executes given test cases | Designs test cases using equivalence partitioning, boundary value, state-transition analysis unprompted; mentors others |
| Automation | Executes existing automated tests | Designs and extends the shared framework, mentors others, contributes to org-wide reusable components |
| Tooling (approved categories) | Uses the tool for basic execution/reporting | Configures/administers the tool, builds integrations, trains others |
| Non-functional testing literacy (perf/security/a11y) | Aware of the standards, executes checklist items | Designs non-functional test scenarios and interprets results independently |
| AI-augmented testing | No usage | Effectively and safely uses approved AI tools per [AI-Adoption-Questionnaire-and-Rubric.md](../05-AI-in-Testing/AI-Adoption-Questionnaire-and-Rubric.md), reviews others' AI-assisted output critically |

## 3. Assessment Method

1. **Self-assessment** first, against the rubric in §2.
2. **Calibration** by the Team QE/SDET Lead, cross-checked against real evidence — automation repo commit history, test design review records, peer feedback — not accepted as self-report alone, consistent with the evidence-gating principle used across this framework.
3. Disagreements between self-assessment and calibration are discussed directly with the tester, not silently overridden.

## 4. Upskill Plan & Progress Tracking

Every identified gap becomes an entry on the tester's Individual Development Plan with:
- A specific target level and dimension.
- A target date.
- A concrete learning action (course, pairing with a Proficient/Expert peer, a stretch assignment).

Progress is tracked as **In Progress / On Track / At Risk / Complete**, reviewed at regular 1:1s — not left to surface only at the next 6-month assessment. Upskilling time draws from the protected tech-debt/enablement capacity defined in [Automation-Coverage-Decisioning-and-Technical-Debt.md §4](../04-Automation-Maturity/Automation-Coverage-Decisioning-and-Technical-Debt.md) — an upskill plan with no protected time behind it is a document, not a plan.

## 5. Org Roll-Up

Team-level (never individually-identified beyond the team) skills-gap heatmaps roll up to the Test COE and feed the training-academy investment decisions in [Org-Wide-Roadmap-Template.md §4](../06-Improvement-Planning/Org-Wide-Roadmap-Template.md).

## 6. Metrics

| Metric | Definition |
|---|---|
| Assessment Completion Rate | % of testers assessed on the defined cadence |
| Upskill Plan On-Time Rate | % of upskill plan milestones met by their target date |
| Skills-Gap Heatmap | Distribution of levels per dimension, team and org roll-up |

Feeds [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md).

## 7. Assessment Hook

Scored under [Questionnaire.md Section K](../02-Assessment-Questionnaire/Questionnaire.md).
