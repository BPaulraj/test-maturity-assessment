# Org-Wide Roadmap Template

*The Test COE fills this in by aggregating all [Team Improvement Plans](Team-Improvement-Plan-Template.md) each cycle. This is the input to the [Leadership Summary](../07-Leadership-Summary/).*

## 1. Grade Distribution Snapshot

| Grade | # Teams | # Teams (last cycle) | Trend |
|---|---|---|---|
| A | | | |
| B | | | |
| C | | | |
| D | | | |

## 2. Profile Shape Distribution

| Profile shape | # Teams | Common root cause seen this cycle |
|---|---|---|
| Process gap | | |
| Automation gap | | |
| AI-lagging | | |
| Foundational | | |

## 3. Phased Org Investment Plan

### Phase 1 (this quarter) — Stabilize
- Target: all Grade D ("Foundational") teams get COE-embedded support, not just a self-service plan.
- Target: close any open non-negotiable violations org-wide (list them explicitly, owner, date).

### Phase 2 (next quarter) — Standardize
- Target: move Grade C "Process gap" teams to Grade B via documentation/discipline fixes (lower cost, faster).
- Target: begin shared automation framework/library consolidation for "Automation gap" teams (see [Automation-Maturity-Levels-and-Roadmap.md](../04-Automation-Maturity/Automation-Maturity-Levels-and-Roadmap.md)).

### Phase 3 (2 quarters out) — Scale Automation
- Target: Grade B teams advance automation capacity (CI gating, parallelisation, dedicated SDET ratio).
- Target: stand up/expand the org AI-tool governance board and approved tool list if not already mature (see [AI-in-Testing-Maturity-Model-and-Governance.md](../05-AI-in-Testing/AI-in-Testing-Maturity-Model-and-Governance.md)).

### Phase 4 (3–4 quarters out) — Optimize & Lead
- Target: Grade A teams pilot AI-augmented/self-healing automation and predictive test selection; document as org best practice.
- Target: at least one Grade A team's practice is formally adopted into the [Org-Test-Policy.md](../01-Policy-and-Standards/Org-Test-Policy.md) or standards docs.

## 4. Org-Level Investments (not team-specific)

| Investment | Rationale | Owner | Timeline |
|---|---|---|---|
| Test COE enablement function staffing | Shared framework/library maintenance, reduces duplicated effort | | |
| Training academy (manual→automation→AI-augmented career path) | Closes competency gap at scale | | |
| Approved AI tool procurement & governance board | Required before safe L3+ AI adoption org-wide | | |
| Tooling consolidation (test mgmt / CI / defect tracking categories) | Enables org-wide reporting, reduces license sprawl | | |
| Shared test data management platform (masking/synthetic generation) | Non-negotiable compliance at scale, reduces per-team rebuild | | |

## 5. Governance Cadence

- **Quarterly:** full re-assessment cycle (questionnaire → scoring → grading → plan update) per [00-Program-Overview/README.md](../00-Program-Overview/README.md).
- **Monthly:** KPI dashboard review (see [Metrics-and-KPI-Standard.md](../01-Policy-and-Standards/Metrics-and-KPI-Standard.md)) — no new assessment, just metric trend check-in.
- **Ad hoc:** any non-negotiable violation or production incident with a testing root cause triggers an immediate review, not a wait for the next quarterly cycle.

## 6. Roll-up Risks to Flag to Leadership

List any team/grade-level risk that needs executive sponsorship to unblock (budget, cross-team dependency, org restructuring need) — this feeds directly into [07-Leadership-Summary](../07-Leadership-Summary/).
