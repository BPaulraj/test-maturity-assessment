# AI in Testing — Adoption Questionnaire

Scored 0–4 using the same anchors as the base questionnaire. This deep-dive exists because AI adoption is moving faster than a yearly assessment cycle can track — run it every quarter, even for teams currently at L1.

## Use-Case Adoption

1. **Test case generation** — Is AI used to draft test cases/scenarios from requirements, with human review before acceptance?
2. **Script generation & maintenance** — Is AI used to generate or heal automation scripts (e.g., self-healing locators, AI-suggested fixes for broken selectors)?
3. **Test data generation** — Is AI used to generate realistic synthetic test data, reducing reliance on masked production data?
4. **Defect triage & RCA assistance** — Is AI used to summarise logs, cluster similar defects, or suggest likely root cause?
5. **Visual/UI comparison** — Is AI-based visual regression (beyond pixel-diffing) in use to reduce false positives from minor rendering changes?
6. **Risk-based test selection/prioritisation** — Is AI/ML used to predict which tests are most likely to catch a regression for a given change, to shrink what actually needs to run?
7. **Exploratory testing assistance** — Are LLM-based assistants used to suggest exploratory charters/edge cases a human might miss?
8. **Test code review** — Is AI used to review test code for anti-patterns (flakiness risk, poor assertions) before merge?

## Governance & Guardrails

9. **Approved tool usage** — Is AI usage limited to the org's approved/governed tool list, with no ungoverned "shadow AI" on code, logs, or data that may be confidential/PII?
10. **Human review gate** — Does every AI-generated test artefact pass through mandatory human review before being trusted as part of the regression suite (same standard as human-authored work)?
11. **Data classification compliance** — Is there a clear, followed rule for what data classification may/may not be sent to an AI tool (e.g., no raw customer PII, no unreleased source for external tools without contractual protection)?
12. **Hallucination/quality monitoring** — Is there a process to catch AI-generated test cases/assertions that are subtly wrong (testing the wrong thing, false confidence) rather than assuming AI output is correct by default?

## Measurement

13. **Impact measurement** — Is time saved or quality uplift from AI usage actually measured (even roughly), rather than assumed?
14. **Adoption trend tracking** — Is the % of AI-assisted artefacts tracked over time as a KPI (per [Metrics-and-KPI-Standard.md](../01-Policy-and-Standards/Metrics-and-KPI-Standard.md))?

## Rubric Summary (maps to levels in the AI maturity model)

| Score range (avg) | Level |
|---|---|
| 0.0–0.8 | L1 — No AI usage |
| 0.9–1.7 | L2 — Ungoverned/individual ("shadow AI") |
| 1.8–2.5 | L3 — Governed, bounded use cases |
| 2.6–3.3 | L4 — Integrated across lifecycle, measured |
| 3.4–4.0 | L5 — AI-driven autonomous testing with exception-based human oversight |

**Gating rule:** A team scoring L3+ on use-case adoption but L0–1 on Governance & Guardrails (items 9–12) is capped at **L2 overall** and flagged as a compliance risk — ungoverned AI usage on confidential data is a bigger organisational risk than no AI usage at all. See [AI-in-Testing-Maturity-Model-and-Governance.md](AI-in-Testing-Maturity-Model-and-Governance.md) for the governance policy this enforces.
