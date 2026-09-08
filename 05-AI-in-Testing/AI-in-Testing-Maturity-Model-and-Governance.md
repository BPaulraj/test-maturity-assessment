# AI in Testing — Maturity Model & Governance Policy

## 1. Maturity Levels

| Level | Name | Description |
|---|---|---|
| **L1** | No AI Usage | AI plays no role in the test lifecycle. |
| **L2** | Shadow AI | Individuals use public/consumer AI tools ad hoc for test ideas, debugging help, or writing test code — with no policy, no data-handling rule, no review gate. This is a **risk state**, not a neutral starting point, because confidential code/data may already be leaving the org ungoverned. |
| **L3** | Governed, Bounded Use | Org-approved AI tools are used for specific, well-scoped tasks (test case drafting, log summarisation, non-sensitive data generation), with a mandatory human review gate before any artefact is trusted. |
| **L4** | Integrated & Measured | AI is used across multiple lifecycle stages (design, script generation/healing, defect triage, visual comparison, risk-based selection) with governance compliance and impact (time saved, quality uplift) actively tracked as KPIs. |
| **L5** | AI-Driven Autonomous Testing | AI materially drives test prioritisation, generation, and maintenance with minimal human intervention except for exceptions/high-risk changes; humans supervise and audit rather than author by default; impact is quantified and reported to leadership as a maturity differentiator. |

## 2. Why Governance Comes Before Adoption Speed

Unlike automation maturity, where slow-and-steady is mostly a cost issue, **ungoverned AI adoption is a direct risk vector**: source code, customer data, or unreleased feature details can leave the organisation's control the first time someone pastes them into an external tool. This is why the [AI-Adoption-Questionnaire](AI-Adoption-Questionnaire-and-Rubric.md) gates overall level on governance score, not just use-case breadth — a team doing more with AI but doing it ungoverned is **less** mature by this model than a team doing less but doing it safely.

## 3. Governance Policy

### 3.1 Approved Tools
- The Test COE (in partnership with Security/Legal) maintains an **approved AI tool list**, reviewed at least quarterly, split by what data classification each tool is cleared for.
- Any AI tool not on the list is "shadow AI" by definition, regardless of how it's used — requesting approval is the required path, not a post-hoc justification.

### 3.2 Data Classification Rules
| Data type | May be sent to an approved internal/enterprise AI tool? | May be sent to a public/consumer AI tool? |
|---|---|---|
| Public documentation, open-source code | Yes | Yes |
| Internal, non-sensitive test code/test cases | Yes | No |
| Confidential source code, architecture details | Only if tool has a contractual no-training/data-isolation guarantee | No |
| Customer PII, regulated data, real production data | No — synthetic/masked data only | No |

### 3.3 Human Review Gate (non-negotiable)
Every AI-generated or AI-modified test artefact (test case, script, assertion, test data set) must be reviewed by a human before it is merged/trusted as part of the regression suite — identical to the code-review bar for human-authored work. AI authorship does not exempt an artefact from this gate; it does not accelerate past it.

### 3.4 Hallucination & Quality Monitoring
- Track a sample of AI-generated test artefacts each cycle for correctness (does the assertion actually test what it claims to?), not just whether it runs and passes.
- A test that passes but asserts the wrong thing is worse than no test — it creates false confidence. This is called out explicitly because it is the most common AI-testing failure mode.

### 3.5 Escalation & Incident Response
Any suspected data leakage via an AI tool (confidential data pasted into an unapproved tool) is treated as a security incident and reported through the standard incident process, not just flagged to the test COE.

## 4. Measuring Impact (avoid AI-adoption theatre)

Track, per [Metrics-and-KPI-Standard.md](../01-Policy-and-Standards/Metrics-and-KPI-Standard.md):
- AI-Assisted Artefact Volume (trend, not a target — a team should not be pressured to inflate this)
- AI Artefact Acceptance Rate (how much AI output survives human review without major rework — a proxy for real usefulness)
- Time Saved via AI Assistance
- AI Governance Compliance (% through approved tools)

A high adoption number with a low acceptance rate indicates the team is generating AI output nobody actually uses — a signal to fix training/prompting practices, not to declare success.

## 5. Advancement Path

Advancement mirrors the automation roadmap's discipline: do not pursue L5 autonomous capability while L3's human-review-gate isn't consistently enforced. See [AI-Adoption-Questionnaire-and-Rubric.md](AI-Adoption-Questionnaire-and-Rubric.md) for the assessment that determines a team's current level, and feed the gap into the [Team-Improvement-Plan-Template.md](../06-Improvement-Planning/Team-Improvement-Plan-Template.md).
