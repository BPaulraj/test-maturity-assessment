# Test Artefact Approval & Sign-off Standard

Purpose: not every test artefact carries the same approval weight, and "approval" that lives only in a verbal okay or a chat thread is not auditable. This standard defines which artefacts need sign-off, from whom, and what makes a sign-off a real, documented record rather than an assertion.

## 1. Artefact Approval Matrix

| Artefact | Required approver(s) | When | Documented as |
|---|---|---|---|
| Test Strategy / Test Plan (per product/service) | Engineering Manager + Test COE (+ Security for Tier 1, + Compliance/Legal if regulated) | Annually, or at major scope change | Signed-off version in the test mgmt tool/wiki, approver name + date attached |
| Test cases for Tier 1 compliance/regulated features | Compliance/Legal + Product | Before first execution | Approval flag/comment on the test case record |
| UAT test cases / acceptance scenarios | Product Owner / Business stakeholder | Before UAT execution begins | Sign-off recorded against the UAT cycle in the test mgmt tool |
| Non-functional test plan (perf/security/a11y) for Tier 1 | Security (DAST), Platform/SRE (performance), Accessibility SME (a11y) | Before the dedicated NFT cycle starts | Recorded in the release's pre-production checklist |
| New automation tool/category adoption | Test COE | Before adoption | Exception/approval record per [Org-Test-Policy.md §7](Org-Test-Policy.md#7-exceptions-process) |

An artefact not on this list does not require formal sign-off — this matrix exists precisely so approval overhead is targeted, not blanket.

## 2. Sprint Package Sign-off

At the end of every sprint, a **Sprint Package Sign-off record** is produced containing:

- Scope: stories delivered in the sprint.
- Test execution summary: pass/fail/skip counts against plan.
- Open defects with severity/priority (per [Defect-Management-Standard.md](Defect-Management-Standard.md)).
- Known issues carried forward from prior sprints.
- Exit-criteria status per [Entry-Exit-Criteria-and-DoD.md](Entry-Exit-Criteria-and-DoD.md).

**Signed by:** Team QE/SDET Lead (test completeness) and Product Owner (business acceptance), recorded at Sprint Review and attached to the sprint record in the work-tracking tool.

## 3. Release Package Sign-off

Before a release passes the pre-production gate ([Sprint-and-Release-Testing-Cadence.md §4.2](../08-Agile-Scrum-Practices/Sprint-and-Release-Testing-Cadence.md)), a **Release Package Sign-off record** is produced containing:

- Full regression summary and non-functional test summary.
- Non-negotiables checklist status ([Org-Test-Policy.md §5](Org-Test-Policy.md#5-non-negotiables)).
- Known issues / risk register with each risk-acceptance decision and decision-maker (see [Defect-Management-Standard.md §9](Defect-Management-Standard.md)).
- Rollback/kill-switch validation status (Tier 1).

**Signed by:** Test COE representative or Team QE Lead (test readiness), Engineering Manager (technical readiness), and Product/Business owner (business go/no-go). For Tier 1, Security also signs off if any DAST finding remains open at release time.

This record **is** the artefact the pre-production gate checks for — a release does not pass the gate on a verbal "looks good," it passes on this document.

## 4. What Makes a Sign-off Valid

A sign-off record is only valid when it states:
1. The named approver and their role.
2. The date.
3. The specific version/build being approved.
4. Any conditions attached (e.g., "approved provided known issue #1234 is fixed by the next release").

A chat message, a verbal "go ahead," or an approval with no named build/version does not satisfy this — consistent with the evidence-gating principle used throughout this framework (see [Scoring-and-Weighting-Guide.md §1](../02-Assessment-Questionnaire/Scoring-and-Weighting-Guide.md)).

## 5. Assessment Hook

Scored under [Questionnaire.md](../02-Assessment-Questionnaire/Questionnaire.md) sections A and C; evidenced per [Evidence-Checklist.md](../02-Assessment-Questionnaire/Evidence-Checklist.md).
