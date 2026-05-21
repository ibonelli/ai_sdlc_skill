---
name: sdlc-phase-4-execution
description: "Phase 4 of SDLC: Execution. Build only what was agreed."
parent_skill: sdlc
---

# Phase 4 — Execution

## When to Load

Main skill routes here after Phase 3 is complete or user jumps to Phase 4.

## Prerequisites

- **Read** `docs/03-architecture-data/Architecture-Overview.md`
- **Read** `docs/03-architecture-data/Data-Contracts.md`
- **Read** `docs/01-requirements/Constraints-Register.md`
- **Read** all accepted `docs/adr/ADR-*.md`

## Workflow

### Step 1: Load Prior Context

1. Read Architecture Overview and Data Contracts
2. Read Constraints Register (this is the AI safety rail during execution)
3. Read all accepted ADRs
4. Summarize: what must be built, architectural constraints, forbidden approaches

### Step 2: Gather Information (Batch Questions)

**Ask the user ALL of the following:**

1. **Scope Implemented** — What was actually built in this iteration?
2. **Files Touched** — List of files created/modified (paths)
3. **Key Decisions** — Any implementation decisions? Link to ADRs if applicable
4. **Edge Cases Handled** — What edge cases were addressed?
5. **Known Limitations** — What doesn't work yet or has caveats?
6. **Migration Steps** — Any database migrations, config changes, or data transformations needed?
7. **How to Test Locally** — Steps another dev would follow to verify

### Step 3: Generate Artifacts

Load templates from `references/templates.md` and generate:

**Artifact 4.1 — Implementation Notes**
- File: `docs/04-execution/Implementation-Notes.md`
- Link to relevant ADRs
- Document edge cases and known limitations

**Artifact 4.2 — Change Log**
- File: `docs/04-execution/Change-Log.md`
- Categorize: Added, Changed, Fixed, Security
- If Change-Log.md already exists, append new entries under "Unreleased"

### Step 4: Cross-Phase Validation

Validate:
- Implementation scope aligns with Delivery Plan work breakdown
- No forbidden solutions (F-xxx) from Constraints Register were used
- Architecture boundaries from Phase 3 are respected
- Any new decisions are flagged for potential ADRs

**Warn if deviations detected:**
```
⚠️ Validation warnings:
- Implementation mentions "direct DB access" but C-004 forbids this
- New technology X not covered by any ADR — consider creating one
```

### Step 5: Present & Confirm

**⚠️ MANDATORY STOPPING POINT**: Present artifacts for approval.

### Step 6: Completion

After writing, return control to main SKILL.md.

## Output

- `docs/04-execution/Implementation-Notes.md`
- `docs/04-execution/Change-Log.md`

## Important

If execution requires a change in architecture → a **new ADR is mandatory**, not an undocumented deviation. Flag this to the user.

## Next

Return to main skill → ADR check → offer Phase 5 (Testing & Validation)
