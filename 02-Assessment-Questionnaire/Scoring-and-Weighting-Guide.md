# Scoring & Weighting Guide

## 1. Scoring a question

Use the 0–4 anchors in [Questionnaire.md](Questionnaire.md). Two rules keep scoring honest:

- **Evidence-gated scoring.** A score of 2 or higher requires a linked artefact (dashboard, repo, pipeline, doc) per [Evidence-Checklist.md](Evidence-Checklist.md). No evidence caps the score at 1, regardless of what's claimed verbally.
- **Assessor + self-score reconciliation.** The team self-scores first; an independent assessor (COE member or peer team lead) scores against the same evidence. A gap of ≥2 points on any question triggers a calibration discussion, not an automatic override in either direction.

## 2. Section score

Section score = average of question scores within that section (N/A questions excluded from the denominator).

## 3. Dimension weighting (for the composite/overall grade)

Sections map to four weighted dimensions used in the [Maturity Model](../03-Maturity-Model/Maturity-Model-Framework.md):

| Dimension | Questionnaire sections | Weight |
|---|---|---|
| **Process** (planning, design, execution, defect mgmt, environments, agile ceremony integration) | A, B, C, E, F, N | 35% |
| **Coverage** (levels/types of testing) | D | 20% |
| **Automation & Tooling** | G, H, I | 25% (cross-checked against [04-Automation-Maturity](../04-Automation-Maturity/) deep-dive) |
| **AI Adoption** | J | 10% (cross-checked against [05-AI-in-Testing](../05-AI-in-Testing/) deep-dive) |
| **Competency, Governance & Culture** | K, L, M | 10% |

Composite score = weighted sum of dimension averages (each dimension average is itself 0–4).

**How a dimension average is computed when it spans multiple sections:** the dimension average is the simple (unweighted) mean of its constituent section scores — each section counts once, regardless of how many questions it contains. This keeps a section with many questions (e.g., Coverage's 17 testing-type rows) from silently dominating a dimension that also includes a 3-question section, and keeps the calculation auditable by hand, not just by a tool.

## 4. Weakest-link gating (critical dimensions)

Regardless of the composite score, apply these caps:

- If **any non-negotiable** from [Org-Test-Policy.md §5](../01-Policy-and-Standards/Org-Test-Policy.md) is violated, the team's overall grade is capped at **Grade C** and flagged as a risk escalation to leadership — no averaging masks a non-negotiable breach.
- If **Coverage (D)** for Security or the applicable non-functional rows scores 0–1 on a Tier 1/2 team, overall grade is capped at **Grade C**.
- If **Automation & Tooling (G/H/I)** scores 0–1 while Process scores 3–4, flag as "process-mature, automation-immature" in the report — a real and common pattern that a blended average would hide.

## 5. Mapping composite score to maturity level

| Composite score range | Level |
|---|---|
| 0.0 – 0.8 | L1 — Ad Hoc / Reactive |
| 0.9 – 1.7 | L2 — Emerging / Repeatable |
| 1.8 – 2.5 | L3 — Defined / Standardized |
| 2.6 – 3.3 | L4 — Managed / Measured |
| 3.4 – 4.0 | L5 — Optimizing / Leading-edge |

See [Maturity-Model-Framework.md](../03-Maturity-Model/Maturity-Model-Framework.md) for full level definitions and grade bands (A–D) used in leadership reporting.

## 6. Anti-gaming measures

- Assessors rotate across teams each cycle so no single assessor's leniency/strictness skews a team's trend.
- Score changes between cycles must cite what specifically changed (evidence delta), not a general "we've improved."
- A dip in score is never treated as a penalty against the team lead — it is treated as a resourcing/prioritisation signal for the improvement plan. This is stated explicitly to prevent defensive/inflated self-reporting.
- Spot-check evidence links quarterly on a sample of teams to confirm links are live and current, not stale artefacts reused across cycles.
