---
name: sdlc-phase-2-planning
description: "Phase 2 of SDLC: Planning & Design. Decides how to deliver."
parent_skill: sdlc
---

# Phase 2 — Planning & Design

## When to Load

Main skill routes here after Phase 1 is complete or user jumps to Phase 2.

## Prerequisites

- **Read** `docs/01-requirements/Requirements.md`
- **Read** `docs/01-requirements/Constraints-Register.md`
- **Read** `docs/00-scoping/Problem-Statement.md` (for scope context)

## Workflow

### Step 1: Load Prior Context

1. Read Requirements and Constraints Register
2. Extract: all FR-xxx, NFR-xxx, constraints (C-xxx), forbidden solutions (F-xxx)
3. Summarize scope and constraints for the user as context

### Step 1b: Apply Active Modes

**Auto-fill mode** — if active, scan the repository before asking any questions:

Scan targets: `.github/` (issues, milestones, project boards), `TODO`, `ROADMAP`, `CHANGELOG*`, CI/CD configs (`.github/workflows/`, `Makefile`, `.circleci/`, `Jenkinsfile`), existing `docs/02-planning/`.

After scanning, propose:
- Work breakdown inferred from open GitHub issues or TODO items
- Rollout strategy inferred from CI/CD pipeline shape
- Observability needs inferred from existing metrics/logging code

Mark anything that can't be inferred as `[UNCLEAR — please provide]`. Present proposed answers and ask the user to confirm or correct specific items only.

**Personal project mode** — if active, apply before gathering information:

Load defaults from `references/personal-project-preset.md`. Pre-fill without asking:
- Rollout strategy → Direct deploy (no feature flags)
- Milestones owners → You (sole developer)

Skip from the question batch:
- **Dependencies** (4) — external teams/vendors/approvals only; still ask about environment deps if present.
- **Rollout Strategy** (6) — pre-filled as direct deploy; only ask if CI/CD pipeline suggests otherwise.

Ask only: Scope Recap, Work Breakdown, Risks & Mitigations, Definition of Done, High-Level Design, Alternatives Considered, Observability Needs (optional).

### Step 2: Gather Information (Batch Questions)

**Ask the user ALL of the following:**

1. **Scope Recap** — Confirm in-scope/out-of-scope (or refine from Phase 0)
2. **Milestones** — What are the key deliverables and who owns them?
3. **Work Breakdown** — Break into Epics → Stories (suggest based on FRs)
4. **Dependencies** — External teams, vendors, environments, approvals needed?
5. **Risks & Mitigations** — What could block delivery? How to mitigate?
6. **Rollout Strategy** — Feature flags? Phased rollout? Rollback plan?
7. **Definition of Done** — What must be true for this to be "done"?
8. **High-Level Design** — System context, proposed solution components, data flow?
9. **Alternatives Considered** — What other approaches were evaluated? Why rejected?
10. **Observability Needs** — Key metrics, logs, alerts, dashboards needed?

### Step 3: Generate Artifacts

Load templates from `references/templates.md` and generate:

**Artifact 2.1 — Delivery Plan**
- File: `docs/02-planning/Delivery-Plan.md`
- Map work breakdown to requirements (traceability)

**Artifact 2.2 — High-Level Design (HLD)**
- File: `docs/02-planning/High-Level-Design.md`
- Reference constraints from Constraints Register
- Link to ADR drafts if decisions are made

**Artifact 2.3 — Observability Plan** (if observability info provided)
- File: `docs/02-planning/Observability-Plan.md`

### Step 4: Cross-Phase Validation

Validate:
- Every FR-xxx appears in at least one work breakdown story
- Constraints (C-xxx) are acknowledged in the HLD
- Rollout strategy addresses availability NFRs

**Warn about gaps.**

### Step 5: Present & Confirm

**⚠️ MANDATORY STOPPING POINT**: Present artifacts for approval.

### Step 6: Completion

After writing, return control to main SKILL.md.

## Output

- `docs/02-planning/Delivery-Plan.md`
- `docs/02-planning/High-Level-Design.md`
- `docs/02-planning/Observability-Plan.md` (optional)

## Next

Return to main skill → ADR check → offer Phase 3 (Data & Architecture)
