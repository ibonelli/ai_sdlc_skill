# Artifact Templates

All templates for SDLC phase artifacts. Load this file when generating artifacts.

---

## Phase 0 — Scoping

### Problem Statement

```markdown
# Problem Statement — <Project / Feature Name>

## 1) Summary (TL;DR)
- **Problem:** <one sentence>
- **Impact:** <who is impacted and how>
- **Proposed outcome:** <what success looks like>

## 2) Background / Context
- Current state:
- Why now:
- Stakeholders:
  - Business owner:
  - Technical owner:
  - Users:

## 3) Scope
### In Scope
- 
### Out of Scope
- 

## 4) Success Criteria (Measurable)
- [ ] Metric 1: <baseline → target>
- [ ] Metric 2:

## 5) Constraints (Known)
- Compliance:
- Security:
- Availability:
- Budget / timeline:
- Tech constraints (existing platforms, languages, integrations):

## 6) Risks & Unknowns
- Risk:
- Unknown:
- Assumption:

## 7) Decision Needed
- Approve / reject / revise scope
- Target date for decision:
```

### Stakeholder Map

```markdown
# Stakeholder Map — <Project>

## Decision Makers
- <Name> — <role>

## Contributors
- <Name> — <role>

## Consulted (SMEs)
- <Name> — <domain>

## Informed
- <Name> — <group>

## Communication cadence
- Weekly sync:
- Status channel:
- Escalation path:
```

---

## Phase 1 — Requirements & Constraints

### Requirements (Lightweight SRS)

```markdown
# Requirements — <Project / Feature>

## 1) Goal
- The system shall...

## 2) Personas / Users
- Persona A:
- Persona B:

## 3) Functional Requirements
> Use MUST language and stable IDs.

- **FR-001:** The system MUST ...
- **FR-002:** The system MUST ...

## 4) Non-Functional Requirements (NFRs)
- **NFR-001 (Security):** MUST ...
- **NFR-002 (Performance):** MUST ...
- **NFR-003 (Availability):** MUST ...

## 5) Data Requirements
- Data elements:
- Retention:
- PII classification:

## 6) Integration Requirements
- Upstream:
- Downstream:
- Contracts:

## 7) Acceptance Criteria
- AC-001:
- AC-002:

## 8) Open Questions
- Q-001:
- Q-002:
```

### Constraints Register

```markdown
# Constraints Register — <Project>

## Purpose
List constraints that are non-negotiable. This is a primary AI context document.

## Constraints
- **C-001 (Platform):** MUST run on <platform>.
- **C-002 (Language):** MUST use <language>.
- **C-003 (Security):** MUST comply with <policy>.
- **C-004 (Data Boundaries):** MUST NOT access <resource> directly.

## Forbidden Solutions (Explicit)
- **F-001:** Do NOT use <tech>.
- **F-002:** Do NOT store secrets in <place>.

## Notes / Rationale
- Why these exist:
```

---

## Phase 2 — Planning & Design

### Delivery Plan

```markdown
# Delivery Plan — <Project>

## 1) Scope recap
- In scope:
- Out of scope:

## 2) Milestones
| Milestone | Deliverable | Owner | Target date |
|---|---|---|---|

## 3) Work Breakdown (Epics → Stories)
- Epic 1:
  - Story 1:
  - Story 2:

## 4) Dependencies
- External teams:
- Vendors:
- Environments:
- Approvals:

## 5) Risks & Mitigations
- Risk:
- Mitigation:

## 6) Rollout strategy
- Feature flags:
- Phased rollout:
- Rollback plan:

## 7) Definition of Done (DoD)
- [ ] Code merged
- [ ] Tests passing
- [ ] Docs updated
- [ ] Monitoring added
```

### High-Level Design (HLD)

```markdown
# High-Level Design (HLD) — <Project>

## 1) Overview
- What are we building:
- Why:

## 2) System Context
- Actors:
- External systems:
- Trust boundaries:

## 3) Proposed Solution (Big picture)
- Components:
- Responsibilities:
- Data flow (describe in steps):

## 4) Alternatives considered
- Option A:
- Option B:
- Why rejected:

## 5) Key Decisions
- Link to ADRs (draft/accepted):
  - ADR-001:
  - ADR-002:

## 6) Non-functional impacts
- Security:
- Performance:
- Operability:
```

