
# Vynues Defect-Severity Taxonomy

**Document ID:** VYN-OPS-QA-003 | **Version:** 1.0
**Owner:** Operations Sprint Team

---

## Severity Levels

### 🔴 SEV-1 — Critical
> Complete failure of a core function, material financial or legal harm, security breach, or an event that cannot proceed as contracted. No acceptable workaround exists.

**Examples:**
- Platform fully down or booking engine non-functional
- Customer event cannot proceed due to Vynues-attributable failure
- Data breach or unauthorized access to customer or payment data
- Vendor delivers fundamentally incorrect service with no on-site remediation
- Signed contract contains materially incorrect terms creating legal exposure

| Attribute | Requirement |
|---|---|
| Acknowledgment | ≤ 15 minutes |
| Customer notification | ≤ 30 minutes |
| Target remediation | ≤ 4 hours |
| Ownership | COO + domain lead |
| Post-incident review | Within 48 hours — RCA mandatory |
| Escalation | COO, Legal (if applicable), CEO |

---

### 🟠 SEV-2 — High
> Significant degradation of a core function, material SLA breach risk, or substantial impairment of service delivery. A workaround exists but is burdensome or temporary.

**Examples:**
- Booking flow producing errors for a significant percentage of users
- Vendor deliverable substantially incomplete but event can partially proceed
- Response-time SLAs missed across a customer segment
- Vendor insurance lapsed before event execution

| Attribute | Requirement |
|---|---|
| Acknowledgment | ≤ 1 hour |
| Customer notification | ≤ 2 hours (if customer-impacting) |
| Target remediation | ≤ 24 hours |
| Ownership | Domain lead |
| Post-incident review | Within 5 business days — RCA recommended |
| Escalation | COO notified within 2 hours |

---

### 🟡 SEV-3 — Medium
> Impairment of a non-critical function or minor customer inconvenience. Does not materially affect event outcome or platform usability. A reasonable workaround exists.

**Examples:**
- Secondary platform feature broken (e.g., saved preferences)
- Minor vendor quality shortfall that does not compromise the event
- Booking confirmation contains a minor factual inaccuracy
- Single isolated SLA miss with no pattern

| Attribute | Requirement |
|---|---|
| Acknowledgment | ≤ 4 business hours |
| Customer notification | Within 1 business day if customer-facing |
| Target remediation | ≤ 5 business days |
| Ownership | Assigned domain team member |
| Post-incident review | Next weekly QA sprint cycle |
| Escalation | Domain lead notified; COO dashboard visibility only |

---

### 🔵 SEV-4 — Low
> Cosmetic issue, minor process inefficiency, or quality observation with negligible impact on customer experience or business outcomes.

**Examples:**
- UI cosmetic issues (alignment, font, color)
- Non-customer-facing process step that is slightly inefficient
- Vendor documentation complete but on outdated template
- Post-event enhancement suggestions

| Attribute | Requirement |
|---|---|
| Acknowledgment | ≤ 2 business days |
| Customer notification | Not required unless customer-initiated |
| Target remediation | Next sprint / quarterly backlog cycle |
| Ownership | Assigned team member (backlog) |
| Post-incident review | Monthly QA aggregate review |
| Escalation | None — dashboard reporting only |

---

## Quick-Reference Matrix

| Severity | Impact | Workaround | Acknowledge | Remediate | RCA |
|---|---|---|---|---|---|
| 🔴 SEV-1 Critical | Complete failure / legal / financial | None | 15 min | 4 hours | Mandatory |
| 🟠 SEV-2 High | Major degradation / material risk | Burdensome | 1 hour | 24 hours | Recommended |
| 🟡 SEV-3 Medium | Minor impairment / isolated deviation | Reasonable | 4 bus. hours | 5 bus. days | Optional |
| 🔵 SEV-4 Low | Cosmetic / negligible | Easy | 2 bus. days | Sprint backlog | Not required |

---

## Classification Decision Tree

```
Is there complete failure, an event that cannot proceed,
a data breach, or immediate legal/financial harm?
└─ YES → 🔴 SEV-1

Is there major degradation of a core function,
material SLA breach risk, or substantial service impairment?
└─ YES → 🟠 SEV-2

Is there minor inconvenience, a non-critical function affected,
or an isolated deviation with a workable fix?
└─ YES → 🟡 SEV-3

Is it cosmetic, a minor inefficiency, or an enhancement observation?
└─ YES → 🔵 SEV-4
```
