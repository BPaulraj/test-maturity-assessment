# Evidence Checklist

Assessors request these artefacts *before* the interview, so the session is spent validating and probing depth, not collecting documents live. A team unable to produce evidence for a section cannot score above 1 on that section regardless of narrative.

| Section | Evidence to request |
|---|---|
| A. Strategy & Planning | Test strategy doc(s), risk-tiering record, planning retro notes/estimate-vs-actual tracking, artefact approval matrix with a signed example |
| B. Test Design & Documentation | Link to live test case repository, sample of bidirectional traceability matrix (story→defect and defect→story), peer-review record for test cases, Master Test Pack with a sample sprint-end sync record and reuse-vs-new ratio |
| C. Execution & Reporting | Screenshot/link of live execution dashboard, a completed exit-criteria checklist from the last release, defect triage meeting cadence/notes, a sprint-package and a release-package sign-off record (named approver, role, date, version) |
| D. Levels/Types of Testing Coverage | CI config showing each test level running, latest performance/security/a11y scan reports, exploratory session charters/notes |
| E. Defect & Quality Management | Defect tracker export/dashboard showing discovery-stage tagging, root-cause analysis sample for a Critical/High defect, defect SLA policy doc, a hotfix-path example (production Critical defect), a non-functional defect example showing domain-specific classification and routing, a known-issue backlog item showing product-backlog placement and last review date |
| F. Environment & Data Management | IaC repo or provisioning workflow, environment uptime/availability report, dedicated performance environment's prod-parity/scaling-extrapolation documentation, data masking/synthetic data generation config, most recent automated PII-scan result from a data refresh |
| G. Automation Capability | Automation framework repo, code review records for test code, flaky-test quarantine dashboard with SLA/age per item, documented in-sprint-vs-defer automation criteria |
| H. Automation Capacity & CI/CD | CI pipeline config showing automated gate, suite execution time trend, parallelisation/grid configuration, tech-debt backlog showing deferred automation items with target sprint, sprint/PI capacity plan showing the protected tech-debt/enablement allocation and actuals, a suite-tier/frequency/environment/pipeline-stage matrix as actually configured |
| I. Tooling | Tool inventory with license/cost, integration diagram/config between test mgmt–CI–defect tracker |
| J. AI in Testing | List of AI tools in use with approval status, sample AI-generated artefact with review trail, any time-saved/impact tracking |
| K. Competency & Skills | Skills matrix document at the current assessment cycle's date, sample individual development plans with tracked milestone status, community-of-practice/brown-bag calendar |
| L. Governance & Metrics | KPI dashboard link, last quarter's improvement plan with closure status |
| M. Culture & Collaboration | UAT sign-off records showing business participation, sprint plan showing testing tasks estimated alongside dev tasks |
| N. Agile Ceremony Integration & Release Aggregation | Refinement/planning notes showing tester participation, a feature-level test pass record distinct from story-level runs, feature-level demo/showcase record, retro notes showing a standing quality discussion item, declared release cadence with a pre-production gate execution record |

## Rules for evidence

- Evidence must be **current** — dated within the assessment period (last quarter), not a one-time historical artefact.
- A live dashboard link is stronger evidence than a static export; prefer it whenever available.
- If evidence reveals a gap between what was claimed and what exists, the score reflects the evidence, and the gap itself becomes a note in the improvement plan (a coaching moment, not a punitive one).
