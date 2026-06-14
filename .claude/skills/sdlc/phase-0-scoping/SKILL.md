---
name: sdlc-phase-0-scoping
description: "Phase 0 of SDLC: Scoping. Decides whether and why to do a project."
parent_skill: sdlc
---

# Phase 0 — Scoping

## When to Load

Main skill routes here when user selects Phase 0 or starts a new project.

## Prerequisites

- None (this is the first phase)

## Workflow

### Step 1: Create docs folder structure

If `docs/` doesn't exist, create:
```
docs/00-scoping/
docs/01-requirements/
docs/02-planning/
docs/03-architecture-data/
docs/04-execution/
docs/05-testing/
docs/06-documentation/
docs/adr/
```

### Step 1b: Apply Active Modes

**Auto-fill mode** — if active, scan the repository before asking any questions:

Scan targets: `README*`, `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `git log --oneline -20`, any files in `docs/`.

After scanning, propose answers for every question below with evidence citations:
```
Project name: "pelis-feed" (from package.json "name" field)
Problem: Automated filtering of movie RSS feeds (from README paragraph 1)
[UNCLEAR — please provide]: Decision Needed
```
Present the full proposed list and ask the user to confirm or correct specific items. Only ask follow-up questions for items marked `[UNCLEAR]`.

**Personal project mode** — if active, apply before gathering information:

Load defaults from `references/personal-project-preset.md`. Pre-fill without asking:
- Stakeholders → Sole developer (you)
- Compliance, budget, decision gate → see preset

Skip from the question batch: **Stakeholders** (6), **Decision Needed** (12).

Ask only: Project name, Problem, Impact, Proposed Outcome, In Scope, Out of Scope, Success Criteria, Known technical constraints, Risks.

### Step 2: Gather Information (Batch Questions)

**Ask the user ALL of the following** in a single batch using `ask_user_question`:

1. **Project/Feature Name** — What is this project or feature called?
2. **Problem** — What problem are we solving? (one sentence)
3. **Impact** — Who is impacted and how?
4. **Proposed Outcome** — What does success look like?
5. **Background/Context** — Current state, why now?
6. **Stakeholders** — Business owner, technical owner, users?
7. **In Scope** — What is included?
8. **Out of Scope** — What is explicitly excluded?
9. **Success Criteria** — Measurable metrics (baseline → target)?
10. **Known Constraints** — Compliance, security, availability, budget, tech constraints?
11. **Risks & Unknowns** — What could go wrong? What don't we know?
12. **Decision Needed** — What approval or decision is required to proceed?

### Step 3: Generate Artifacts

Using the answers, generate two artifacts by loading templates from `references/templates.md`:

**Artifact 0.1 — Problem Statement**
- File: `docs/00-scoping/Problem-Statement.md`
- Fill all sections from the template with user answers
- For any section the user didn't address, leave placeholder with `<!-- TODO: Fill this section -->`

**Artifact 0.2 — Stakeholder Map** (if stakeholder info provided)
- File: `docs/00-scoping/Stakeholder-Map.md`
- Fill Decision Makers, Contributors, Consulted, Informed sections

### Step 4: Present & Confirm

**⚠️ MANDATORY STOPPING POINT**: Show generated content to user before writing.

Present:
```
I've generated the following artifacts for Phase 0:
1. Problem-Statement.md — [summary]
2. Stakeholder-Map.md — [summary]

Sections left incomplete: [list any TODO sections]

Write these files to docs/00-scoping/? (Yes / Modify / Skip)
```

**If user approves:** Write files to disk.
**If user wants modifications:** Ask what to change, regenerate.

### Step 5: Completion

After writing:
1. Confirm files written successfully
2. Warn about any skipped sections: "Note: X sections were left as TODO — you can fill these later."
3. Return control to main SKILL.md for ADR check + next phase offer

## Output

- `docs/00-scoping/Problem-Statement.md`
- `docs/00-scoping/Stakeholder-Map.md` (optional)

## Next

Return to main skill → ADR check → offer Phase 1 (Requirements & Constraints)
