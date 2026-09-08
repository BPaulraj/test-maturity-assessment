# Automation Maturity Levels & Advancement Roadmap

## Level Definitions

| Level | Name | State |
|---|---|---|
| **L1** | Manual / No Automation | Testing is entirely manual, or limited to unmaintained record-and-playback scripts that break constantly and are ignored. |
| **L2** | Basic Scripted, Siloed | Individual engineers write automation in their own style; runs manually or on an unreliable schedule; no shared framework; high maintenance burden relative to value. |
| **L3** | Framework-Driven, CI-Integrated | Standardised framework, version-controlled, code-reviewed; runs in CI on a schedule; reasonably stable; pyramid shape is emerging (some API/unit automation, not just UI). |
| **L4** | Scaled, Gating, Parallelised | Automation gates PR merges and deploys across most/all services; parallel execution keeps feedback fast; flaky-test management is active; dedicated SDET capacity exists; framework components are reused across teams. |
| **L5** | AI-Augmented Continuous Testing | Self-healing locators, AI-assisted test generation/maintenance, predictive/impact-based test selection (only run what the change affects), continuous testing extends safely into production (canary/synthetic). Automation is a measured competitive advantage. |

## Advancement Roadmap

### L1 → L2: "Stop the bleeding"
- **Focus:** Pick one framework/tooling category org-wide (per [Testing-Types-Standards.md](../01-Policy-and-Standards/Testing-Types-Standards.md)) and stop new ad hoc scripts being written outside it.
- **Actions:** Baseline current manual regression suite; identify top 20% of test cases by run-frequency/risk for first automation candidates; put automation code under version control immediately.
- **Typical timeframe:** 1 quarter.
- **Team structure implication:** Identify/assign at least one automation champion, even if not a dedicated SDET yet.

### L2 → L3: "Make it a system, not a script pile"
- **Focus:** Introduce a layered framework (abstraction layer, config-driven environments, data-driven design). Wire into CI on a schedule.
- **Actions:** Refactor existing scripts into the shared framework; add code review for test code; start tracking flaky tests instead of ignoring them; begin API-layer automation to rebalance the pyramid.
- **Typical timeframe:** 1–2 quarters.
- **Team structure implication:** At least one part-time or rotating SDET role recognised formally.

### L3 → L4: "Make it fast, trusted, and everywhere"
- **Focus:** Move automation from "runs nightly and someone checks it" to "gates the merge and everyone trusts it."
- **Actions:** Parallelise execution (grid/cloud runners); set and enforce a feedback-time SLO (e.g., <30 min); formal flaky-test quarantine process; establish dedicated SDET capacity ratio (e.g., 1 SDET per N developers, tuned to context); publish reusable framework components to the org COE library.
- **Typical timeframe:** 2–3 quarters.
- **Team structure implication:** Dedicated SDET role(s), not just a champion; automation maintenance time explicitly planned into sprints.

### L4 → L5: "Let the system get smarter than the checklist"
- **Focus:** Introduce AI/ML-assisted capability and shift from "run everything" to "run what matters."
- **Actions:** Adopt self-healing locator tooling; pilot AI-assisted test authoring/maintenance under the governance in [05-AI-in-Testing](../05-AI-in-Testing/); implement impact-based test selection (map code changes to affected tests to avoid full-suite runs every time); extend continuous testing into production via canary releases/synthetic monitoring; formally measure and report automation ROI as a KPI.
- **Typical timeframe:** Ongoing — this is a continuous-improvement level, not a destination with an end date.
- **Team structure implication:** SDETs work increasingly on framework/platform capability rather than one-off test authoring; close partnership with a Test COE / platform engineering function.

## Notes for the Improvement Plan

- Do not attempt to skip a level — an L2 team chasing AI-augmented self-healing before it has a stable, reviewed framework will produce more automation debt, not less.
- Capability and Capacity (see [Automation-Capability-Assessment.md](Automation-Capability-Assessment.md)) can be at different levels simultaneously; the roadmap step chosen should target whichever sub-score is the actual bottleneck.
- This roadmap feeds directly into the [Team-Improvement-Plan-Template.md](../06-Improvement-Planning/Team-Improvement-Plan-Template.md).
