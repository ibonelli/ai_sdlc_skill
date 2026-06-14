---
name: sdlc-phase-3-architecture
description: "Phase 3 of SDLC: Data & Architecture. Locks structural decisions code must follow."
parent_skill: sdlc
---

# Phase 3 — Data & Architecture

## When to Load

Main skill routes here after Phase 2 is complete or user jumps to Phase 3.

## Prerequisites

- **Read** `docs/02-planning/High-Level-Design.md`
- **Read** `docs/02-planning/Delivery-Plan.md`
- **Read** `docs/01-requirements/Constraints-Register.md`
- **Read** any existing `docs/adr/ADR-*.md` (draft ADRs from Phase 2)

## Workflow

### Step 1: Load Prior Context

1. Read HLD and Delivery Plan from Phase 2
2. Read Constraints Register from Phase 1
3. Extract: proposed components, data flows, constraints, draft ADR decisions
4. Summarize architecture context for the user

### Step 2: Gather Information (Batch Questions)

**Ask the user ALL of the following:**

1. **Service Boundaries & Ownership** — What services/components exist? Who owns each?
2. **Interfaces** — API endpoints, events/topics, data stores?
3. **Data Entities/Events** — What are the core data objects? Definitions, owners, versioning?
4. **Data Schemas** — JSON/schema examples for each entity/event?
5. **Validation Rules** — What business rules govern data validity?
6. **Compatibility Rules** — Backward compatibility policy? Deprecation strategy?
7. **Security Model** — AuthN, AuthZ, secrets management approach?
8. **Operational Model** — Deployment strategy, scaling approach, failure modes?
9. **Draft ADR Finalization** — Review draft ADRs from Phase 2: accept, revise, or reject each?

### Step 3: Generate Artifacts

Load templates from `references/templates.md` and generate:

**Artifact 3.1 — Data Contracts**
- File: `docs/03-architecture-data/Data-Contracts.md`
- Include entity definitions, JSON schemas, validation rules, compatibility rules

**Artifact 3.2 — Architecture Overview**
- File: `docs/03-architecture-data/Architecture-Overview.md`
- Include boundaries, interfaces, security model, operational model

**Artifact 3.3 — Finalized ADRs**
- Files: `docs/adr/ADR-NNN-<title>.md`
- Update status from "Proposed" to "Accepted" for approved decisions
- Create new ADRs for decisions made in this phase

### Step 4: Cross-Phase Validation

Validate:
- Architecture addresses all NFRs (security, performance, availability)
- Data contracts cover all data requirements from Phase 1
- Constraints Register items are respected in the architecture
- All components from HLD are accounted for in Architecture Overview

**Warn about gaps.**

### Step 5: Present & Confirm

**⚠️ MANDATORY STOPPING POINT**: Present artifacts for approval.

### Step 6: Completion

After writing, return control to main SKILL.md.

## Output

- `docs/03-architecture-data/Data-Contracts.md`
- `docs/03-architecture-data/Architecture-Overview.md`
- `docs/adr/ADR-NNN-*.md` (finalized)

## Next

Return to main skill → ADR check → offer Phase 4 (Execution)
