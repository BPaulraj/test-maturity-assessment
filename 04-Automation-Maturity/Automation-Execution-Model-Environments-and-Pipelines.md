# Automation Execution Model — Environments & Pipelines

Purpose: "automation runs in CI" isn't specific enough to operate against. Different suite tiers need different run frequencies, different environments, and different pipeline stages — and the environment used to judge suite *health* has to be stable enough that infrastructure noise doesn't get misdiagnosed as test flakiness.

## 1. Suite Tier → Frequency → Environment → Pipeline Stage

| Suite tier | Frequency | Environment | Pipeline stage |
|---|---|---|---|
| Smoke | Every commit/PR | Ephemeral/Dev, or a CI-spun-up instance | PR pipeline — fast feedback, minutes |
| Sanity | Every merge to main | SIT/QA (shared) | Post-merge pipeline |
| Full Regression | Nightly, and always pre-release | SIT/QA (stable) | Scheduled nightly pipeline + pre-release pipeline |
| Non-functional (perf, DAST, manual a11y) | Per feature-complete / per release, per [NFR-and-Specialized-Testing-Placement-in-STLC.md](../08-Agile-Scrum-Practices/NFR-and-Specialized-Testing-Placement-in-STLC.md) | Staging / dedicated Performance environment | Pre-release pipeline, gated stage |
| Release Candidate full pass | Every release candidate | Staging / Pre-prod (prod-parity, per [Test-Environment-Strategy.md](../01-Policy-and-Standards/Test-Environment-Strategy.md)) | Release pipeline — blocking gate |

## 2. Which Environment to Judge Suite Health From

Automation suite health — flaky-test detection and execution-time trend, per [In-Sprint-Automation-and-Flaky-Test-Management.md §3](In-Sprint-Automation-and-Flaky-Test-Management.md) — must be judged from a **stable, dedicated** environment: the nightly full-regression run against SIT/QA, not the PR-pipeline smoke run against an ephemeral environment.

Ephemeral/ad hoc environments carry their own noise — spin-up variability, shared-resource contention — that gets misattributed to test flakiness if that's where health is measured. A practical diagnostic: **if a test is flaky in the PR-pipeline smoke run but stable in the nightly stable-environment run, the root cause is very likely environment/infrastructure, not the test itself** — investigate the environment before quarantining the test.

## 3. Pipeline Design Principles

- **Fail-fast ordering**: smoke before sanity before full regression — don't run a 45-minute full suite before a 2-minute smoke check would have caught the same failure.
- **Result ingestion**: every pipeline stage's results feed the test management tool automatically, per [Test-Artefact-and-Tooling-Standard.md §1](../01-Policy-and-Standards/Test-Artefact-and-Tooling-Standard.md), not pasted in after the fact.
- **Gates block, they don't just notify**: a failed gate prevents promotion to the next pipeline stage — it does not merely raise an alert while the pipeline continues on.

## 4. Assessment Hook

Scored under [Questionnaire.md Section H](../02-Assessment-Questionnaire/Questionnaire.md).
