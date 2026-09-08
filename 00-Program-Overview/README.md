# Test Maturity & Quality Excellence Program

This directory is the complete operating framework for assessing, grading, and improving test maturity across all engineering teams in the organisation. It is designed to be run as a repeatable, evidence-based assessment cycle — not a one-time audit.

## What's in here

| Folder | Purpose |
|---|---|
| [01-Policy-and-Standards](../01-Policy-and-Standards/) | The org-level "what good looks like" — non-negotiables, per-testing-type standards, entry/exit criteria, KPI standard. This is the target state every team is graded against. |
| [02-Assessment-Questionnaire](../02-Assessment-Questionnaire/) | The instrument used to capture AS-IS state from any team: the questionnaire itself, scoring/weighting guide, and the evidence checklist assessors use to avoid self-reported scores. |
| [03-Maturity-Model](../03-Maturity-Model/) | Turns questionnaire scores into a 5-level maturity grade (L1–L5) per dimension and overall, with gating rules and grade bands (A–D) for leadership reporting. |
| [04-Automation-Maturity](../04-Automation-Maturity/) | A deep-dive on test automation specifically — capability *and* capacity — plus the advancement roadmap from manual to AI-augmented continuous testing. |
| [05-AI-in-Testing](../05-AI-in-Testing/) | AI adoption questionnaire, maturity levels, and the governance guardrails needed before AI is trusted with test artefacts. |
| [06-Improvement-Planning](../06-Improvement-Planning/) | Templates to convert a team's gap analysis into a funded, owned improvement plan, plus the org-wide roadmap and RACI operating model. |
| [07-Leadership-Summary](../07-Leadership-Summary/) | The one output leadership actually reads: narrative executive summary plus a visual dashboard artefact. |
| [08-Agile-Scrum-Practices](../08-Agile-Scrum-Practices/) | How testing plugs into the actual Scrum rhythm — shift-left across every ceremony, the story/feature/release "three levels of done," and demo/showcase cadence. |

## Mode & Format — Running This For Real

Everything below is the framework; [Assessment-Operating-Procedure.md](Assessment-Operating-Procedure.md) is the concrete mechanics — what file format teams fill in, why scoring happens in a separate tool, and how results consolidate. The live scoring/consolidation tool is the [Maturity Scoring Console](https://claude.ai/code/artifact/07e9a0d7-d96d-4f5b-8eab-b806bf82f67c).

## How to run an assessment cycle end to end

1. **Calibrate** — Read [01-Policy-and-Standards](../01-Policy-and-Standards/Org-Test-Policy.md) so assessors and teams share the same definition of "good."
2. **Collect** — Run the [Questionnaire](../02-Assessment-Questionnaire/Questionnaire.md) with each team lead/SDET lead. Do not accept scores without the evidence listed in [Evidence-Checklist.md](../02-Assessment-Questionnaire/Evidence-Checklist.md).
3. **Score** — Apply [Scoring-and-Weighting-Guide.md](../02-Assessment-Questionnaire/Scoring-and-Weighting-Guide.md) to get dimension scores.
4. **Grade** — Map scores to levels/grades using [Maturity-Model-Framework.md](../03-Maturity-Model/Maturity-Model-Framework.md) and the detailed [Dimension-Rubrics.md](../03-Maturity-Model/Dimension-Rubrics.md).
5. **Deep-dive automation & AI** — Every team additionally runs [04-Automation-Maturity](../04-Automation-Maturity/) and [05-AI-in-Testing](../05-AI-in-Testing/) since these move faster than the base model and warrant their own cadence.
6. **Plan** — Each team fills a [Team-Improvement-Plan-Template.md](../06-Improvement-Planning/Team-Improvement-Plan-Template.md); the COE rolls these into the [Org-Wide-Roadmap-Template.md](../06-Improvement-Planning/Org-Wide-Roadmap-Template.md).
7. **Report** — Findings and the roadmap are packaged into [07-Leadership-Summary](../07-Leadership-Summary/).
8. **Repeat** — Re-assess quarterly (see cadence in the RACI/operating model doc). Maturity is a trend line, not a point-in-time score.

## Design principles behind this framework

- **Evidence over self-report.** Every questionnaire score must be backed by an artefact (dashboard, repo, pipeline config), not an opinion.
- **Weakest-link gating.** A team cannot claim a high overall grade while a critical dimension (release quality, security testing, environment stability) is weak — see gating rules in the maturity model.
- **Risk-based, not one-size-fits-all.** Standards scale with the risk tier of the product/service being tested, not a flat checklist.
- **Automation and AI are tracked separately from "process" maturity** because a team can be process-mature and automation-immature, or vice versa — collapsing them into one score hides the real gap.
- **The output is a plan, not a scoreboard.** Grading exists to produce funded, owned improvement plans — never to rank teams competitively in a way that discourages honest self-reporting.
