# Automation Maturity — Capability & Capacity Deep-Dive Assessment

The base questionnaire (sections G/H) gives a summary automation score. Because automation compounds — a weak framework silently taxes every future sprint — every team gets this deeper assessment at least twice yearly, even Grade A teams.

Score each item 0–4 using the same anchors as the base questionnaire. This deep-dive splits into **Capability** (is it well-built?) and **Capacity** (can it scale and does it get run?) — a team can have excellent capability but poor capacity (e.g., a great framework only one person knows how to extend).

## Part 1 — Capability (framework quality)

1. **Architecture** — Is there a layered framework (page/screen objects or equivalent abstraction, reusable utilities, config-driven environment switching) rather than copy-pasted scripts?
2. **Maintainability** — Can a locator/API change be fixed in one place, not across dozens of tests?
3. **Data-driven / keyword-driven design** — Are test scenarios parameterised from data rather than hard-coded per test?
4. **Code quality practices** — Is test automation code linted, reviewed, and held to the same standard as production code?
5. **Cross-layer coverage** — Does automation exist at unit, API, and UI layers (pyramid-shaped), or is it UI-heavy (inverted pyramid, expensive and brittle)?
6. **Self-healing / resilient locators** — Does the framework tolerate minor UI changes without breaking (AI-assisted locator healing, resilient selectors)?
7. **Cross-browser/device abstraction** — Can the same suite target multiple browsers/devices via config, not duplicated suites?
8. **API/contract test automation** — Are service contracts automated (not just UI-driven checks of API behaviour)?
9. **Performance test automation** — Is load/performance testing scripted and repeatable, not a one-off manual exercise?
10. **Reporting & observability** — Do automation runs produce rich, debuggable reports (screenshots, video, trace logs on failure), not just pass/fail counts?

## Part 2 — Capacity (scale, integration, sustainability)

1. **CI/CD integration depth** — Does automation run on every PR/commit, nightly, and pre-release, with results visible in the PR itself?
2. **Gating authority** — Can/does the suite actually block a merge or deploy when it fails, or is it advisory only (routinely overridden)?
3. **Parallelisation & execution speed** — Is execution distributed across a grid/cloud runners to keep feedback under a target time (e.g., <30 min for PR-gating suite)?
4. **Flaky test management** — Is there an active process (quarantine, auto-retry with tracking, root-cause fixing) rather than ignoring/re-running until green?
5. **Dedicated capacity** — Is there headcount/time explicitly allocated to automation maintenance (SDET ratio), or is it done in the gaps between manual testing?
6. **Onboarding/bus factor** — Can a new team member extend the framework within days using documentation, or does it depend on one person's tribal knowledge?
7. **Reuse across teams** — Are framework components/libraries shared across teams via the COE, or is every team building from scratch?
8. **Cost governance** — Is cloud/device-farm/grid spend on automation tracked and justified against ROI?

## Composite Automation Maturity Level

Average Part 1 and Part 2 separately, then combine using the same 0–4 → L1–L5 mapping as [Scoring-and-Weighting-Guide.md §5](../02-Assessment-Questionnaire/Scoring-and-Weighting-Guide.md). Report **both** sub-scores — a "Capability L4 / Capacity L2" team needs investment in headcount/CI integration, not more framework engineering; the inverse needs the opposite. Collapsing these into one number, as noted in the base model, hides exactly this distinction.

Feed the resulting level into [Automation-Maturity-Levels-and-Roadmap.md](Automation-Maturity-Levels-and-Roadmap.md) to generate the advancement plan.
