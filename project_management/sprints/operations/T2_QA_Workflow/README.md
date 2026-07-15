
# QA — UX Quality Assurance Directory

## Purpose
This directory contains the QA workflow, UX heuristic audit framework,
and QA execution checklists for Vynues. All files in this directory
are operational documents — they govern how quality is measured,
tested, and signed off before any release.

## Files

| File | Purpose |
|---|---|
| `qa_workflow.md` | End-to-end QA execution workflow (7 phases) |
| `ux_heuristics.md` | UX heuristic audit framework (H1–H14) |
| `qa_checklist.md` | Sprint and release-gate checklists |

## Relationship to `tests/`

| QA Artifact Here | Maps To |
|---|---|
| `qa_workflow.md` Phase 2 | `tests/unit/` · `tests/integration/` |
| `qa_workflow.md` Phase 3 | `tests/e2e/` · `tests/performance/` · `tests/security/` |
| `ux_heuristics.md` | `tests/ux/heuristic_audits/` |
| `qa_checklist.md` | All layers — sprint gate + release gate |

## Ownership

| Role | Responsibility |
|---|---|
| QA Lead | Maintains all files; owns workflow gates |
| UX Designer | Co-owns `ux_heuristics.md`; runs heuristic audits |
| Product Owner | Co-owns acceptance criteria in `qa_checklist.md` |
| Engineering Lead | Enforces CI gates mapped in `qa_workflow.md` |

## Cadence

| Review | Frequency |
|---|---|
| Heuristic spot-check | Every sprint |
| Full heuristic audit | Quarterly |
| Accessibility audit | Every release candidate |
| Document review | Quarterly or after any S0 incident |

---
*Sprint: Operations Sprint — T2*
*Owner: QA Lead*
*Last updated: [DATE]*
