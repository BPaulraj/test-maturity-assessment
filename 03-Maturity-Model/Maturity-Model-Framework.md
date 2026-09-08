# Test Maturity Model — Framework

This model converts questionnaire scores into a level (L1–L5) per dimension and an overall grade (A–D) suitable for leadership reporting. It draws on the structure of established models (TMMi, CMMI-style staged levels) but is customised to score **Process, Coverage, Automation & Tooling, AI Adoption, and Competency/Governance/Culture** as distinct dimensions rather than one blended number, because teams frequently advance unevenly across these.

## 1. The Five Levels (holistic definition)

| Level | Name | Characterised by |
|---|---|---|
| **L1** | Ad Hoc / Reactive | Testing happens, but is undocumented, person-dependent, and reactive to whatever broke last. No reliable metrics. Automation, if present, is fragile scripts nobody trusts. |
| **L2** | Emerging / Repeatable | Basic process exists and is followed inconsistently. Some documentation, some automation, but heavily manual and not measured. Heroics still save releases. |
| **L3** | Defined / Standardized | Process, tooling, and automation are standardised and followed consistently across the team. Dashboards exist. Entry/exit criteria are enforced. This is the **minimum acceptable steady state** for Tier 1/2 teams. |
| **L4** | Managed / Measured | Everything in L3, plus metrics actively drive decisions (release go/no-go, where to invest in automation). Automation gates CI/CD. AI is used in a governed way for specific tasks. Continuous improvement is a running cadence, not a one-off. |
| **L5** | Optimizing / Leading-edge | The team is a source of org-wide best practice. Predictive/AI-driven testing, self-healing automation, continuous testing in production (safely), and metrics are used to *prevent* problems, not just detect them. Actively benchmarked against industry practice. |

## 2. Dimension → Level mapping

Each dimension gets its own level using the section-to-dimension weighting in [Scoring-and-Weighting-Guide.md](../02-Assessment-Questionnaire/Scoring-and-Weighting-Guide.md) §5's score-to-level table, applied to that dimension's average instead of the composite. This produces a **maturity profile**, e.g.:

```
Process:                L3
Coverage:                L2
Automation & Tooling:    L2
AI Adoption:             L1
Competency/Gov/Culture:  L3
Overall (weighted, gated): L2
```

This profile is what actually drives the improvement plan — the overall grade is for leadership roll-up, the profile is for the team.

## 3. Overall Grade Bands (for leadership reporting)

| Grade | Maps to composite level | Leadership interpretation | Typical posture |
|---|---|---|---|
| **Grade A** | L4–L5 | Low risk. Model team. Candidate to host org best-practice/enablement | Fund their innovation; use as internal reference/mentor for other teams |
| **Grade B** | L3 | Acceptable steady state, meets the policy floor | Fund targeted advancement (automation scale, AI adoption) |
| **Grade C** | L2, or gated down from higher by a critical gap (see §4) | Below policy floor; carries real release/quality risk | Requires a funded improvement plan with executive visibility |
| **Grade D** | L1 | High risk; foundational gaps | Immediate intervention — COE-embedded support, not just a plan on paper |

## 4. Gating Rules (weakest-link — repeated from scoring guide for visibility)

An overall grade is **capped at Grade C** regardless of composite score when:
- Any [non-negotiable](../01-Policy-and-Standards/Org-Test-Policy.md#5-non-negotiables) is violated, **or**
- Security/critical non-functional coverage scores 0–1 on a Tier 1/2 team, **or**
- A single dimension scores L1 while others score L4+ (prevents one glaring gap from being statistically buried).

This is deliberate: leadership must never see a comfortable "Grade B" that is hiding a security-testing gap or PII exposure in test data.

## 5. Grouping teams for org-wide reporting

Teams are grouped into their grade band for the [Leadership Summary](../07-Leadership-Summary/). Within a band, teams are further tagged by their **profile shape**, since two Grade C teams can have opposite problems:

- **"Process gap"** — weak Process/Coverage, but decent Automation — usually a discipline/documentation fix.
- **"Automation gap"** — strong Process, weak Automation & Tooling — usually a capacity/investment fix (see [04-Automation-Maturity](../04-Automation-Maturity/)).
- **"AI-lagging"** — otherwise strong, low AI Adoption — usually an enablement/training fix (see [05-AI-in-Testing](../05-AI-in-Testing/)).
- **"Foundational"** — broadly weak across all dimensions — needs COE-embedded support, not a self-service improvement plan.

## 6. Detailed rubrics

See [Dimension-Rubrics.md](Dimension-Rubrics.md) for the level-by-level descriptive criteria per dimension, used by assessors to justify a level assignment beyond the numeric score.

## 7. Org-Level Aggregation

A grade *distribution* (how many teams are A/B/C/D) tells leadership how the portfolio is spread out. It does not answer "what is the org's maturity, as one number" — that requires a genuine org-level aggregation, computed as follows:

1. **Org-level dimension score** = the average of that dimension's score across every team assessed in the cycle, **equal-weighted per team** (a large Tier 1 team and a small Tier 4 team count the same by default — see the weighting note below). This produces an org-level dimension profile (Process, Coverage, Automation & Tooling, AI Adoption, Competency/Governance/Culture), exactly analogous to a team's profile.
2. **Org-level composite** = the same weighted formula as team level (Process 35%, Coverage 20%, Automation & Tooling 25%, AI 10%, Competency 10%) applied to the org-level dimension averages.
3. **Org-level Level and Grade** = the same L1–L5 bands and A–D grade mapping used at team level, applied to the org-level composite.

**Gating does not disappear at org scale — it changes form.** The org-level grade is **not** automatically capped by one team's gate (an org-wide average legitimately represents a portfolio, not one system). But a cycle report is **incomplete** — not merely conservative — if it shows a clean org-level grade without also listing, by name, every team gated that cycle and why. The org number and the gated-teams list are reported **together**, always, so leadership never sees "Org: Grade B" while a Tier 1 team sits on an unresolved non-negotiable breach one click away from view.

**Weighting is a declared choice, not a default to silently change.** Equal-weighting per team is the default because it's the most auditable by hand. An org may choose to weight by risk tier (a Tier 1 team's score counts more toward the org number) or by team size — but whichever is used must be stated explicitly next to any org-level number reported to leadership, since it changes what "org maturity" actually means.
