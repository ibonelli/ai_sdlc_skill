---
name: sdlc-phase-1-requirements
description: "Phase 1 of SDLC: Requirements & Constraints. Defines what must be true."
parent_skill: sdlc
---

# Phase 1 — Requirements & Constraints

## When to Load

Main skill routes here after Phase 0 is complete or user jumps to Phase 1.

## Prerequisites

- **Read** `docs/00-scoping/Problem-Statement.md` (auto-read for context)
- **Read** `docs/00-scoping/Stakeholder-Map.md` if it exists

Use the Problem Statement to pre-populate context and validate alignment.

## Workflow

### Step 1: Load Prior Context

1. Read `docs/00-scoping/Problem-Statement.md`
2. Extract: problem summary, scope boundaries, success criteria, known constraints
3. Use these as context for questions below

### Step 2: Gather Information (Batch Questions)

**Ask the user ALL of the following** in a single batch:

1. **Goal** — What shall the system do? (restate from problem statement or refine)
2. **Personas/Users** — Who are the system users? (with brief descriptions)
3. **Functional Requirements** — List what the system MUST do (use FR-xxx IDs):
   - Suggest initial FRs based on the Problem Statement scope
4. **Non-Functional Requirements** — Security, performance, availability requirements (NFR-xxx IDs)
5. **Data Requirements** — Data elements, retention policies, PII classification?
6. **Integration Requirements** — Upstream/downstream systems, contracts?
7. **Acceptance Criteria** — How do we know each requirement is met? (AC-xxx)
8. **Open Questions** — What is still unclear or needs research?

### Step 3: Generate Artifacts

Load templates from `references/templates.md` and generate:

**Artifact 1.1 — Requirements (Lightweight SRS)**
- File: `docs/01-requirements/Requirements.md`
- Use MUST/SHOULD/MAY language per RFC 2119
- Assign stable IDs: FR-001, NFR-001, AC-001

**Artifact 1.2 — Constraints Register**
- File: `docs/01-requirements/Constraints-Register.md`
- Extract from Problem Statement constraints + new user inputs
- Use MUST/MUST NOT language
- Include Forbidden Solutions section (F-xxx)

### Step 4: Cross-Phase Validation

Before presenting to user, validate:
- Every in-scope item from Problem Statement has at least one FR-xxx
- Success criteria from Phase 0 map to acceptance criteria
- Known constraints from Phase 0 appear in Constraints Register

**If gaps found**, warn:
```
⚠️ Validation warnings:
- Scope item "X" from Problem Statement has no matching requirement
- Constraint "Y" from Phase 0 not reflected in Constraints Register
```

### Step 5: Present & Confirm

**⚠️ MANDATORY STOPPING POINT**: Show generated content to user before writing.

Present both artifacts with a summary of:
- Total requirements count (FR + NFR)
- Validation status (pass/warnings)
- Sections left as TODO

### Step 6: Completion

After writing:
1. Confirm files written
2. Warn about skipped sections or validation gaps
3. Return control to main SKILL.md

## Output

- `docs/01-requirements/Requirements.md`
- `docs/01-requirements/Constraints-Register.md`

## Next

Return to main skill → ADR check → offer Phase 2 (Planning & Design)
