# Artifact Chain — Cross-Phase Validation Rules

## How to Use

After generating artifacts for any phase, validate them against prior phase outputs using the rules below. Surface warnings to the user but do NOT block progress.

---

## Phase Transitions & Required Documents

| Transition | Documents Passed Forward |
|------------|------------------------|
| Phase 0 → Phase 1 | `Problem-Statement.md`, `Stakeholder-Map.md` |
| Phase 1 → Phase 2 | `Requirements.md`, `Constraints-Register.md` |
| Phase 2 → Phase 3 | `Delivery-Plan.md`, `High-Level-Design.md`, Draft ADRs |
| Phase 3 → Phase 4 | `Architecture-Overview.md`, `Data-Contracts.md`, Accepted ADRs |
| Phase 4 → Phase 5 | `Implementation-Notes.md`, `Change-Log.md` |
| Phase 5 → Phase 6 | `Validation-Report.md`, `Traceability.md` |

---

## Validation Rules by Phase

### Phase 1 (Requirements) Validation

| Rule | Check | Severity |
|------|-------|----------|
| R1-1 | Every in-scope item from Problem Statement has at least one FR-xxx | Warning |
| R1-2 | Success criteria from Phase 0 map to acceptance criteria (AC-xxx) | Warning |
| R1-3 | Known constraints from Phase 0 appear in Constraints Register | Error |
| R1-4 | All FR-xxx use MUST/SHOULD/MAY language | Info |

### Phase 2 (Planning) Validation

| Rule | Check | Severity |
|------|-------|----------|
| R2-1 | Every FR-xxx appears in at least one work breakdown story | Warning |
| R2-2 | Constraints (C-xxx) are acknowledged in HLD | Warning |
| R2-3 | Rollout strategy addresses availability NFRs | Info |
| R2-4 | Definition of Done covers testing and documentation | Info |

### Phase 3 (Architecture) Validation

| Rule | Check | Severity |
|------|-------|----------|
| R3-1 | Architecture addresses all NFRs (security, perf, availability) | Warning |
| R3-2 | Data contracts cover all data requirements from Phase 1 | Warning |
| R3-3 | Constraints Register items are respected in architecture | Error |
| R3-4 | All HLD components appear in Architecture Overview | Warning |
| R3-5 | Draft ADRs from Phase 2 are either accepted or explicitly rejected | Info |

### Phase 4 (Execution) Validation

| Rule | Check | Severity |
|------|-------|----------|
| R4-1 | Implementation scope aligns with Delivery Plan work breakdown | Warning |
| R4-2 | No forbidden solutions (F-xxx) appear in implementation | Error |
| R4-3 | Architecture boundaries from Phase 3 are respected | Error |
| R4-4 | New technology choices not covered by ADR are flagged | Warning |

### Phase 5 (Testing) Validation

| Rule | Check | Severity |
|------|-------|----------|
| R5-1 | Every FR-xxx has at least one TC-xxx | Error |
| R5-2 | Every NFR-xxx has at least one TC-xxx | Warning |
| R5-3 | Constraints (C-xxx) have negative test cases | Warning |
| R5-4 | Edge cases from Implementation Notes have coverage | Info |
| R5-5 | Exit criteria are measurable and verifiable | Info |

### Phase 6 (Documentation) Validation

| Rule | Check | Severity |
|------|-------|----------|
| R6-1 | System Overview is consistent with Architecture Overview | Warning |
| R6-2 | All ADRs are referenced in Onboarding doc | Info |
| R6-3 | Failure modes from test reports appear in Runbook | Warning |
| R6-4 | Operational model from Phase 3 is reflected in Runbook | Warning |

---

## Severity Levels

- **Error**: Critical gap — likely to cause problems. Strongly recommend addressing before proceeding.
- **Warning**: Important gap — should be addressed but won't block progress.
- **Info**: Nice to have — optional improvement suggestion.

## Validation Output Format

```
Cross-Phase Validation Results:
================================
✅ R1-1: All in-scope items have requirements — PASS
⚠️ R1-2: Success criterion "95% uptime" has no AC-xxx — WARNING
❌ R1-3: Constraint "MUST use Python" from Phase 0 missing from Register — ERROR

Summary: 5 passed, 2 warnings, 1 error
```
