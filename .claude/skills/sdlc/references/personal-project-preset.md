# Personal Project Preset

Load this file when **personal project mode** is active. It defines the pre-filled values and the reduced question set for every phase.

## Core principle

Treat "you" (the developer) as simultaneously: the business owner, technical owner, sole user, and only stakeholder. There is no team, no compliance requirement, no SLA, and no budget beyond personal time.

---

## Pre-filled Values (apply to all phases)

| Field | Pre-filled value |
|-------|-----------------|
| Stakeholders — Decision Makers | Sole developer (you) |
| Stakeholders — Contributors | N/A |
| Stakeholders — Consulted | N/A |
| Stakeholders — Informed | N/A |
| Communication cadence | N/A (solo project) |
| Compliance constraints | None |
| Budget | Personal time only (no financial budget) |
| On-call / team | Developer (you) |
| Availability SLA | Best-effort — no formal SLA |
| Rollout strategy | Direct deploy (no feature flags required) |
| Deployment approvals | N/A |
| External team dependencies | None |

---

## Per-Phase Reduced Question Sets

### Phase 0 — Scoping

**Skip entirely (pre-filled above):**
- Stakeholders
- Decision Needed / approval gate
- Target date for decision

**Ask only:**
1. Project name
2. Problem — what problem are you solving?
3. Proposed outcome — what does success look like?
4. In scope / out of scope
5. Success criteria (measurable)
6. Known technical constraints or risks

### Phase 1 — Requirements & Constraints

**Skip entirely (pre-filled above):**
- Integration Requirements *(ask only if the project clearly integrates with external systems)*
- PII classification *(ask only if personal data is involved)*

**Ask only:**
1. Goal — what shall the system do?
2. Functional requirements (FR-xxx) — list what it MUST do
3. Non-functional requirements — performance, security if relevant
4. Acceptance criteria — how will you know each requirement is met?
5. Open questions

### Phase 2 — Planning & Design

**Skip entirely (pre-filled above):**
- External team dependencies / approvals
- Rollout strategy (assume direct deploy)
- Milestones with owners (you own all of them)
- Communication / status updates

**Ask only:**
1. Work breakdown — what are the main tasks?
2. Risks — what could block or slow you?
3. High-level design — key components and data flow
4. Alternatives considered
5. Observability needs (optional)

### Phase 3 — Data & Architecture

**Skip entirely (pre-filled above):**
- Service boundaries & ownership (single owner assumed)
- Multi-team interface contracts

**Ask only:**
1. Data entities / events — what are the core data objects?
2. Data schemas — rough JSON/schema examples
3. Validation rules
4. Security model — authentication approach (even if simple)
5. Operational model — how will it run, how will failures surface?
6. Draft ADR finalization (if any from Phase 2)

### Phase 4 — Execution

No changes — all questions are relevant for solo developers. Run standard Phase 4 workflow.

### Phase 5 — Testing & Validation

**Simplify:**
- Test environments: collapse to "local" and optionally "production/deployed"

**Ask only:**
1. Test scope — what is in/out of testing scope?
2. Test types — which apply (unit, integration, manual)?
3. Entry / exit criteria
4. Test cases per requirement (FR-xxx, NFR-xxx)
5. Known risky areas

**Skip:**
- Formal environment matrix (DEV/QA/PROD)
- External QA approvals

### Phase 6 — Documentation & Knowledge Capture

**Skip entirely (pre-filled above):**
- Team ownership / on-call rotation
- SLOs / SLIs (best-effort, no formal targets)
- Alert escalation paths (escalation = you)
- Communication cadence

**Ask only:**
1. System purpose — one-paragraph description
2. How to operate it — start/stop, how you monitor it
3. Known failure modes and how to detect/fix them
4. Repository map — how is the repo organized?
5. How to run locally
6. How to deploy

---

## Artifact adjustments

When generating artifacts in personal project mode, omit or collapse sections that have no content:
- Stakeholder Map: generate a minimal one-liner ("Sole developer") rather than skipping the file entirely
- Runbook: omit the "SLOs/SLIs", "escalation", and "on-call" sections
- Onboarding: omit "team contacts" and "communication cadence"

Do not leave empty section headers — remove the section entirely if it has no content.
