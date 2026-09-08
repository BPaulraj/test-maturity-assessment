# Testing Types & Levels — Org Standard

Purpose: define, for every testing type/level in scope, the minimum expectation, ownership, and required tooling *category* (not a mandated vendor — see [Org-Test-Policy.md §3.6](Org-Test-Policy.md)). "Required for Tier" references the risk tiers in the policy.

## Test Pyramid Levels

| Level | Owner | Minimum Expectation | Required for Tier | Tooling Category |
|---|---|---|---|---|
| **Unit** | Developers | ≥ 70% meaningful line/branch coverage on new/changed code (not vanity coverage on generated/boilerplate code); runs on every commit | 1–3 mandatory, 4 recommended | Language-native test runner (xUnit family) |
| **Component / Integration** | Developers + SDET | Every service tested in isolation with dependencies mocked/stubbed or via contract tests; runs in CI on every PR | 1–2 mandatory, 3 recommended | Language-native + contract testing tool (e.g., consumer-driven contracts) |
| **API** | SDET | All public/internal API contracts covered for happy path, auth failure, validation failure, and rate-limit/error handling | 1–2 mandatory, 3 recommended | API test/automation framework |
| **System / End-to-End** | SDET + Testers | Critical user journeys only (not exhaustive UI coverage) — E2E is the most expensive layer and must stay thin | 1–2 mandatory, 3 optional | UI/E2E automation framework |
| **Regression** | SDET | Full regression suite automated and run at minimum nightly, and on every release candidate | 1–3 mandatory | CI-integrated automation suite |

## Non-Functional & Specialised Testing

| Type | Minimum Expectation | Required for Tier | Notes |
|---|---|---|---|
| **Performance / Load** | Baseline load test before major release; SLO thresholds defined and enforced as a build gate for Tier 1 | 1 mandatory, 2 recommended | Include soak/endurance test at least annually for Tier 1 |
| **Security (SAST/DAST/dependency scanning)** | Automated SAST + dependency/SCA scan on every build; DAST/pen-test at least annually or per major release for Tier 1 | 1–2 mandatory (non-negotiable), 3 recommended | Never skipped for customer-facing Tier 1/2 — see policy §5 |
| **Accessibility (a11y)** | WCAG 2.1 AA automated scan in CI + manual screen-reader spot check before release | 1–2 mandatory for customer-facing UI | Non-negotiable for public-facing Tier 1/2 |
| **Usability / UAT** | Structured UAT with real or proxy users before major feature launch | 1–2 mandatory, 3 recommended | Can be lightweight (5-user hallway test) for Tier 3 |
| **Exploratory Testing** | Time-boxed, chartered exploratory sessions (session-based test management) logged with findings, every sprint | All tiers recommended, 1–2 mandatory | Complements, never replaces, scripted coverage |
| **Contract Testing** | Consumer-driven contracts for all internal service-to-service dependencies | 1–2 mandatory where microservices used | Prevents integration breakage without full E2E |
| **Chaos / Resilience** | Fault-injection game days at least twice yearly for Tier 1 services | 1 mandatory, 2 recommended | Validates rollback/kill-switch non-negotiable |
| **Data / ETL / Pipeline Testing** | Schema validation, row-count reconciliation, and data-quality rule checks automated per pipeline run | 1–2 mandatory for data platforms | Include PII masking validation |
| **Mobile-specific (device/OS matrix)** | Coverage across a defined device/OS support matrix, prioritised by install-base analytics | 1–2 mandatory for mobile apps | Cloud device farm category |
| **Compatibility (browser/OS)** | Coverage of the org's officially supported browser/OS matrix, published and reviewed yearly | 1–2 mandatory | |
| **Localization / Internationalization** | Pseudo-localization automated check + linguistic review for shipped locales | 1–2 mandatory where multi-locale | |
| **Visual Regression** | Automated visual diffing on key screens for design-system-driven UIs | 2–3 recommended | Reduces manual UI regression burden |

## Test Environment & Data Standard (cross-cutting)

- Environments are provisioned via IaC/self-service, not manual ticket-based provisioning, for Tier 1–2 by maturity Level 3+.
- Test data is synthetic or masked; no raw production PII in non-prod environments (non-negotiable, see policy §5).
- Environment parity with production (config, versions) is tracked and drift is alerted, for Tier 1.

## When Each Type Runs (STLC / Sprint Placement)

The table above defines *what's* required; it deliberately doesn't say *when* in the sprint/release cycle each type executes — several of these (DAST, full performance tests, manual accessibility, chaos) need a live deployed build, an assembled feature, or a dedicated environment, and don't fit the default per-story cadence. See [08-Agile-Scrum-Practices/NFR-and-Specialized-Testing-Placement-in-STLC.md](../08-Agile-Scrum-Practices/NFR-and-Specialized-Testing-Placement-in-STLC.md) for the full placement table (story vs. feature vs. release level, in-sprint vs. dedicated cycle).

## How this maps to assessment

Each row above becomes a scored item in the [Questionnaire](../02-Assessment-Questionnaire/Questionnaire.md) section D ("Levels/Types of Testing Coverage"). A team is only assessed against the rows applicable to its risk tier and architecture (e.g., mobile-specific rows are N/A for a backend-only service, and are excluded from the denominator — not scored as zero).
