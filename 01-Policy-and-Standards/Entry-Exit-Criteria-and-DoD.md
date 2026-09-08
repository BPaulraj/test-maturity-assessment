# Entry/Exit Criteria & Definition of Done

## 1. Definition of Ready (before a story enters a sprint)

- Acceptance criteria are written in a testable form (given/when/then or equivalent).
- Risk tier of the affected component is known (drives which standards apply).
- Test data / environment needs are identified, not discovered mid-sprint.
- Non-functional requirements (perf, security, a11y) are explicit when applicable, and stated as a **quantified, testable threshold** (e.g., "p95 response time < 300ms at 200 concurrent users"), never a qualitative statement like "should be fast" — see [NFR-and-Specialized-Testing-Placement-in-STLC.md §3](../08-Agile-Scrum-Practices/NFR-and-Specialized-Testing-Placement-in-STLC.md). A story/feature carrying a non-measurable NFR fails Definition of Ready.

## 2. Test Planning Entry Criteria

- Requirements/acceptance criteria are baselined (even if lightweight for agile teams).
- Risk assessment completed to determine depth of testing needed (see risk tiers in [Org-Test-Policy.md](Org-Test-Policy.md)).

## 3. Test Execution Entry Criteria

- Code has passed unit/component tests and static analysis in CI.
- Build is deployed to a stable, environment-parity test environment.
- Test data required for the scenarios is available and refreshed.

## 4. Test Execution Exit Criteria

- 100% of planned P1/critical test cases executed (not just "attempted").
- No open Critical/High severity defects without a documented, time-boxed waiver signed by Product + Engineering.
- Automated regression suite green on the release candidate build.
- Non-functional test results (perf/security/a11y where applicable) reviewed against thresholds.

## 5. Definition of Done — Story Level

A story is **Done** only when:
1. Code merged with unit/component tests passing in CI.
2. Acceptance criteria independently verified (by a tester or a peer developer, not solely the author).
3. Regression suite updated if new/changed behaviour affects existing coverage.
4. Defects found are logged, triaged, and Critical/High ones resolved or explicitly deferred with sign-off.
5. Relevant documentation (test cases, API contracts) updated.

## 6. Definition of Done — Feature Level

Passing every constituent story's own AC does **not** prove a feature works — two independently-correct stories can be incompatible once combined. A feature is **Done** only when, in addition to every constituent story meeting §5:

1. A feature-level aggregation test pass has run — end-to-end scenarios crossing every story that composes the feature, scheduled as its own backlog item, never assumed to happen automatically once the last story closes.
2. Integration between the feature's constituent stories is verified (not just each story against mocks/stubs of the others).
3. Non-functional checks that only make sense once the feature is whole (performance, security, accessibility) have run against the assembled feature.
4. A feature-level demo/showcase has been held per [Sprint-and-Release-Testing-Cadence.md §3](../08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md).

See [08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md](../08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md) for the full rationale and ceremony mapping.

## 7. Definition of Done — Release Level

A release is **Done** only when:
1. All story-level and feature-level DoD met for included scope.
2. Full regression + applicable non-functional suites passed on the release candidate.
3. Non-negotiables from [Org-Test-Policy.md §5](Org-Test-Policy.md) are satisfied with evidence attached (not asserted).
4. Rollback/kill-switch validated for Tier 1 services.
5. Release notes include known issues and their risk acceptance sign-off.
6. Post-release monitoring/synthetic checks are configured and owned.

## 8. Evidence Trail

Every gate above must leave an artefact (CI run link, signed-off waiver, dashboard snapshot). "We tested it" without a linked artefact does not satisfy exit criteria — this is what the [Evidence-Checklist.md](../02-Assessment-Questionnaire/Evidence-Checklist.md) checks for during assessment.
