---
name: sdlc
description: "AI-assisted Software Development Life Cycle. Guides users through 7 SDLC phases: scoping, requirements, planning, architecture, execution, testing, and documentation. Use when starting a new software project, planning features, creating project documentation, defining requirements, or managing the full development lifecycle. Triggers: SDLC, project planning, scoping, requirements, architecture, delivery plan, test plan."
---

# SDLC AI Assistance

## When to Use

- Starting a new software development project
- Planning a feature or system change
- Generating SDLC documentation (requirements, design, test plans)
- Resuming work on an in-progress project with existing artifacts

## Workflow

### Step 1: Detect Project Progress

**Actions:**

1. **Scan** the `docs/` folder in the project root for existing phase artifacts:

```
docs/00-scoping/Problem-Statement.md     → Phase 0
docs/01-requirements/Requirements.md     → Phase 1
docs/02-planning/Delivery-Plan.md        → Phase 2
docs/03-architecture-data/Data-Contracts.md → Phase 3
docs/04-execution/Implementation-Notes.md  → Phase 4
docs/05-testing/Test-Plan.md             → Phase 5
docs/06-documentation/System-Overview.md  → Phase 6
docs/adr/ADR-*.md                        → ADRs (any phase)
```

2. **Build progress map** — mark each phase as: Complete, Partial, or Not Started.

3. **Read** `references/artifact-chain.md` for validation rules.

### Step 2: Present Options to User

**⚠️ MANDATORY STOPPING POINT**: Present the progress status and ask what to do.

**If no artifacts exist:**
```
No SDLC artifacts found. Options:
1. Start a new project from Phase 0 (Scoping)
2. Jump to a specific phase
3. Auto-fill from repository — I'll read the codebase and propose answers
4. Personal project mode — Simplified questions, solo-developer defaults pre-filled
5. Auto-fill + Personal project — Both combined
```

**If artifacts exist:**
```
Project progress detected:
- Phase 0 (Scoping): ✅ Complete
- Phase 1 (Requirements): ⚠️ Partial
- Phase 2 (Planning): ❌ Not started
...

Options:
1. Continue from next incomplete phase (Phase X)
2. Jump to a specific phase
3. Re-do a completed phase
4. Auto-fill from repository — I'll read the codebase and propose answers
5. Personal project mode — Simplified questions, solo-developer defaults pre-filled
6. Auto-fill + Personal project — Both combined
```

**Mode definitions (carry these forward into every phase sub-skill):**

- **Auto-fill mode**: Before asking any questions, scan the repository for evidence and propose inferred answers. User confirms or corrects rather than answering from scratch.
- **Personal project mode**: Pre-fill solo/hobby defaults (stakeholders, compliance, team, on-call, SLA) and skip questions that don't apply to a solo developer. Load defaults from `references/personal-project-preset.md`.
- These modes are independent and can be combined.

### Step 3: Route to Phase Sub-Skill

**Before routing**: note the active mode(s) as context so the phase sub-skill applies them correctly.

Based on user selection, load the appropriate sub-skill:

| Phase | Load |
|-------|------|
| Phase 0 — Scoping | `phase-0-scoping/SKILL.md` |
| Phase 1 — Requirements & Constraints | `phase-1-requirements/SKILL.md` |
| Phase 2 — Planning & Design | `phase-2-planning/SKILL.md` |
| Phase 3 — Data & Architecture | `phase-3-architecture/SKILL.md` |
| Phase 4 — Execution | `phase-4-execution/SKILL.md` |
| Phase 5 — Testing & Validation | `phase-5-testing/SKILL.md` |
| Phase 6 — Documentation & Knowledge Capture | `phase-6-documentation/SKILL.md` |

### Step 4: Post-Phase ADR Check

After ANY phase sub-skill completes:

1. **Ask** the user: "Were any significant or irreversible decisions made during this phase that should be recorded as an ADR?"
2. **If yes**: Load `references/adr-template.md`, ask for decision details, write to `docs/adr/ADR-NNN-<title>.md`
3. **If no**: Proceed to next phase offer

### Step 5: Offer Continuation

After phase completion + ADR check:
- Ask if user wants to continue to the next phase or stop here

## Folder Structure Created

When starting a new project, create:

```
docs/
  00-scoping/
  01-requirements/
  02-planning/
  03-architecture-data/
  04-execution/
  05-testing/
  06-documentation/
  adr/
```

## Stopping Points

- ✋ After progress detection (Step 2) — user picks phase
- ✋ After each phase completes — ADR check + continuation choice
- ✋ Within each phase sub-skill — approval before writing files

## Output

- Markdown artifacts written to `docs/` following the fixed folder structure
- ADRs in `docs/adr/` with sequential numbering
- Cross-phase validation warnings surfaced when inconsistencies detected

## Key Principles

- AI is a "junior engineer with perfect recall and poor judgment" — user approves all artifacts
- Constraints Register (`docs/01-requirements/Constraints-Register.md`) is the single most important document
- If rules are not explicit, they WILL be violated
- Keep artifacts short and useful — warn about skipped sections but don't block progress
