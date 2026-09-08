# Master Test Pack Maintenance Standard

Purpose: the **Master Test Pack** is the single canonical, versioned regression suite that release-level testing runs from. Left unmanaged, it either stagnates (sprint additions never make it in, so release testing runs against a stale baseline) or bloats (every sprint clones near-duplicate cases instead of reusing what's there). This standard prevents both.

## 1. Definition

The Master Test Pack is the curated set of test cases (manual and automated) that constitute the team's current regression baseline, organised per the taxonomy in [Test-Case-Management-and-Risk-Based-Design.md](Test-Case-Management-and-Risk-Based-Design.md). It is versioned and lives in the test management tool, per [Test-Artefact-and-Tooling-Standard.md](Test-Artefact-and-Tooling-Standard.md) — never a parallel spreadsheet kept "in sync" by hand.

## 2. Sprint-End Sync

At the end of every sprint, new or changed test cases authored during the sprint (story-level and feature-level) are reviewed and merged into the Master Test Pack. This is not optional or assumed — it is a checklist item on the Sprint Package Sign-off ([Test-Artefact-Approval-and-Signoff-Standard.md §2](Test-Artefact-Approval-and-Signoff-Standard.md)). A test case that stays in a story-level silo and never reaches the Master Test Pack will not be picked up by the next release regression run, silently leaving a coverage gap that looks, from the outside, like the story was properly tested.

## 3. Reuse-First Rule

Before authoring a new test case, in order:

1. **Search** the Master Test Pack for existing coverage of the scenario, or a closely related one.
2. If an existing case covers it with minor variation, **extend or parameterise** the existing case (e.g., add a new data row to a data-driven test) rather than cloning it into a near-duplicate.
3. Only author a **net-new** test case when no reasonable existing coverage exists, or the change introduces genuinely new behaviour.

Uncontrolled cloning is the single biggest driver of suite bloat: a 10,000-case suite where 40% are near-duplicates isn't more thorough — it's slower to run, harder to maintain, and no more likely to catch a real regression than a well-curated 6,000-case suite.

## 4. Ownership & Governance

Module owners (per [Test-Case-Management-and-Risk-Based-Design.md §6](Test-Case-Management-and-Risk-Based-Design.md)) are accountable for catching duplicate or near-duplicate additions during sprint-end sync. The existing quarterly test case health audit is the backstop for anything that slips through.

## 5. Metrics

| Metric | Definition |
|---|---|
| Test Case Reuse Rate | % of a sprint's test-coverage needs met by extending existing cases vs. net-new authoring |
| Master Pack Size Trend | Case count over time, by module — a pack that only ever grows, never prunes, is a maturity signal worth investigating |
| Duplication Rate | From the quarterly health audit (per [Test-Case-Management-and-Risk-Based-Design.md §5](Test-Case-Management-and-Risk-Based-Design.md)) |

These feed [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md).

## 6. Assessment Hook

Scored under [Questionnaire.md Section B](../02-Assessment-Questionnaire/Questionnaire.md).
