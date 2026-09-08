# Assessment Operating Procedure — Mode & Format

Purpose: the framework in folders 01–08 defines *what* good testing looks like and *how* it's scored. This document defines the mechanics: what file format teams actually use, why the scoring step must happen in a different file, how results consolidate centrally, and how both per-team and org-level reports get regenerated each cycle.

## Step 1 — Team Intake

**Format:** [Team-Response-Template.csv](../02-Assessment-Questionnaire/Team-Response-Template.csv) — one blank copy per team per cycle, saved as `{TeamName}_{Cycle}_Response.csv` (e.g., `PaymentsTeam_2026-Q1_Response.csv`).

**Mode:** filled out **collaboratively**, in a live session between the assessor and the Team QE/SDET Lead — not emailed out for the team to complete alone. A score produced without a conversation about evidence drifts toward self-flattery; the live session is where the assessor applies the evidence-gated scoring and self-score/assessor reconciliation described in [Scoring-and-Weighting-Guide.md §1](../02-Assessment-Questionnaire/Scoring-and-Weighting-Guide.md).

**What gets edited:** only the **Score** and **Evidence Link / Note** columns. `ID`, `Dimension`, `Section`, and `Question` are fixed and never edited — this keeps every team's file structurally identical and machine-parseable regardless of who fills it in.

**Once the session ends, this file is immutable.** It's the raw-intake record — archived as-is in the team's assessment folder. If a re-score is ever needed, it happens in a new, dated copy; history is never edited in place.

## Step 2 — Scoring: a Different File, on Purpose

Your instinct to keep this separate from the intake file is correct, for three reasons:

1. **It protects the raw record.** A formula error or accidental overwrite in a scoring workbook should never be able to corrupt what the team actually reported.
2. **The scoring logic evolves faster than the intake record should.** This questionnaire has already changed three times in one round of feedback — a scoring mechanism that lives inside every team's individual file would need re-wiring 20+ times over. A separate, single scoring mechanism only needs updating once.
3. **It preserves the audit trail.** "What the team reported" and "how it was interpreted into a grade" are different questions with different owners (Team Lead vs. Test COE) — collapsing them into one file blurs that accountability.

Two ways to implement the scoring step — pick based on your org's constraints:

| | Option A — Excel/Google Sheets | Option B — Maturity Scoring Console (recommended) |
|---|---|---|
| What it is | A master **Scoring Workbook** with a Calc tab that pulls values from each team's CSV (paste values only — never a live formula link into the raw file) | A live tool (built alongside this framework) that parses a pasted/uploaded CSV and computes the same logic automatically |
| Section/dimension math | `AVERAGEIF` per section (excluding NA), dimension = simple mean of that dimension's section averages (per [Scoring-and-Weighting-Guide.md §3](../02-Assessment-Questionnaire/Scoring-and-Weighting-Guide.md)), weighted sum for composite, `VLOOKUP`/lookup table for the level band | Same formulas, implemented in code instead of spreadsheet formulas |
| Gating checks | Manual checkboxes for "non-negotiable violated?" and "Tier 1/2 critical-coverage 0–1?" (these need assessor judgement, not just arithmetic); the "one dimension L1 while others L4+" gate can be a formula | Same manual checkboxes for judgement calls; the arithmetic-detectable gate is automatic |
| Consolidation | A "Consolidated" tab, one row appended per team per cycle | Built-in — every scored team is saved centrally automatically |
| Best for | Orgs that require everything auditable as a spreadsheet artefact for compliance reasons | Avoiding re-wiring formulas every time the questionnaire changes, and avoiding a manual "copy each team's result into one sheet" step |

**Option B is built and live:** [Maturity Scoring Console](https://claude.ai/code/artifact/07e9a0d7-d96d-4f5b-8eab-b806bf82f67c) — paste a team's completed `Team-Response-Template.csv`, it computes the section/dimension/composite/gating logic automatically, and (with your name and cycle entered) saves the result to a shared store every assessor's view of the same tool can see. It also renders the Team Report and Org Roll-up views described in Steps 3–4 below directly from that shared store — nothing needs to be manually copied into a separate report each cycle.

Whichever option is used, it produces the same output per team per cycle — see Step 3.

## Step 3 — Consolidation

The output of scoring, regardless of which option, is **one row per team per cycle** in a central store, containing: Team, Cycle, Risk Tier, the 5 dimension scores and levels, composite score, gated overall grade, gating reason (if capped), and profile-shape tag (per [Maturity-Model-Framework.md §5](../03-Maturity-Model/Maturity-Model-Framework.md)).

This central store — the Consolidated tab in Option A, or the built-in database in Option B — is what **both** the per-team and org-level reports are generated *from*. Nobody re-derives numbers by hand when writing a report; the report is a view over this store, which is also what keeps re-reporting cheap every quarter instead of a fresh manual exercise each time.

## Step 4 — Regenerating Reports

- **Per-team report:** rendered from that team's consolidated row, plus its history across prior cycles for trend — using the same dimension-ladder and grade-card visual language as the org-level report, so every output in the program looks like it comes from one coherent system rather than a different ad hoc format each quarter.
- **Org-level report:** aggregates every team's consolidated row for the selected cycle into a grade distribution, a profile-shape distribution, and a list of any org-wide gating flags. **This is what replaces the "illustrative example" placeholder** in the published [Leadership Briefing](../07-Leadership-Summary/leadership-dashboard.html) once Cycle 1 actually completes — the illustrative bars get swapped for the real aggregated numbers, not rebuilt from scratch.

## Cadence

This four-step loop runs once per quarter, per the cadence defined in [RACI-and-Operating-Model.md](../06-Improvement-Planning/RACI-and-Operating-Model.md).
