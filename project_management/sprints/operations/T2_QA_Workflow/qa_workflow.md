
# QA Workflow — Vynues

## Overview

Seven-phase workflow from story creation through production
monitoring. Every phase maps to a test artifact layer, a UX
heuristic checkpoint, a severity gate, and a named owner.

```
PLAN ──► DEVELOP ──► TEST ──► TRIAGE ──► RELEASE ──► MONITOR ──► IMPROVE
```

---

## Phase 1 — PLAN: Acceptance Criteria & Test Skeleton

**Trigger:** Product Owner creates or refines a user story.

**Outputs:**
- Acceptance criteria written in Given/When/Then format
- Test file skeleton committed to `tests/e2e/flows/`
- Severity floor pre-assigned to story

**Gate — story is NOT sprint-ready until:**
- [] Acceptance criteria written (Given/When/Then)
- [ ] Test skeleton committed to `tests/`
- [ ] Severity floor assigned (S1/S2/S3/S4)
- [ ] UX heuristics at risk identified (H1–H14)

**Owner:** Product Owner + QA Lead

**Acceptance Criteria Template:**
```
GIVEN  [system / user precondition]
WHEN   [action taken]
THEN   [observable, measurable outcome]
AND    [additional assertions]

Severity floor:        S1 / S2 / S3 / S4
UX heuristic(s):       H#
Test artifact(s):      tests/path/to/file
```

---

## Phase 2 — DEVELOP: Shift-Left Testing

**Trigger:** Developer picks up sprint-ready story.

**Outputs:**
- Unit tests in `tests/unit/<module>/`
- Integration test stubs in `tests/integration/<boundary>/`

**Developer QA Checklist (required before PR open):**
- [ ] Unit tests written and passing locally
- [ ] Integration stubs committed
- [ ] Coverage delta ≥ 80% on net-new code
- [ ] H5 (Error Prevention) self-review complete
- [ ] H9 (Error Recovery) self-review complete
- [ ] No secrets or PII in test fixtures
- [ ] Acceptance criteria referenced in PR description

**Owner:** Software Engineer (author)

---

## Phase 3 — TEST: Multi-Layer Execution

### 3a — Automated CI Pipeline (every PR)

| Layer | Artifact | Pass Criteria |
|---|---|---|
| Unit | `tests/unit/` | 0 failures; ≥80% net-new coverage |
| Integration | `tests/integration/` | 0 failures on critical paths |
| Contract | `tests/contracts/*.pact` | No breaking API changes |

**Gate:** All three layers must pass before merge to `develop`.

### 3b — End-to-End Flows (merge to `develop`)

| Flow | Artifact | Heuristics Validated |
|---|---|---|
| Event creation | `tests/e2e/flows/event_creation_flow.spec` | H1, H2, H7 |
| Vendor booking | `tests/e2e/flows/vendor_booking_flow.spec` | H1, H6, H10 |
| Payment checkout | `tests/e2e/flows/payment_checkout_flow.spec` | H5, H9, H8 |
| Vendor onboarding | `tests/e2e/flows/vendor_onboarding_flow.spec` | H6, H4, H5 |

**E2E Pass Criteria:**
- All happy-path scenarios pass
- All error-path scenarios show correct user-facing messages
- No broken navigation or dead-end screens
- Page transitions ≤ 2 s; search results ≤ 5 s

### 3c — Performance Testing (release candidate)

| Test | Artifact | Threshold |
|---|---|---|
| Venue search load | `tests/performance/venue_search_load.k6` | p95 ≤ 3 s @ 200 concurrent users |
| Booking engine stress | `tests/performance/booking_engine_stress.k6` | 0 errors @ 100 concurrent bookings |
| API throughput | `tests/performance/api_throughput.k6` | ≥ 500 req/s for 5 min sustained |

### 3d — Security Scanning (release candidate)

| Check | Artifact | Standard |
|---|---|---|
| Auth & session | `tests/security/auth_penetration/` | OWASP Top 10; no privilege escalation |
| Dependencies | `tests/security/dependency_scan/` | 0 Critical CVEs in production deps |
| Data exposure | `tests/security/` | No PII in API responses or logs |

### 3e — UX Heuristic Audit (every sprint + release candidate)

See `ux_heuristics.md` for full H1–H14 audit framework.

**Sprint cadence:** Lightweight spot-check, QA + UX, ≤ 2 hours.
**Release cadence:** Full audit against all 14 heuristics.
**Accessibility:** WCAG 2.1 AA audit every release candidate.

---

## Phase 4 — TRIAGE: Defect Severity Routing

**Routing is mechanical — severity drives action, no judgment calls.**

| Severity | Action | SLA |
|---|---|---|
| S1— Critical | Halt release. Page on-call. War room. | Fix within 4 hours |
| S2 — High | Block current story. Fix within sprint. | Fix within 24 hours |
| S3 — Medium | Backlog with priority tag. | Fix within 2 sprints |
| S4 — Low | Backlog. | Fix at discretion |

**Required for every defect before fix is merged:**
- Regression test committed to `tests/regression/DEF-[NNNN]_<desc>.spec`

**Defect Record Fields:**
```
ID:               DEF-[NNNN]
Title:            [component] — [brief description]
Severity:         S0 / S1 / S2 / S3
Heuristic(s):     H# (if UX-related)
Affected flow:    tests/e2e/flows/<name>
Steps to repro:   [numbered]
Expected:         [from acceptance criteria]
Actual:           [observed]
Evidence:         [screenshot / log / trace link]
Assigned to:      [engineer]
SLA deadline:     [auto-calculated]
Regression test:  tests/regression/DEF-[NNNN]_<desc>.spec
Status:           Open / In Fix / In Verification / Closed
```

---

## Phase 5 — RELEASE: QA Sign-Off Gate

**No deployment proceeds without QA Lead sign-off.**

See `qa_checklist.md` — Release Gate Checklist.

**Owner:** QA Lead
**Sign-off recorded in:** Release ticket + deployment log

---

## Phase 6 — MONITOR: Production Observability

| Signal | Tool Slot | Threshold / Alert |
|---|---|---|
| Error rate | APM (Datadog / Sentry) | > 1% 5xx errors → page on-call |
| Latency (p95) | APM | > 3 s venue search → alert |
| Booking success rate | Custom metric | < 98% → alert QA Lead |
| UX drop-off rate | Analytics | > 15% drop-off at checkout → UX review |

**Defect creation rule:** Any production alert that persists > 15 min
becomes a defect record (Phase 4 triage) with severity assigned.

---

## Phase 7 — IMPROVE: Continuous Improvement

| Activity | Frequency | Owner |
|---|---|---|
| Sprint retrospective — QA items | Every sprint | QA Lead + Team |
| Defect trend review | Monthly | QA Lead |
| KPI baseline review | Monthly | QA Lead + COO |
| Full QA document review | Quarterly | QA Lead |
| Heuristic audit + UX review | Quarterly | UX Lead |

**Input to improvement:** Defect trends, KPI deltas,
retrospective actions, production incident post-mortems.

---
*Sprint: Operations Sprint — T2*
*Owner: QA Lead*
*Last updated: [DATE]*
```

