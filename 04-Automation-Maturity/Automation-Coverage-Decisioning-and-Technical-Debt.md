# Automation Coverage Decisioning & Technical Debt

Purpose: not everything can or should be automated within the sprint that introduces it. This document gives a concrete framework for deciding what must be automated now vs. what can reasonably wait, a real mechanism for the backlog that results (not a graveyard), and the protected capacity that keeps that mechanism from being permanently starved by feature work.

## 1. What Must Be Automated In-Sprint

A case is a **must-automate-now** candidate when it meets all of:
- It is **P0/P1** priority (per [Test-Case-Management-and-Risk-Based-Design.md](../01-Policy-and-Standards/Test-Case-Management-and-Risk-Based-Design.md)).
- The scenario/UI/API is **stable** — not expected to change again imminently.
- It will be **run repeatedly** (a genuine regression-suite candidate, not a one-off exploratory check).
- It's technically feasible with the **current** automation framework without a disproportionate one-off investment.

A case is **acceptable to defer** when:
- It's genuinely one-off/exploratory, not a repeat-run regression candidate.
- It's P2/P3 priority.
- It's blocked by a framework capability gap that itself needs investment (e.g., a new plugin/tool).
- The underlying feature is still expected to change significantly (automating now means rewriting almost immediately).

## 2. The Agreement Point

The coverage target for a story/feature — which P0/P1 cases will be automated in-sprint vs. deferred — is **explicitly agreed at sprint planning**, alongside the test-approach discussion in [Sprint-and-Release-Testing-Cadence.md §1](../08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md). It is not decided unilaterally by whoever happens to pick up the story, and it is visible on the story/feature as an explicit checklist or sub-task, not an implicit understanding.

## 3. Handling Deviation — the Technical-Debt Path

Any P0/P1 case not automated in-sprint as agreed becomes an explicit, tracked technical-debt backlog item:

1. **Same priority tag carries over** — a deferred P0 automation item is logged as P0 tech debt, not automatically deprioritised for being "just tech debt."
2. **Given a real target** — the default expectation is the **immediate next sprint**; a later target is only acceptable when genuinely blocked (framework gap, environment dependency), with the specific blocker and target sprint/PI stated explicitly — never "someday."
3. **Tracked on a visible tech-debt backlog**, not buried inside a generic "chores" catch-all, and reviewed at the automation suite health cadence ([In-Sprint-Automation-and-Flaky-Test-Management.md §3](In-Sprint-Automation-and-Flaky-Test-Management.md)).
4. **Escalation on repeat rollover** — an item that rolls over more than twice without being addressed is escalated to the Engineering Manager as a resourcing signal, not re-logged silently for a third sprint.

## 4. Protecting Capacity for Tech Debt & Enablement

Sprint/PI planning reserves an **explicit capacity allocation** for: deferred automation from §3, flaky-test fixes, automation framework/tooling maintenance, and team upskilling/training.

- **Guideline: 10–20% of sprint or PI capacity**, set per team based on current automation maturity level — a team at Automation Maturity L2 building its framework from scratch typically needs the higher end; an L4 team with a mature, stable suite can run leaner.
- **This allocation is protected** — it appears as its own line in sprint/PI capacity planning, the same way an SRE team protects toil/on-call time, and is not the first thing silently cut when a feature deadline tightens.
- **Upskilling draws from this same allocation** — training time for a new tool, framework, or AI-assisted testing skill (per [AI-Adoption-Questionnaire-and-Rubric.md](../05-AI-in-Testing/AI-Adoption-Questionnaire-and-Rubric.md)) ties directly into the individual development plans scored under [Questionnaire.md Section K](../02-Assessment-Questionnaire/Questionnaire.md).
- **Tracked and reported**: planned vs. actually-delivered tech-debt/enablement capacity, every sprint/PI. A team that plans 15% but consistently delivers 2% has a capacity-protection problem — that gap is itself a leadership-visible metric (see [Metrics-and-KPI-Standard.md](../01-Policy-and-Standards/Metrics-and-KPI-Standard.md)), not a private team failure to quietly absorb.

## 5. Assessment Hook

Scored under [Questionnaire.md](../02-Assessment-Questionnaire/Questionnaire.md) sections G/H (coverage decisioning) and K/L (capacity protection, governance visibility).
