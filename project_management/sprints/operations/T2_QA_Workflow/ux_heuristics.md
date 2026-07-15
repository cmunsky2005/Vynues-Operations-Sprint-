
# UX Heuristic Audit Framework — Vynues

## Overview

14 heuristics: Nielsen's original 10 (H1–H10) plus 4 Vynues
event-platform extensions (H11–H14). Each heuristic has:
- A plain-language definition
- A Vynues-specific application
- The audit question(s) to ask
- The test artifact it maps to
- The defect severity floor if violated

---

## Heuristic Reference Table

| # | Name | Severity Floor if Violated |
|---|---|---|
| H1 | Visibility of system status | S1 |
| H2 | Match between system and real world | S2 |
| H3 | User control and freedom | S1 |
| H4 | Consistency and standards | S2 |
| H5 | Error prevention | S1 |
| H6 | Recognition over recall | S2 |
| H7 | Flexibility and efficiency of use | S3 |
| H8 | Aesthetic and minimalist design | S3 |
| H9 | Help users recognize, diagnose, recover from errors | S1 |
| H10 | Help and documentation | S3 |
| H11 | Trust and transparency *(ext.)* | S1 |
| H12 | Time sensitivity *(ext.)* | S1 |
| H13 | Multi-stakeholder clarity *(ext.)* | S2 |
| H14 | Regulatory and compliance visibility *(ext.)* | S0 |

---

## H1 — Visibility of System Status

**Definition:** The system always keeps users informed about
what is going on, through appropriate feedback within
reasonable time.

**Vynues application:** Booking and payment processing states
must be visible in real time. Users must never be unsure
whether a booking was confirmed or a payment was submitted.

**Audit questions:**
- Does every async action (search, booking, payment) show
  a loading / processing indicator?
- Is the final state (confirmed / failed / pending) clearly
  communicated?
- Are booking confirmation details immediately visible
  and retrievable?

**Test artifact:** `tests/e2e/flows/payment_checkout_flow.spec`
· `tests/e2e/flows/vendor_booking_flow.spec`

**Severity floor if violated:** S1

---

## H2 — Match Between System and Real World

**Definition:** The system speaks the users' language, using
words, phrases, and concepts familiar to the user.

**Vynues application:** Event-industry vocabulary must be used
throughout: headcount, run-of-show, F&B minimum, hold,
tentative, confirmed, room flip, setup/breakdown window.

**Audit questions:**
- Are technical or internal terms exposed to end users?
- Does the venue/vendor search use industry-standard
  category names?
- Are date/time formats appropriate for the user's locale?

**Test artifact:** `tests/ux/heuristic_audits/H2_language_match.md`

**Severity floor if violated:** S2

---

## H3 — User Control and Freedom

**Definition:** Users often choose system functions by mistake
and need a clearly marked "emergency exit."

**Vynues application:** Cancel / back must be available at every
step of the booking wizard. Users must be able to exit any
flow without completing it and without data loss.

**Audit questions:**
- Is there a visible back/cancel option at every wizard step?
- Does canceling a booking mid-flow warn the user of
  any fee implications before confirming?
- Is unsaved work (event draft) preserved on accidental exit?

**Test artifact:** `tests/e2e/flows/event_creation_flow.spec`
· `tests/ux/heuristic_audits/H3_user_control.md`

**Severity floor if violated:** S1

---

## H4 — Consistency and Standards

**Definition:** Users should not have to wonder whether
different words, situations, or actions mean the same thing.

**Vynues application:** The vendor portal must match main app
conventions. Design system components must be used
consistently. "Book," "Reserve," and "Hold" must have
consistent, defined meanings platform-wide.

**Audit questions:**
- Are the same actions labeled the same way across
  all surfaces?
- Does the vendor-facing portal use the same design
  system as the planner-facing app?
- Are status labels (Confirmed / Tentative / Cancelled)
  used identically everywhere?

**Test artifact:** `tests/e2e/flows/vendor_onboarding_flow.spec`
· `tests/ux/heuristic_audits/H4_consistency.md`

**Severity floor if violated:** S2

---

## H5 — Error Prevention

**Definition:** Even better than good error messages is a
careful design that prevents a problem from occurring.

**Vynues application:** Form validation before submission.
Double-confirm on cancellations with fees. Card details
validated client-side before API call. Date conflicts
flagged before booking is attempted.

**Audit questions:**
- Are required fields validated before form submission?
- Is the user warned before any irreversible action
  (cancellation with fee, permanent delete)?
- Are date/time conflicts detected before the user
  reaches the payment step?

**Test artifact:** `tests/e2e/flows/payment_checkout_flow.spec`
· `tests/ux/heuristic_audits/H5_error_prevention.md`

**Severity floor if violated:** S1

---

## H6 — Recognition Over Recall

**Definition:** Minimize the user's memory load by making
objects, actions, and options visible.

**Vynues application:** Venue and vendor cards show images,
ratings, capacity, and key attributes — users never need to
remember a code or ID. Saved searches and recent events
are surfaced automatically.

**Audit questions:**
- Can users identify a venue/vendor from its card


