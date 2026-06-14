---
name: sdlc-phase-5-testing
description: "Phase 5 of SDLC: Testing & Validation. Proves the system meets requirements."
parent_skill: sdlc
---

# Phase 5 — Testing & Validation

## When to Load

Main skill routes here after Phase 4 is complete or user jumps to Phase 5.

## Prerequisites

- **Read** `docs/01-requirements/Requirements.md` (FR-xxx, NFR-xxx for traceability)
- **Read** `docs/04-execution/Implementation-Notes.md`
- **Read** `docs/04-execution/Change-Log.md`
- **Read** `docs/01-requirements/Constraints-Register.md`

## Workflow

### Step 1: Load Prior Context

1. Read Requirements (all FR-xxx and NFR-xxx IDs)
2. Read Implementation Notes (what was built, edge cases, limitations)
3. Read Constraints Register (what must not be violated)
4. Build a requirement-to-test mapping skeleton

### Step 1b: Apply Active Modes

**Auto-fill mode** — if active, scan the repository before asking any questions:

Scan targets: test directories (`tests/`, `test/`, `spec/`, `__tests__/`), CI configuration (`.github/workflows/`, `.circleci/`, `Makefile test` targets), coverage reports if present, existing test file names and function names.

After scanning, propose:
- Test types in use inferred from existing test files and imports
- Test cases per requirement by matching existing test names to FR-xxx IDs
- Entry/exit criteria inferred from CI pass/fail thresholds

Mark anything that can't be inferred as `[UNCLEAR — please provide]`. Present proposed answers and ask the user to confirm or correct specific items only.

**Personal project mode** — if active, apply before gathering information:

Load defaults from `references/personal-project-preset.md`. Collapse test environments:
- **Test Environments** (3) → ask only: "Local? Deployed prod?" — skip formal DEV/QA/PROD matrix.

Skip from the question batch:
- Formal environment matrix configuration differences (assume local = dev, deployed = prod).

Ask only: Test Scope, Test Types, Entry Criteria, Exit Criteria, Test Cases per requirement, Known Risks.

### Step 2: Gather Information (Batch Questions)

**Ask the user ALL of the following:**

1. **Test Scope** — What is in/out of testing scope for this iteration?
2. **Test Types Needed** — Which apply: Unit, Integration, Contract, Performance, Security?
3. **Test Environments** — DEV, QA, PROD? Configuration differences?
4. **Entry Criteria** — What must be true before testing begins?
5. **Exit Criteria** — What must be true to consider testing complete?
6. **Test Cases** — For each FR-xxx and NFR-xxx, what test verifies it?
   - Suggest test cases based on requirements (AI assistance)
7. **Known Risks** — Any areas of higher risk that need extra coverage?

### Step 3: Generate Artifacts

Load templates from `references/templates.md` and generate:

**Artifact 5.1 — Test Plan**
- File: `docs/05-testing/Test-Plan.md`
- Include scope, test types, environments, entry/exit criteria
- List test cases with IDs (TC-xxx)

**Artifact 5.2 — Traceability Matrix**
- File: `docs/05-testing/Traceability.md`
- Map EVERY FR-xxx and NFR-xxx to at least one TC-xxx
- Mark status: Planned, Passed, Failed, Blocked

**Artifact 5.3 — Validation Report** (if tests have been run)
- File: `docs/05-testing/Validation-Report.md`
- Execution summary, results, defects, risk acceptance

### Step 4: Cross-Phase Validation (Critical)

This is the most important validation step:

- **Every FR-xxx** must have at least one TC-xxx → warn if missing
- **Every NFR-xxx** must have at least one TC-xxx → warn if missing
- **Constraints (C-xxx)** should have negative test cases (prove they can't be violated)
- **Edge cases** from Implementation Notes should have coverage

```
⚠️ Traceability gaps:
- FR-003 has no test case assigned
- NFR-002 (Availability) has no test case
- Constraint C-001 has no negative test
```

### Step 5: Present & Confirm

**⚠️ MANDATORY STOPPING POINT**: Present artifacts for approval.

Highlight:
- Total coverage: X/Y requirements have test cases
- Gaps found (if any)
- Suggested additional test cases for uncovered requirements

### Step 6: Completion

After writing, return control to main SKILL.md.

## Output

- `docs/05-testing/Test-Plan.md`
- `docs/05-testing/Traceability.md`
- `docs/05-testing/Validation-Report.md` (optional, if tests already run)

## Next

Return to main skill → ADR check → offer Phase 6 (Documentation & Knowledge Capture)
