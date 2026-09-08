# Test Data Management Standard

Purpose: [Org-Test-Policy §5](Org-Test-Policy.md#5-non-negotiables) makes "no raw production PII in non-prod" non-negotiable. This document defines *how* teams get realistic, sufficient test data without breaking that rule, and on what cadence — because "just don't use prod data" without a real alternative is how the non-negotiable quietly gets ignored under deadline pressure.

## 1. Two Supply Models, Used Together

| Model | Best for | Limitation |
|---|---|---|
| **Synthetic generation** — algorithmically/tool-generated data matching schema and business rules, no real customer data involved | Negative/boundary/edge-case testing; high-volume performance testing needing known, reproducible data shapes | Can miss the "messy real-world" edge cases a synthetic generator's rules didn't anticipate |
| **Sanitized production copy** — a periodic extract of real production data passed through an automated masking/anonymisation pipeline before landing in non-prod | Realistic exploratory testing; catching real-world data shapes synthetic generation misses | Requires a robust, validated masking pipeline; heavier to refresh |

Neither model alone is sufficient — synthetic data is used as the default for scripted/automated testing (reproducibility matters more there), and masked production copies are used for exploratory/UAT-style testing where realism matters more than reproducibility.

## 2. Masking Pipeline Requirements (for the sanitized-copy model)

- PII fields (name, email, phone, national ID, payment data, address, etc.) are tokenized or irreversibly scrambled — not merely truncated or partially redacted.
- Referential integrity is preserved across tables/services after masking (a masked customer ID must still join correctly across the schema).
- The masking pipeline itself is automated and version-controlled, not a manual one-off script run by whoever remembers to.
- **Masking validation is itself a test**: after every refresh, an automated PII-pattern scan (email/SSN/card-number regex and equivalent) runs against the refreshed dataset and must pass before the environment is marked usable. This scan result is the evidence an assessor checks per the [Evidence-Checklist.md](../02-Assessment-Questionnaire/Evidence-Checklist.md).

## 3. Refresh Cadence (per environment)

| Environment | Data source | Refresh cadence |
|---|---|---|
| Dev / per-developer | Synthetic seed set | On-demand, self-service |
| SIT / QA (shared) | Synthetic seed set, occasionally topped up from masked prod | Weekly, or on-demand reset to baseline |
| Staging / UAT | Masked production copy | Monthly, or per-release for Tier 1 |
| Performance | Synthetic, production-representative volume (see [Test-Environment-Strategy.md](Test-Environment-Strategy.md)) | Before every performance test cycle |

Cadence is a floor, not a ceiling — a team may refresh more often; going less often requires an exception per [Org-Test-Policy §7](Org-Test-Policy.md#7-exceptions-process).

## 4. Self-Service & Speed

- Testers can reset/seed their environment's data to a known baseline state without filing a ticket and waiting — a shared dataset that only one person knows how to reset is a Level 1–2 anti-pattern.
- "Time to usable test data" is tracked as part of Environment Provisioning Lead Time in [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md) — data readiness is part of that metric, not a separate invisible wait.

## 5. Volume & Subsetting Strategy

- Functional/exploratory environments use a right-sized subset — enough variety to exercise edge cases, not a full production-scale copy that's slow to refresh and overkill for the purpose.
- Performance environments use production-representative **volume and distribution** (row counts, data skew, not just row count) so load test results are meaningful — see the sizing/extrapolation approach in [Test-Environment-Strategy.md](Test-Environment-Strategy.md).

## 6. Ownership

- The platform/data engineering function owns the masking and refresh pipeline as a shared service.
- QE defines the masking validation test and the data requirements per environment.
- Any suspected raw PII exposure found in non-prod is treated as a security incident per [AI-in-Testing-Maturity-Model-and-Governance.md §3.5](../05-AI-in-Testing/AI-in-Testing-Maturity-Model-and-Governance.md)'s equivalent escalation path — not quietly patched and forgotten.
