# RACI & Operating Model

## RACI Matrix

R = Responsible, A = Accountable, C = Consulted, I = Informed

| Activity | Test COE / Head of QE | Team QE/SDET Lead | Eng. Manager | Product Owner | AI Governance Board |
|---|---|---|---|---|---|
| Own & update Org Test Policy | A/R | C | C | C | C |
| Run team assessment (questionnaire) | R | R | I | I | — |
| Score & grade the team | A | C | I | I | — |
| Approve risk-tier exceptions | A | R (requests) | C | C | — |
| Author team improvement plan | C | A/R | C | I | — |
| Resource/fund improvement plan | I | R | A | C | — |
| Approve non-negotiable exceptions | A | R (requests) | C | I | — |
| Maintain approved AI tool list | C | I | I | I | A/R |
| Approve new AI tool for testing use | C | R (requests) | I | I | A |
| Investigate AI data-leakage incident | C | I | I | I | A/R (with Security) |
| Roll up org-wide roadmap | A/R | C | I | I | C |
| Present findings to leadership | A/R | C (data) | I | I | I |
| Maintain shared automation framework/library | A/R | C (contributes) | I | — | — |

## Operating Cadence

| Ritual | Frequency | Participants | Output |
|---|---|---|---|
| Team assessment cycle | Quarterly | Team QE Lead + COE assessor | Updated scores, grade, profile |
| Improvement plan review | Quarterly (with assessment) | Team QE Lead, Eng Manager, COE | Updated [Team Improvement Plan](Team-Improvement-Plan-Template.md) |
| KPI dashboard review | Monthly | Team QE Lead, Eng Manager | Trend check-in, early warning |
| AI Governance Board review | Quarterly | COE, Security, Legal, AI Governance Board | Updated approved tool list |
| Org maturity review with leadership | Quarterly | Head of QE, Eng leadership | Updated [Leadership Summary](../07-Leadership-Summary/) |
| Policy review | Semi-annual | Head of QE, Eng leadership | Updated [Org-Test-Policy.md](../01-Policy-and-Standards/Org-Test-Policy.md) |
| Ad hoc incident review | Triggered by non-negotiable breach or test-attributable production incident | Head of QE, affected team, Eng Manager | Root cause + immediate remediation plan |

## Escalation Path

1. Team-level gap → handled in Team Improvement Plan.
2. Cross-team/resourcing gap (needs budget or org decision) → escalated by Test COE to Engineering leadership via the quarterly org maturity review.
3. Non-negotiable violation or AI governance breach → immediate escalation outside the quarterly cadence, per the incident row above.

## Decision Rights

- **Test COE** decides tooling *category* standards and the maturity model/policy itself.
- **Teams** decide the specific tool/product within an approved category, and their own sprint-level prioritisation of improvement initiatives.
- **AI Governance Board** (cross-functional: COE + Security + Legal) is the sole approver of new AI tools for use on test artefacts, code, or data — no team or individual COE member can unilaterally approve a new AI tool.
