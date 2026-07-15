**Document:** `project_management/sprints/operations/T2_QA_Workflow/qa_checklist.md
**Sprint:** Operations Sprint — Quality Assurance, Supply Chains & Procurement
**Owner:** QA Lead / Operations Sprint Team
**Standards:** ISO 9001 · Lean/Six Sigma · SRE/ITIL · Nielsen's 10 Usability Heuristics
**Status:** DRAFT v1.0
**Last Updated:** 2025-07-08

---

## Purpose & Scope

This checklist maps Vynues QA workflow to:
1. Test artifacts in `tests/` (unit, integration, E2E, API, performance)
2. UX heuristics (Nielsen's 10 + WCAG 2.1 AA)
3. Defect-severity taxonomy established in T1
4. Acceptance criteria gates before any release or vendor-facing deployment

Use this checklist at every **sprint review gate**, **release candidate cut**, and **vendor/client delivery milestone**.

---

## Checklist Structure

```
Section A  — Pre-Testing Readiness
Section B  — Test Artifact Coverage (maps to tests/)
Section C  — Functional & API Acceptance
Section D  — UX Heuristic Review
Section E  — Accessibility (WCAG 2.1 AA)
Section F  — Performance & Reliability
Section G  — Security & Compliance
Section H  — Defect Triage & Resolution Gate
Section I  — Release / Delivery Sign-Off
```

---

## Section A — Pre-Testing Readiness

> **Gate:** All items must be ✅ before test execution begins.

| ID | Check | Owner | Status | Notes |
|----|-------|-------|--------|-------|
| A1 | Test environment matches production configuration (env vars, DB seed, API keys masked) | DevOps | ☐ | |
| A2 | `tests/` directory artifacts are current — no stale fixtures or commented-out suites | QA Lead | ☐ | Audit `tests/` file tree |
| A3 | Acceptance criteria for the sprint/feature are documented and signed off by Product | Product + QA | ☐ | Reference T1 criteria doc |
| A4 | Defect-severity taxonomy (T1) is accessible to all testers | QA Lead | ☐ | Link to T1 doc in ticket |
| A5 | Regression suite baseline from prior sprint is available and passing | QA Lead | ☐ | CI pipeline green |
| A6 | Test data (venues, vendors, events, users) is seeded and version-controlled | QA Lead | ☐ | Check `tests/fixtures/` |
| A7 | All external vendor API sandboxes / stubs are live and accessible | DevOps | ☐ | |
| A8 | Browser/device matrix confirmed (see Section D) | QA Lead | ☐ | |
| A9 | QA environment access granted to all team members running checks | DevOps | ☐ | |
| A10 | Known pre-existing defects documented and risk-accepted by Product Owner | Product | ☐ | |

---

## Section B — Test Artifact Coverage

> Maps directly to the `tests/` directory structure. Each sub-section corresponds to a test type. Coverage thresholds are minimums — flag any suite below threshold as a **Severity-2 blocker**.

### B1 — Unit Tests (`tests/unit/`)

| ID | Check | Threshold | Status | Notes |
|----|-------|-----------|--------|-------|
| B1.1 | All new functions/methods have corresponding unit tests | 100% new code | ☐ | |
| B1.2 | Overall unit test code coverage ≥ 80% (line + branch) | ≥ 80% | ☐ | Export coverage report |
| B1.3 | Edge cases covered: null inputs, empty arrays, max-length strings, negative integers | Per function | ☐ | |
| B1.4 | Business-logic units tested in isolation (mocks/stubs for dependencies) | All BL modules | ☐ | |
| B1.5 | Unit tests execute in < 2 min total in CI | < 2 min | ☐ | |
| B1.6 | No test is marked `.skip` or `.only` in committed code | 0 skips | ☐ | |
| B1.7 | Test naming follows convention: `[module]_[function]_[scenario]_[expected]` | 100% | ☐ | |

**Vynues-Specific Unit Checks:**

| ID | Module | Check | Status |
|----|--------|-------|--------|
| B1.V1 | Venue-matching algorithm | Unit tests cover matching weight scoring, tie-breaking, and null-result paths | ☐ |
| B1.V2 | Vendor-ranking logic | Tests cover ranking with 0, 1, and N vendors; capacity-constraint edge cases | ☐ |
| B1.V3 | Pricing / quote calculator | Tests cover floor price, ceiling cap, discount stacking, and zero-guest edge case | ☐ |
| B1.V4 | Availability engine | Tests cover double-booking prevention, timezone normalization, DST edge case | ☐ |
| B1.V5 | Notification dispatcher | Tests cover retry logic, deduplication, and channel-fallback (email → SMS) | ☐ |

---

### B2 — Integration Tests (`tests/integration/`)

| ID | Check | Threshold | Status | Notes |
|----|-------|-----------|--------|-------|
| B2.1 | All service-to-service integrations have integration tests | 100% integration points | ☐ | |
| B2.2 | Database CRUD operations tested end-to-end against test DB | All models | ☐ | |
| B2.3 | Auth flow tested: signup → login → token refresh → logout | Full flow | ☐ | |
| B2.4 | Venue search → selection → booking flow tested as integrated sequence | Full flow | ☐ | |
| B2.5 | Vendor assignment → confirmation → notification flow tested | Full flow | ☐ | |
| B2.6 | Payment integration tested in sandbox mode (charge, refund, failure) | All paths | ☐ | |
| B2.7 | Integration tests isolated from production data (separate DB schema/container) | 100% | ☐ | |
| B2.8 | Integration suite completes in < 10 min in CI | < 10 min | ☐ | |

---

### B3 — End-to-End Tests (`tests/e2e/`)

| ID | Check | Status | Notes |
|----|-------|--------|-------|
| B3.1 | Critical user journeys (CUJs) below are each covered by at least one E2E test | ☐ | |
| B3.2 | E2E tests run in headless browser (Playwright / Cypress) against staging | ☐ | |
| B3.3 | E2E suite passes with 0 failures on release candidate build | ☐ | |
| B3.4 | Screenshots / video artifacts captured on failure and linked in defect ticket | ☐ | |
| B3.5 | E2E tests are deterministic — no flaky tests in last 5 CI runs | ☐ | Flag flaky tests as S2 |

**Critical User Journeys (CUJ) Traceability Matrix:**

| CUJ ID | Journey | E2E Test File | Pass/Fail | Defect ID |
|--------|---------|---------------|-----------|-----------|
| CUJ-01 | B2C: New user signup → profile creation → first event inquiry | `tests/e2e/b2c_onboarding.spec` | ☐ | |
| CUJ-02 | B2C: Event search → venue browse → venue shortlist → inquiry submission | `tests/e2e/b2c_venue_search.spec` | ☐ | |
| CUJ-03 | B2C: Vendor browse → vendor inquiry → quote review → booking confirmation | `tests/e2e/b2c_vendor_booking.spec` | ☐ | |
| CUJ-04 | B2C: Payment capture → receipt → booking dashboard update | `tests/e2e/b2c_payment.spec` | ☐ | |
| CUJ-05 | B2B: Venue/vendor account creation → listing setup → availability config | `tests/e2e/b2b_listing_setup.spec` | ☐ | |
| CUJ-06 | B2B: Inquiry received → quote sent → contract signed (digital signature flow) | `tests/e2e/b2b_contract_flow.spec` | ☐ | |
| CUJ-07 | B2B: Dashboard — booking management, calendar sync, analytics view | `tests/e2e/b2b_dashboard.spec` | ☐ | |
| CUJ-08 | Admin: Vendor approval workflow → tier assignment → SLA configuration | `tests/e2e/admin_vendor_approval.spec` | ☐ | |
| CUJ-09 | EULA / ToS acceptance flow — digital signature capture and record storage | `tests/e2e/legal_acceptance_flow.spec` | ☐ | Maps to KR6, KR7 |
| CUJ-10 | Cancellation → refund initiation → vendor notification → status update | `tests/e2e/cancellation_refund.spec` | ☐ | |

---

### B4 — API Tests (`tests/api/`)

| ID | Check | Status | Notes |
|----|-------|--------|-------|
| B4.1 | All public API endpoints documented in OpenAPI/Swagger spec | ☐ | |
| B4.2 | Every endpoint has a corresponding API test (happy path + error paths) | ☐ | |
| B4.3 | HTTP status codes validated: 200, 201, 400, 401, 403, 404, 409, 422, 500 | ☐ | |
| B4.4 | Response schema validated against OpenAPI contract (no schema drift) | ☐ | |
| B4.5 | Auth boundary tests: unauthenticated requests return 401; unauthorized return 403 | ☐ | |
| B4.6 | Rate-limiting tested: requests beyond threshold return 429 with Retry-After header | ☐ | |
| B4.7 | Pagination tested: `page`, `limit`, `cursor` params produce correct slices | ☐ | |
| B4.8 | Input validation tested: malformed JSON, XSS strings, SQL injection strings | ☐ | |
| B4.9 | API versioning: `v1` endpoints backward-compatible; breaking changes require `v2` | ☐ | |
| B4.10 | Vendor API integrations (venue data providers, payment, calendar) tested with mocks | ☐ | |

---

### B5 — Performance Tests (`tests/performance/`)

| ID | Check | Threshold | Status | Notes |
|----|-------|-----------|--------|-------|
| B5.1 | Venue search API response time under normal load | p95 ≤ 500ms | ☐ | |
| B5.2 | Venue search API response time under peak load (10× normal) | p95 ≤ 1,500ms | ☐ | |
| B5.3 | Page load time — critical pages (home, search results, venue detail) | LCP ≤ 2.5s | ☐ | Core Web Vitals |
| B5.4 | Time to Interactive (TTI) — booking flow pages | TTI ≤ 3.8s | ☐ | |
| B5.5 | Database query time for matching/ranking algorithm | p99 ≤ 200ms | ☐ | |
| B5.6 | Concurrent booking transactions tested (no race condition / double-book) | 50 concurrent | ☐ | |
| B5.7 | Memory leak check: extended soak test (60 min) shows stable heap | No growth > 5% | ☐ | |
| B5.8 | API throughput: requests per second under load | ≥ 500 RPS | ☐ | |

---

## Section C — Functional & API Acceptance

| ID | Feature Area | Acceptance Criterion | Pass/Fail | Defect ID |
|----|-------------|---------------------|-----------|-----------|
| C1 | User Authentication | Users can sign up, verify email, log in, reset password, and log out without error | ☐ | |
| C2 | Venue Search & Filtering | Search returns results filtered by location, capacity, date, category, and price range within 500ms | ☐ | |
| C3 | Venue Detail Page | All venue fields render correctly: photos, capacity, amenities, pricing, availability calendar | ☐ | |
| C4 | Inquiry / Booking Request | User can submit inquiry; venue/vendor receives notification within 60 seconds | ☐ | |
| C5 | Quote & Proposal Flow | Venue/vendor can generate and send quote; client can accept/reject; status updates reflected | ☐ | |
| C6 | Contract & eSignature | Digital signature captured, timestamped, stored, and accessible in dashboard (maps to KR6/KR7) | ☐ | |
| C7 | Payment Processing | Payments captured, receipts issued, refunds processed; all sandbox transactions reconcile | ☐ | |
| C8 | Calendar & Availability | Availability blocks create/update correctly; double-booking prevented; iCal sync functional | ☐ | |
| C9 | Vendor Dashboard | Bookings, inquiries, analytics, and documents visible and accurate | ☐ | |
| C10 | Notification System | Email and in-app notifications delivered for all trigger events; no duplicates | ☐ | |
| C11 | Admin Panel | Admin can approve/reject vendors, assign risk tiers, configure SLAs, view audit logs | ☐ | |
| C12 | EULA / ToS Acceptance | Acceptance event logged with user ID, timestamp, IP, version — queryable for compliance | ☐ | |
| C13 | Supply Chain Visibility | Venue/vendor status visible to ops team in real time (maps to T3 SCOR deliver stage) | ☐ | |
| C14 | Reporting & KPI Export | KPI dashboard exports CSV/PDF; data matches source records (maps to T7) | ☐ | |

---

## Section D — UX Heuristic Review

> Review against **Nielsen's 10 Usability Heuristics**. Each heuristic rated: ✅ Pass · ⚠️ Minor Issue · ❌ Fail (Defect Required)

### D0 — Review Scope & Device Matrix

**Pages under review this sprint:** _(list sprint-specific pages)_
- [ ] Homepage / Landing
- [ ] Venue Search Results
- [ ] Venue Detail
- [ ] Vendor Profile
- [ ] Booking / Inquiry Flow
- [ ] Quote & Contract Flow
- [ ] Payment
- [ ] B2B Dashboard
- [ ] B2C User Dashboard
- [ ] Admin Panel

**Device / Browser Matrix:**

| Device | Browser | Viewport | Tester | Status |
|--------|---------|----------|--------|--------|
| Desktop | Chrome latest | 1440×900 | | ☐ |
| Desktop | Firefox latest | 1440×900 | | ☐ |
| Desktop | Safari latest | 1440×900 | | ☐ |
| Desktop | Edge latest | 1440×900 | | ☐ |
| Tablet | Safari iOS | 768×1024 | | ☐ |
| Tablet | Chrome Android | 800×1280 | | ☐ |
| Mobile | Safari iOS | 390×844 | | ☐ |
| Mobile | Chrome Android | 360×800 | | ☐ |

---

### D1 — Visibility of System Status

> *"The system should always keep users informed about what is going on, through appropriate feedback within reasonable time."*

| ID | Check | Pages | Status | Defect ID |
|----|-------|-------|--------|-----------|
| D1.1 |
