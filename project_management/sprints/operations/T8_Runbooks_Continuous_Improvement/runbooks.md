# Operations Runbooks — Library

This document contains the five runbooks identified as required in the Operations Runbooks (T8) framework document. Each follows the Standard Runbook Format defined there. Content is synthesized from the process detail already established in QA Workflow (T2), SCOR Framework Applied to Vynues (T3), Procurement Contract (T5), Vendor Onboarding Process (T6), and Vendor Performance Scorecard (T6).

---

## Runbook 1 — Vendor Onboarding

| Field | Detail |
|---|---|
| **Objective** | Evaluate, approve, and integrate a new vendor into the Vynues procurement process before they are eligible for project assignment. |
| **Trigger** | A department submits a vendor request identifying a business need for a new vendor. |
| **Process Owner** | Operations Team (execution); Operations Manager (final approval). |
| **Required Inputs** | Vendor request (business name, contact, address, services offered); Business Registration; Tax Documentation; Insurance Certificate; Professional Licenses (if applicable); Banking Information; Vendor Agreement; Procurement Contract; SLA. |
| **Procedure** | 1. Requesting department submits vendor request to Operations Team. 2. Vendor submits required documentation. 3. Operations Team verifies documentation completeness and accuracy; returns for correction if incomplete. 4. Operations Team evaluates vendor against eligibility criteria (capability, industry experience, financial stability, references, insurance, compliance). 5. Operations Manager reviews the completed onboarding package. 6. If approved, vendor is added to the approved vendor registry and becomes eligible for project assignment. If not approved, vendor is notified of outstanding requirements and the process remains open. |
| **Expected Outputs** | Approved vendor added to the vendor registry; executed Vendor Agreement, Procurement Contract, and SLA; initial Vendor Risk Tier assignment (Vendor Risk Assessment Process, T6). |
| **Escalation Requirements** | Escalate to Level 2 (Department Manager) if documentation remains incomplete after two follow-up requests, or if evaluation criteria cannot be verified. Escalate to Level 3 (COO) if the vendor is being considered for a Critical-risk-tier engagement. |
| **Success Criteria** | Vendor is fully documented, evaluated, risk-tiered, and either approved with an active file in the registry or clearly notified of outstanding requirements — with no onboarding request left in an undetermined state. |

---

## Runbook 2 — Procurement Approval

| Field | Detail |
|---|---|
| **Objective** | Formalize a vendor engagement through a signed Procurement Contract and SLA before work begins on a specific event or project. |
| **Trigger** | A vendor has been shortlisted and selected for a specific event (SCOR Source phase) and is ready to move to contracting. |
| **Procedure Owner** | Procurement. |
| **Required Inputs** | Vendor quotations/proposals; approved vendor status (from Vendor Onboarding runbook); budget authorization; contract templates (Procurement Contract, SLA, Change Order Form); insurance certificates. |
| **Procedure** | 1. Procurement negotiates pricing and scope with the selected vendor. 2. Procurement completes the Procurement Contract (Parts 1–5: parties, definitions, scope, deliverables, pricing/payment schedule) using the standard template. 3. Procurement confirms the SLA is attached and its performance standards match the engagement type. 4. Contract routes for required internal approvals (budget, legal if applicable). 5. Contract and SLA are signed by both parties. 6. Deposit is collected per the payment schedule. 7. Signed documents are filed in procurement records with the Contract ID. |
| **Expected Outputs** | Signed Procurement Contract; signed SLA; issued purchase order; confirmed booking; deposit collected. |
| **Escalation Requirements** | Escalate to Level 2 (Department Manager) if contract terms cannot be agreed within the standard negotiation window or if budget authorization is exceeded. Escalate to Level 3 (COO) for any contract requiring a liability cap or remedy terms outside standard template ranges. |
| **Success Criteria** | Fully executed Procurement Contract and SLA on file before the vendor's setup/delivery start date, with all Part 3 (Scope) and Part 5 (Pricing) fields completed — no [PLACEHOLDER] fields remaining. |

---

## Runbook 3 — Quality Assurance Review

