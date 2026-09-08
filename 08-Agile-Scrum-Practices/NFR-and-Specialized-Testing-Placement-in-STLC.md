# NFR & Specialized Testing Placement in the STLC

Purpose: security (DAST), accessibility, and performance testing don't fit the same "test it in this story's sprint" rhythm as functional testing — some need a live, deployed build; some need an assembled feature; performance needs a dedicated environment entirely. This document pins each specialized testing type to a classic STLC stage and to a concrete cadence tier, so "when does this actually run" has one answer instead of being reinvented per team.

## 1. STLC Stages, Mapped to Agile Ceremonies

| Classic STLC stage | Agile equivalent |
|---|---|
| Requirement Analysis | Backlog Refinement |
| Test Planning | Sprint Planning |
| Test Case Design & Review | Story development (shift-left) |
| Test Environment Setup | Ongoing / dedicated for performance (see [Test-Environment-Strategy.md](../01-Policy-and-Standards/Test-Environment-Strategy.md)) |
| Test Execution | Story / Feature / Release level (see [Sprint-and-Release-Testing-Cadence.md](Sprint-and-Release-Testing-Cadence.md)) |
| Test Cycle Closure | Sprint Review / Retrospective, or Release sign-off |

This is the same ceremony mapping as [Sprint-and-Release-Testing-Cadence.md §1](Sprint-and-Release-Testing-Cadence.md); this document adds the placement detail for the testing types that don't fit the default story-level rhythm.

## 2. Placement by Testing Type

| Testing type | STLC stage(s) | Cadence tier | In-sprint or dedicated cycle |
|---|---|---|---|
| SAST + dependency/SCA scan | Test Execution | Story-level | **In-sprint** — automated on every commit/build; no dedicated cycle needed |
| DAST (automated dynamic scan) | Test Execution | Feature-level | Needs a deployed, running build — runs against a staging/feature environment once the feature is assembled, not against an in-progress story |
| DAST (manual pen-test) | Test Execution | Release-level | Outside sprint scope entirely — annual or per-major-release cadence per [Testing-Types-Standards.md](../01-Policy-and-Standards/Testing-Types-Standards.md) |
| Accessibility — automated scan (e.g., axe-core class of tooling) | Test Execution | Story-level | **In-sprint** — part of CI for any UI-bearing story |
| Accessibility — manual screen-reader spot check | Test Execution | Feature-level | Scheduled once the feature's UI is assembled, before the feature-level demo |
| Performance / Load — lightweight in-sprint smoke check (e.g., single-endpoint response budget) | Test Execution | Story-level | Can run in-sprint with lightweight tooling, if the endpoint is stable |
| Performance / Load — full load/soak test | Test Planning (NFR defined) + Test Execution | Feature or Release level | **Outside the single sprint by default** — needs the dedicated performance environment ([Test-Environment-Strategy.md §2](../01-Policy-and-Standards/Test-Environment-Strategy.md)) and a sufficiently complete build; still a committed obligation tracked against the feature/release, never indefinitely deferred |
| Contract testing | Test Execution | Story-level | In-sprint, part of CI |
| Chaos / Resilience (game days) | Test Execution | Release-level, scheduled | Twice yearly for Tier 1, per [Testing-Types-Standards.md](../01-Policy-and-Standards/Testing-Types-Standards.md) |
| Visual Regression | Test Execution | Story or Feature level | In-sprint where tooling supports it |

## 3. Non-Functional Requirements Must Be Measurable

An NFR captured at planning time is only useful if it's a testable threshold, not a sentiment. At Definition of Ready (per [Entry-Exit-Criteria-and-DoD.md](../01-Policy-and-Standards/Entry-Exit-Criteria-and-DoD.md)), a performance/security/accessibility NFR must be stated as a **quantified, measurable target**:

- **Not acceptable:** "The system should be fast."
- **Acceptable:** "p95 API response time < 300ms at 200 concurrent users."
- **Not acceptable:** "The page should be accessible."
- **Acceptable:** "Page passes WCAG 2.1 AA automated scan with zero critical/serious violations; primary user flow completable via screen reader."

A story or feature carrying a non-measurable NFR fails Definition of Ready and is sent back to refinement — this is not a formality, it's what makes the NFR testable at all.

## 4. When It Genuinely Can't Run In-Sprint

For anything that needs a dedicated environment or an assembled feature (full performance test, dynamic DAST, manual accessibility, chaos), the obligation does not disappear at the sprint boundary — it is explicitly scheduled at feature-completion or release-candidate stage and tracked as part of that feature's or release's Definition of Done (see [Entry-Exit-Criteria-and-DoD.md §6–7](../01-Policy-and-Standards/Entry-Exit-Criteria-and-DoD.md)). "The sprint ended" is never an acceptable reason for a performance or security obligation to quietly vanish — it moves to the next applicable gate, not off the books.

## 5. Assessment Hook

Scored via [Questionnaire.md Section D](../02-Assessment-Questionnaire/Questionnaire.md) (coverage, cadence-aware) and Section A/N items on measurable NFRs and feature/release-level NFR execution.
