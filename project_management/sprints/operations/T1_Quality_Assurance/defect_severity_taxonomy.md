
# Defect Severity Taxonomy — Vynues
**Standard:** ISO 9001:2015 Clause 8.7 | VMS QA | Lean Six Sigma
**Owner:** COO
**Review Cadence:** Quarterly

---

## 1. Purpose

This taxonomy classifies all defects discovered across Vynues 
product and service delivery into four severity levels (S1–S4), 
with defined response times, owners, and resolution paths.

Aligned to VMS principle:
> "Identify and correct quality defects as early as possible 
>  in the process."

---

## 2. Defect Classification Matrix

### S1 — Critical (System Down / Client Impact)

| Field | Definition |
|---|---|
| **Impact** | Complete system failure OR client-facing data loss OR security breach OR contractual breach |
| **Examples** | Platform down; booking data corrupted; payment failure; PII exposed; S1 SLA breach |
| **Detection Target** | < 1 hour from occurrence |
| **Response SLA** | Immediate — COO notified within 15 minutes |
| **Resolution SLA** | < 4 hours |
| **Owner** | COO + Lead Engineer |
| **Gate** | Hard gate — zero S1s released to production |
| **Process** | Detect → Escalate to COO → War room → Fix → Re-test → Post-mortem within 24 hrs |

---

### S2 — High (Major Function Broken / Degraded)

| Field | Definition |
|---|---|
| **Impact** | Core feature broken with no workaround OR significant client experience degradation |
| **Examples** | Venue search
