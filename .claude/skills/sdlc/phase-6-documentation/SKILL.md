---
name: sdlc-phase-6-documentation
description: "Phase 6 of SDLC: Documentation & Knowledge Capture. Makes work transferable and reusable."
parent_skill: sdlc
---

# Phase 6 — Documentation & Knowledge Capture

## When to Load

Main skill routes here after Phase 5 is complete or user jumps to Phase 6.

## Prerequisites

- **Read** `docs/05-testing/Validation-Report.md`
- **Read** `docs/05-testing/Traceability.md`
- **Read** `docs/03-architecture-data/Architecture-Overview.md`
- **Read** all `docs/adr/ADR-*.md`
- **Read** `docs/04-execution/Implementation-Notes.md`

## Workflow

### Step 1: Load Prior Context

1. Read all prior phase artifacts
2. Extract: architecture summary, operational model, ADR decisions, implementation details
3. Synthesize into documentation context

### Step 2: Gather Information (Batch Questions)

**Ask the user ALL of the following:**

1. **System Purpose** — One-paragraph description of what this system does
2. **Architecture Summary** — Key components and data flow (simplify from Phase 3)
3. **How to Operate** — Start/stop procedures, monitoring approach, common incidents
4. **Known Failure Modes** — What can fail, how is it detected, how to remediate?
5. **Ownership** — Team responsible, on-call rotation?
6. **SLOs/SLIs** — Service level objectives and indicators?
7. **Alerts** — What alerts exist? What each means, immediate action, escalation path?
8. **Common Operational Tasks** — Credential rotation, recovery procedures, etc.?
9. **Repository Map** — How is the repo organized? Key directories?
10. **How to Run Locally** — Steps for a new developer?
11. **How to Deploy** — Deployment process?

### Step 3: Generate Artifacts

Load templates from `references/templates.md` and generate:

**Artifact 6.1 — System Overview**
- File: `docs/06-documentation/System-Overview.md`
- Synthesize from architecture + implementation + testing artifacts

**Artifact 6.2 — Runbook**
- File: `docs/06-documentation/Runbook.md`
- Include SLOs, alerts, common tasks, post-incident checklist

**Artifact 6.3 — Onboarding Notes**
- File: `docs/06-documentation/Onboarding.md`
- Repository map, local setup, deployment, key decisions (link to ADR index)

### Step 4: Cross-Phase Validation

Validate:
- System Overview is consistent with Architecture Overview from Phase 3
- All ADRs are referenced in the Onboarding doc
- Failure modes mentioned in test reports appear in the Runbook
- Operational model from Architecture Overview is reflected in Runbook

**Warn about gaps.**

### Step 5: Present & Confirm

**⚠️ MANDATORY STOPPING POINT**: Present artifacts for approval.

### Step 6: Completion

After writing:
1. Confirm all files written
2. Present final project summary:
```
SDLC Complete! Artifacts generated:
- Phase 0: Problem-Statement.md, Stakeholder-Map.md
- Phase 1: Requirements.md, Constraints-Register.md
- Phase 2: Delivery-Plan.md, High-Level-Design.md, Observability-Plan.md
- Phase 3: Data-Contracts.md, Architecture-Overview.md, ADRs
- Phase 4: Implementation-Notes.md, Change-Log.md
- Phase 5: Test-Plan.md, Traceability.md, Validation-Report.md
- Phase 6: System-Overview.md, Runbook.md, Onboarding.md
```
3. Remind: "Keep the Constraints Register current — it's your AI safety rail."

## Output

- `docs/06-documentation/System-Overview.md`
- `docs/06-documentation/Runbook.md`
- `docs/06-documentation/Onboarding.md`

## Next

This is the final phase. SDLC cycle complete.
