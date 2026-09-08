# Test Artefact & Tooling Standard

Purpose: [Org-Test-Policy.md §3.6](Org-Test-Policy.md) says tooling is standardised at the category level, not the vendor level. This document defines what a test management tool must support, and — more importantly — what artefact lives where, so a team's tool choice never fragments org-wide reporting or leaves artefacts scattered across spreadsheets and chat threads.

## 1. Required Capabilities of a Test Management Tool (category, not vendor)

Whatever product a team chooses within the approved category, it must support:

1. Linkage to the Agile work-tracking tool (story/AC ↔ test case), bidirectional where possible.
2. A test case repository with a folder/module hierarchy (see [Test-Case-Management-and-Risk-Based-Design.md](Test-Case-Management-and-Risk-Based-Design.md)).
3. Test cycle / test run tracking (an execution instance separate from the test case definition itself).
4. Defect linkage — from a failed test run to a logged defect, and back.
5. Traceability reporting (requirement/AC → test case → run → defect) generated from the tool, not hand-built.
6. An audit trail / version history on test cases.
7. API or native integration to ingest automated test results from CI, so automated and manual results live in one place.

A tool lacking any of these is not an approved category member regardless of popularity — raise an exception request per [Org-Test-Policy §7](Org-Test-Policy.md#7-exceptions-process) if a team believes their case is different.

## 2. Artefact Taxonomy — What Lives Where

| Artefact | Definition | Source of truth | Notes |
|---|---|---|---|
| **Test Strategy / Test Plan** | Per product/service, per [Org-Test-Policy](Org-Test-Policy.md) | Test mgmt tool or linked wiki page, referenced from the tool | Reviewed at least yearly |
| **Test Suite / Module folder** | Organisational grouping of test cases | Test mgmt tool | Structured per [Test-Case-Management-and-Risk-Based-Design.md](Test-Case-Management-and-Risk-Based-Design.md) |
| **Test Case** | Atomic, versioned, tagged test definition | Test mgmt tool | Never duplicated into a spreadsheet "for convenience" |
| **Test Cycle / Test Run** | One execution instance of a suite, tied to a sprint or release | Test mgmt tool | Automated run results ingested via CI integration, not pasted in manually |
| **Traceability Matrix** | User Story/AC ↔ test case ↔ defect, navigable **in both directions** | Generated report from the tool | Forward (story → test case → defect) supports coverage/impact analysis; reverse (defect → test case → story) supports root-cause and "what did we miss" analysis. A manually maintained traceability spreadsheet, or one that only works forward, is a Level 1–2 anti-pattern per [Dimension-Rubrics.md](../03-Maturity-Model/Dimension-Rubrics.md) |
| **Defect** | Logged issue with severity/priority/status | Defect tracker (may be the same tool or an integrated one) | See [Defect-Management-Standard.md](Defect-Management-Standard.md) |
| **Automation Script** | The actual executable test code | Automation framework's version control repo | The test mgmt tool holds a *pointer* + last-run result, never a duplicate copy of the script itself |

## 3. Maintenance Rules

- **One source of truth per artefact type.** If a defect also appears in a personal spreadsheet or a Slack thread as the "real" tracker, that is a non-compliant shadow system, regardless of intent.
- **Ownership is explicit.** Every module/suite has a named owner responsible for its health (see risk-based ownership in [Test-Case-Management-and-Risk-Based-Design.md](Test-Case-Management-and-Risk-Based-Design.md)).
- **Retention, not deletion.** When a feature is deprecated, its test cases are archived (excluded from active runs, kept for traceability history), not deleted — this preserves the audit trail for any future compliance or incident investigation.
- **Access control** distinguishes edit (test designer/SDET), execute (any tester), and view (broader stakeholders including Product) rights.
- **Quarterly artefact audit** — the Test COE spot-checks a sample of teams for orphaned test cases (no longer linked to a live requirement), stale cases (not reviewed in 2+ quarters), and shadow-tracker evidence, feeding findings into that team's next [Improvement Plan](../06-Improvement-Planning/Team-Improvement-Plan-Template.md).

## 4. Tool Change / Migration Process

A team wanting to move to a different tool within the approved category notifies the Test COE, who confirms the new tool meets §1, and coordinates a migration window that preserves traceability history (export/import of test cases and historical run data, not a clean-slate restart).