| Field | Detail |
|---|---|
| **Objective** | Verify that an operational deliverable, vendor deliverable, or platform release meets Vynues quality standards before approval. |
| **Trigger** | A deliverable reaches the Verify phase of the QA Workflow (T2) — e.g., a vendor deliverable is ready for inspection, or a platform feature is ready for release review. |
| **Process Owner** | Quality Assurance. |
| **Required Inputs** | QA Standards (T1); Acceptance Criteria; QA Checklist (T2); Defect Severity Taxonomy (T1); UX Heuristic Audit Framework (T2) if the review is platform-related. |
| **Procedure** | 1. Reviewer completes the QA Checklist sections relevant to the deliverable type (Documentation Review, Operational Review, Acceptance Review). 2. For platform/UX-related reviews, apply the relevant Nielsen heuristics (H1–H10) and log findings. 3. Any deficiency found is logged as a defect and classified using the Defect Severity Taxonomy (S1–S4). 4. Corrective action is assigned to the responsible owner. 5. Reviewer verifies the correction before closing the defect. 6. Once all Acceptance Criteria are satisfied and no S1/S2 defects remain open, the reviewer issues approval. |
| **Expected Outputs** | Completed QA Checklist; logged and classified defects (if any); verified corrective actions; QA approval or documented hold. |
| **Escalation Requirements** | Escalate to Level 2 (Department Manager) for any unresolved S2 defect after the standard correction window. Escalate to Level 3 (COO) for any S1 defect, per the Defect Severity Taxonomy's required immediate escalation. |
| **Success Criteria** | Deliverable has zero open S1 or S2 defects and a completed, signed-off QA Checklist prior to approval for release or delivery. |

---

## Runbook 4 — Supply Chain Issue Response

| Field | Detail |
|---|---|
| **Objective** | Respond to and resolve a disruption in the venue/vendor supply chain (e.g., vendor no-show, double-booking, equipment failure) with minimal impact to event execution. |
| **Trigger** | Any risk identified in the SCOR Framework's phase-level risk registers (T3) materializes — e.g., a vendor cancels, a venue becomes unavailable, or a Deliver-phase incident occurs. |
| **Process Owner** | On-Site Coordinator (Deliver-phase issues) or Operations (Plan/Source/Make-phase issues), per the SCOR Full Supply Chain Summary (T3). |
| **Required Inputs** | Event brief and vendor shortlist (Plan); signed contracts and SLA (Source); run-of-show and vendor briefing packets (Make); incident report template. |
| **Procedure** | 1. Issue is identified and logged with the affected SCOR phase, vendor, and event. 2. Coordinator attempts resolution using existing contingencies (backup vendor shortlist, SLA remedy provisions, change order if scope must shift). 3. If resolved, document the resolution and root cause. 4. If not resolved within the standard response window, escalate per the Escalation Paths (T8) process. 5. Post-incident, log findings in the vendor's performance record (feeds Vendor Performance Scorecard, T6) and the Return-phase root cause analysis (T3). |
| **Expected Outputs** | Incident report; resolution record or escalation record; updated vendor performance/risk data; root cause analysis for recurring or high-impact issues. |
| **Escalation Requirements** | Escalate to Level 2 (Department Manager) if the issue affects event timeline or budget. Escalate to Level 3 (COO) if the issue is a Deliver-phase safety incident, a vendor no-show with no available backup, or triggers contract remedies under Part 6 of the Procurement Contract (T5). |
| **Success Criteria** | Issue resolved (or escalated and resolved at the appropriate level) before it prevents event execution; incident documented; root cause and corrective action captured for repeated or high-severity issues. |

---

## Runbook 5 — Vendor Performance Review

| Field | Detail |
|---|---|
| **Objective** | Evaluate a vendor's performance following a completed project or service engagement and update their standing accordingly. |
| **Trigger** | A project or event involving the vendor reaches completion (SCOR Return phase). |
| **Process Owner** | Project Manager (completes evaluation); Operations Team (reviews and tracks trends). |
| **Required Inputs** | Vendor Performance Scorecard (T6) template; Procurement Contract and SLA for the engagement; incident reports (if any) from Supply Chain Issue Response; customer feedback/survey results. |
| **Procedure** | 1. Project Manager completes the Vendor Performance Scorecard within [X] days of project completion, scoring each of the seven weighted categories (1–5 scale). 2. Calculate the weighted overall score and determine vendor classification (Preferred / Approved / Improvement Required / Under Review). 3. Reviewer documents strengths, areas for improvement, and corrective actions if required. 4. Results are shared with the vendor when appropriate. 5. Update the vendor's Risk Tier (Vendor Risk Assessment Process, T6) if the outcome affects their risk classification — e.g., two consecutive Preferred/Approved ratings may lower the tier; any S1/S2 defect during the engagement may raise it. |
| **Expected Outputs** | Completed Vendor Performance Scorecard; updated vendor classification; updated Vendor Risk Tier where applicable; corrective action plan (if Improvement Required or Under Review). |
| **Escalation Requirements** | Escalate to Level 2 (Department Manager) if a vendor scores "Improvement Required" for two consecutive engagements. Escalate to Level 3 (COO) if a vendor scores "Under Review" or is moved to the Critical risk tier as a result of the review. |
| **Success Criteria** | Scorecard completed and filed within the required window after every engagement; vendor classification and risk tier reflect the most recent evaluation; corrective action plans are issued and tracked for any vendor scoring below "Approved." |

---

## Runbook Maintenance

These runbooks should be reviewed on the same Quarterly cadence defined in Review Cadence (T8), and updated whenever the underlying process (T2, T3, T5, T6) changes. Review results feed into the Continuous Improvement Process (T8).
