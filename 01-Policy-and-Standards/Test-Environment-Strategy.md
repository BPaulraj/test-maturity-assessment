# Test Environment Strategy

Purpose: environment instability is one of the most common, most underrated causes of lost test time and unreliable automation results. This standard defines the environment topology, and gives a concrete answer to "how close is performance testing to production" instead of leaving it as an aspiration.

## 1. Standard Environment Topology

```
Dev (per-developer / ephemeral)
   → SIT / QA (shared, integration testing)
      → Staging / UAT (production-like, business sign-off)
         → Performance (dedicated — see §2)
            → [Tier 1 only] Pre-Prod / Canary
               → Production
```

Tier 3–4 systems may collapse SIT and Staging into one environment; Tier 1 systems must keep them separate so a performance run or a UAT sign-off is never blocked by unrelated integration-testing churn.

## 2. Dedicated Performance Environment — Requirements

A performance environment that is just "a copy of QA, but bigger" produces numbers nobody can trust. It must be:

1. **Physically/logically isolated** from functional SIT/UAT, so a load test never destabilises other testers' work and other testers' activity never skews load-test results.
2. **Prod-parity, explicitly documented**, covering:
   - Same application topology (number of tiers, service boundaries).
   - Same **load balancer configuration and routing behaviour** as production — this is the single most common place perf environments silently diverge from prod.
   - Same or a **documented, versioned scaling-extrapolation factor** when full parity isn't cost-justified — e.g., "Perf env runs at 25% of production node count; results are extrapolated using a validated capacity model, re-validated against actual production behaviour quarterly." A scaling factor that has never been validated against real production numbers is not a scaling factor, it's a guess.
   - Same network/CDN/caching-layer configuration where feasible, or an explicitly documented deviation.
   - Production-representative data **volume and distribution**, per [Test-Data-Management-Standard.md §5](Test-Data-Management-Standard.md).
3. **Config-drift checked before every cycle** — an automated diff against the production infrastructure-as-code baseline, run before each performance test cycle, not assumed to still match from last time.

## 3. Environment Stability Practices

- **Uptime/availability is tracked** per [Metrics-and-KPI-Standard.md](Metrics-and-KPI-Standard.md) ("Environment Availability/Uptime").
- **Recurring instability triggers an RCA, not just another ticket.** A threshold (e.g., more than a defined number of stability incidents per month on the same environment) automatically escalates to a root-cause investigation rather than being absorbed as "normal."
- **Shared-environment booking/scheduling** exists for any non-ephemeral shared environment (SIT, Performance) to prevent test collisions — two teams running conflicting load tests or data resets against the same environment at once is a process failure, not bad luck.
- **Self-service provisioning** is the target for Tier 1–2 environments once a team reaches maturity Level 3+ (per [Testing-Types-Standards.md](Testing-Types-Standards.md)) — manual, ticket-based provisioning is treated as a maturity gap, not a neutral default.

## 4. Ownership

| Responsibility | Owner |
|---|---|
| Environment provisioning tooling / IaC | Platform / Infra Engineering |
| Environment usage scheduling | QE / Team SDET Lead |
| Prod-parity checklist accuracy & scaling-factor validation | Platform Engineering + QE jointly, reviewed quarterly |
| Stability RCA when triggered | Platform Engineering, with QE input on impact |

## 5. Assessment Hook

Scored under Questionnaire section F (Test Environment & Data Management) and cross-checked at the automation deep-dive level, since flaky automation and unstable environments are frequently the same underlying problem wearing different symptoms — see [Automation-Capability-Assessment.md](../04-Automation-Maturity/Automation-Capability-Assessment.md).
