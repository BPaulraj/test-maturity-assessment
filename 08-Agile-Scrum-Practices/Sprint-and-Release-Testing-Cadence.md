# Sprint & Release Testing Cadence

Purpose: this is the piece that ties the whole framework into the actual rhythm of a Scrum team. It answers three related questions: how do testers work shift-left across every ceremony (not just "at the end")? Does passing every story's acceptance criteria mean the feature actually works? And how often does the business actually see the thing being built?

## 1. Shift-Left Across Ceremonies

Testing is not a phase that starts when a story's code is "complete" — it is present, in a different form, at every ceremony.

| Ceremony | Testing activity | Anti-pattern this replaces |
|---|---|---|
| **Backlog Refinement / Grooming** | Tester reviews AC for testability; raises non-functional and edge-case questions before the story is pulled into a sprint | AC written without a tester in the room, discovered to be untestable mid-sprint |
| **Sprint Planning** | Test approach and estimate discussed alongside the dev estimate, as one conversation, not tacked on after; test data/environment needs flagged here | Test effort invisibly absorbed into "dev is done" estimates, then discovered too late to resource |
| **Daily Standup** | Testers report blockers exactly like developers do — environment down, data missing, AC ambiguity — as first-class impediments | Testing status only mentioned when it's already late |
| **Story development** | Dev and tester pair on AC clarification and test case drafting *before* code is complete; exploratory and automated checks begin against any testable slice as soon as it exists | Testing only starts once a developer declares "code complete" |
| **Sprint Review / Demo** | Story-level demo to the Product Owner happens as each story completes, rolling through the sprint — see §3 | All demos batched into the last day of the sprint, discovering issues with no time left to fix them |
| **Retrospective** | A standing agenda item: "what escaped, why, what do we change" — feeds [Defect-Management-Standard.md §5](../01-Policy-and-Standards/Defect-Management-Standard.md) escape analysis | Retro discusses velocity and process friction but never quality trend |

This is the practical, ceremony-by-ceremony expression of [Org-Test-Policy.md principle 3](../01-Policy-and-Standards/Org-Test-Policy.md) ("shift-left and shift-right") and of Questionnaire section M (Culture & Stakeholder Collaboration).

## 2. Three Levels of "Done" — Story, Feature, Release

Story-level AC verification alone does not prove a feature works. Two stories can each individually pass their own AC and still be incompatible once combined — this is the most common blind spot in agile testing, and it's why this framework adds an explicit **feature-level gate** between story and release (updating the [Entry-Exit-Criteria-and-DoD.md](../01-Policy-and-Standards/Entry-Exit-Criteria-and-DoD.md) Definition of Done accordingly).

| Level | Scope | When it happens | What it validates |
|---|---|---|---|
| **Story** | The story's own AC, in isolation — may use mocks/stubs for not-yet-built dependent stories | As each story completes | The narrow slice does what its AC says |
| **Feature** | End-to-end scenarios crossing every story that composes the feature; integration between those stories; non-functional checks (perf/security/a11y) that only make sense once the feature is whole | Once all stories for the feature are Done — typically the sprint the feature completes, or a stabilisation buffer | The feature works as a whole, not just its parts |
| **Release** | Cross-feature interaction, full regression, full non-functional suite, all non-negotiables | Before a release cutting across multiple features | Nothing shipped together breaks something shipped alongside it |

**Feature-level aggregation testing is scheduled as its own backlog item** — it is never assumed to happen "for free" once the last story is marked Done. A feature is not Done until this pass has run, in addition to every constituent story's own Done state.

## 3. Demo / Showcase Cadence

| Level | Audience | Cadence | Purpose |
|---|---|---|---|
| **Story** | Product Owner (informal) | Rolling, as each story completes within the sprint | Quick confidence check — not a formal gate |
| **Sprint** | Broader Scrum team + immediate stakeholders | End of every sprint (standard Sprint Review) | Formal demo of everything completed; testers present known issues/risk alongside the demo, not just "it works" |
| **Feature** | Business stakeholders beyond the Scrum team | Once the feature-level aggregation pass (§2) is complete | Paired with feature-level test results; this is typically where formal UAT (per [Testing-Types-Standards.md](../01-Policy-and-Standards/Testing-Types-Standards.md)) happens |
| **Release** | Leadership / release approval group | Before a Tier 1/2 release | Go/no-go demo plus exit-criteria review, not a demo alone |

A story-level demo passing is never presented as if it were a feature-level or release-level sign-off — each level of demo answers a different question, and conflating them is how integration gaps reach production undetected.

## 4. Release Cadence & the Pre-Production Gate

Sprint cadence and release cadence are **not the same thing**, and conflating them is how a package ends up shipping straight from a sprint's dev/test environment to production with no independent check.

### 4.1 Release Models

| Model | Description |
|---|---|
| **Continuous Deployment** | Every merge (or every sprint) ships, relying on very strong automated gates to substitute for a separate release cycle |
| **Release Train (fixed cadence)** | Releases happen on a fixed calendar cadence (e.g., every 2 weeks) regardless of sprint boundaries, batching one or more sprints' worth of change |
| **Milestone / Version release** | Release timing is tied to feature completeness rather than the calendar |

Whichever model a team uses, it is **declared explicitly** — "our release cadence is every 2 weeks" — as part of the team's profile, reviewed by the Test COE, and used to plan regression scope (§4.3).

### 4.2 The Pre-Production Gate (non-negotiable regardless of model)

A package never goes straight from a sprint's dev/test environment to production. Every release — whatever the cadence — passes through a **pre-production/staging environment** that mirrors production configuration (per [Test-Environment-Strategy.md](../01-Policy-and-Standards/Test-Environment-Strategy.md)) and executes the full Release-level Definition of Done (per [Entry-Exit-Criteria-and-DoD.md §7](../01-Policy-and-Standards/Entry-Exit-Criteria-and-DoD.md)) before production deployment. This is also where any full performance test, dynamic DAST scan, or manual accessibility check that couldn't run at feature-level (per [NFR-and-Specialized-Testing-Placement-in-STLC.md](NFR-and-Specialized-Testing-Placement-in-STLC.md)) gets its last chance to run before production.

### 4.3 Regression Scope Scales With Batch Size

The more sprints' worth of change a release batches together, the larger the regression blast radius — a release-level regression pass sized for "one sprint of change" is not sufficient for a release train that accumulated three sprints of merges. Regression scope for a given release is planned against the actual accumulated change set, not run at a fixed size regardless of what's in the batch.

## 5. Assessment Hook

This cadence is scored via a new Questionnaire section — see [Questionnaire.md Section N](../02-Assessment-Questionnaire/Questionnaire.md) — and evidenced per the updated [Evidence-Checklist.md](../02-Assessment-Questionnaire/Evidence-Checklist.md).