### Observability Plan

```markdown
# Observability Plan — <Project>

## Metrics
- M-001:
- M-002:

## Logs
- Required fields:
- Correlation ID strategy:

## Alerts
- A-001:
- A-002:

## Dashboards
- D-001:
```

---

## Phase 3 — Data & Architecture

### Data Contracts

````markdown
# Data Contracts — <Project>

## 1) Entities / Events
- Entity/Event name:
  - Definition:
  - Owner:
  - Versioning:

## 2) Schema (JSON examples)
### <Entity/Event> v1
```json
{
  "field": "type",
  "example": "value"
}
```

## 3) Validation Rules
- Rule 1:
- Rule 2:

## 4) Compatibility rules
- Backward compatibility:
- Deprecation policy:
````

### Architecture Overview

```markdown
# Architecture Overview — <Project>

## 1) Boundaries & Ownership
- Service A owns:
- Service B owns:

## 2) Interfaces
- API endpoints:
- Events/topics:
- Data stores:

## 3) Security Model
- AuthN:
- AuthZ:
- Secrets management:

## 4) Operational Model
- Deployment:
- Scaling:
- Failure modes:
```

---

## Phase 4 — Execution

### Implementation Notes

```markdown
# Implementation Notes — <Project / Feature>

## Scope implemented
- 

## Files touched
- `path/file1`
- `path/file2`

## Key decisions (links to ADRs)
- ADR-001:

## Edge cases handled
- 

## Known limitations
- 

## Migration steps (if needed)
- 

## How to test locally
- Step 1:
- Step 2:
```

### Change Log

```markdown
# Change Log — <Project>

## Unreleased
- Added:
- Changed:
- Fixed:
- Security:

## YYYY-MM-DD
- 
```

---

## Phase 5 — Testing & Validation

### Test Plan

```markdown
# Test Plan — <Project>

## Scope of testing
- In scope:
- Out of scope:

## Test types
- Unit:
- Integration:
- Contract:
- Performance:
- Security:

## Environments
- DEV:
- QA:
- PROD:

## Entry criteria
- 

## Exit criteria
- 

## Test cases (high-level)
- TC-001:
- TC-002:
```

### Traceability Matrix

```markdown
# Traceability — Requirements to Tests

| Requirement ID | Description | Test Case ID(s) | Status |
|---|---|---|---|
| FR-001 |  | TC-001 | Planned |
| NFR-001 |  | TC-005 | Planned |
```

### Validation Report

```markdown
# Validation Report — <Project>

## Test execution summary
- Date:
- Environment:
- Build version:

## Results
- Passed:
- Failed:
- Blocked:

## Defects found
- DEF-001:
- DEF-002:

## Risk acceptance (if any)
- What risk:
- Approved by:
- Expiry date:
```

---

## Phase 6 — Documentation & Knowledge Capture

### System Overview

```markdown
# System Overview — <Project>

## What this system does
- 

## Architecture summary
- Components:
- Data flow:

## How to operate it
- Start/stop:
- Monitoring:
- Common incidents:

## Known failure modes
- Failure mode:
- Detection:
- Remediation:

## Ownership
- Team:
- On-call:
```

### Runbook

```markdown
# Runbook — <System>

## SLOs / SLIs
- 

## Alerts
- Alert name:
  - Meaning:
  - Immediate action:
  - Escalation:

## Common tasks
### Rotate credentials
Steps...

### Recover from <failure>
Steps...

## Post-incident checklist
- [ ] Root cause documented
- [ ] Preventative action created
```

### Onboarding Notes

```markdown
# Onboarding — <Project>

## Repository map
- `/src`:
- `/docs`:
- `/deploy`:

## How to run locally
- 

## How to deploy
- 

## Key decisions
- Link to ADR index:
```
