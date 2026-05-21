# AI Workflow Artifacts

## Table of contents

- [AI Workflow Artifacts](#ai-workflow-artifacts)
  - [Table of contents](#table-of-contents)
  - [Folder structure (recommended)](#folder-structure-recommended)
  - [Phase 0 — Scoping](#phase-0--scoping)
    - [Artifact 0.1 — Problem Statement (Opportunity Brief)](#artifact-01--problem-statement-opportunity-brief)
      - [Example snippet (filled)](#example-snippet-filled)
    - [Artifact 0.2 — Stakeholder Map (optional but useful)](#artifact-02--stakeholder-map-optional-but-useful)
  - [Phase 1 — Requirements \& Constraints](#phase-1--requirements--constraints)
    - [Artifact 1.1 — Requirements (Lightweight SRS)](#artifact-11--requirements-lightweight-srs)
      - [Example snippet](#example-snippet)
    - [Artifact 1.2 — Constraints Register (AI guardrails)](#artifact-12--constraints-register-ai-guardrails)
      - [Example snippet](#example-snippet-1)
  - [Phase 2 — Planning \& Design](#phase-2--planning--design)
    - [Artifact 2.1 — Delivery Plan (Execution Plan)](#artifact-21--delivery-plan-execution-plan)
      - [Example snippet](#example-snippet-2)
    - [Artifact 2.2 — High-Level Design (HLD)](#artifact-22--high-level-design-hld)
    - [Artifact 2.3 — Logging/Observability Plan (optional, but you’ll regret skipping it)](#artifact-23--loggingobservability-plan-optional-but-youll-regret-skipping-it)
  - [Phase 3 — Data Architecture \& Detailed Architecture](#phase-3--data-architecture--detailed-architecture)
    - [Artifact 3.1 — Data Contracts](#artifact-31--data-contracts)
  - [3) Validation Rules](#3-validation-rules)
  - [4) Compatibility rules](#4-compatibility-rules)
    - [Artifact 3.3 — ADRs (Decision Records)](#artifact-33--adrs-decision-records)
      - [Example snippet](#example-snippet-3)
  - [Phase 4 — Execution](#phase-4--execution)
    - [Artifact 4.1 — Implementation Notes (PR-ready)](#artifact-41--implementation-notes-pr-ready)
    - [Artifact 4.2 — Change Log (Release notes seed)](#artifact-42--change-log-release-notes-seed)
  - [Phase 5 — Testing \& Validation](#phase-5--testing--validation)
    - [Artifact 5.1 — Test Plan](#artifact-51--test-plan)
    - [Artifact 5.2 — Traceability Matrix (requirements → tests)](#artifact-52--traceability-matrix-requirements--tests)
    - [Artifact 5.3 — Validation Report / Test Summary](#artifact-53--validation-report--test-summary)
  - [Phase 6 — Documentation \& Knowledge Capture](#phase-6--documentation--knowledge-capture)
    - [Artifact 6.1 — System Overview (for humans)](#artifact-61--system-overview-for-humans)
    - [Artifact 6.2 — Runbook (Operations)](#artifact-62--runbook-operations)
    - [Artifact 6.3 — Onboarding Notes (“Day 1 doc”)](#artifact-63--onboarding-notes-day-1-doc)
  - [The “chain” (how to use these as next-phase context)](#the-chain-how-to-use-these-as-next-phase-context)
    - [Scoping → Requirements](#scoping--requirements)
    - [Requirements → Planning/Design](#requirements--planningdesign)
    - [Planning/Design → Architecture/Data](#planningdesign--architecturedata)
    - [Architecture/Data → Execution](#architecturedata--execution)
    - [Execution → Testing](#execution--testing)
    - [Testing → Documentation](#testing--documentation)
  - [Critical guidance (this is where most teams screw up)](#critical-guidance-this-is-where-most-teams-screw-up)

Absolutely — this is a good move. If you make the **outputs explicitly Markdown artifacts**, you can:

*   chain phases cleanly (“output becomes next input”),
*   feed them to Copilot/LLMs as **structured context**,
*   and reduce “tribal knowledge” / bus factor.

Below are **ready-to-use Markdown templates** per phase, plus **example filled snippets** so you can see what “good” looks like. I’m also adding a **few optional artifacts** that are usually necessary in real delivery (otherwise “Planning” becomes hand-wavy and “Testing” becomes reactive).

## Folder structure (recommended)

Create a predictable structure so the AI (and humans) can find things:

```text
/docs
  /00-scoping
  /01-requirements
  /02-planning
  /03-architecture-data
  /04-execution
  /05-testing
  /06-documentation
  /adr
    ADR-000-template.md
```

## Phase 0 — Scoping

### Artifact 0.1 — Problem Statement (Opportunity Brief)

**Filename:** `docs/00-scoping/Problem-Statement.md`

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

#### Example snippet (filled)

```markdown
## 1) Summary (TL;DR)
- **Problem:** Password-based API authentication is failing compliance audits.
- **Impact:** Integrations with Vendor X risk being disabled.
- **Proposed outcome:** Token-based auth with audit trail and rotation.

## 4) Success Criteria
- [ ] 100% of API calls use OAuth tokens by 2026-06-15
- [ ] Rotation process documented and tested quarterly
```

### Artifact 0.2 — Stakeholder Map (optional but useful)

**Filename:** `docs/00-scoping/Stakeholder-Map.md`

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

## Phase 1 — Requirements & Constraints

### Artifact 1.1 — Requirements (Lightweight SRS)

**Filename:** `docs/01-requirements/Requirements.md`

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

#### Example snippet

```markdown
## 3) Functional Requirements
- **FR-001:** The system MUST obtain `access_token` and `id_token` from Identity Provider within 2 seconds.
- **FR-002:** The system MUST log token refresh events with correlation ID.

## 4) NFRs
- **NFR-001 (Security):** Tokens MUST NOT be written to disk in plaintext.
- **NFR-002 (Availability):** Service MUST tolerate IdP transient failures via retries/backoff.
```

### Artifact 1.2 — Constraints Register (AI guardrails)

**Filename:** `docs/01-requirements/Constraints-Register.md`

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

#### Example snippet

```markdown
## Constraints
- **C-002 (Language):** MUST be Bash + curl + jq only (no Python allowed in runtime container).
- **C-004 (Data Boundaries):** MUST call Auth service; direct database access is forbidden.

## Forbidden Solutions
- **F-001:** Do NOT persist tokens in files or logs.
```

## Phase 2 — Planning & Design

### Artifact 2.1 — Delivery Plan (Execution Plan)

**Filename:** `docs/02-planning/Delivery-Plan.md`

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

#### Example snippet

```markdown
## 6) Rollout strategy
- Feature flag `auth_v2_enabled`
- Enable in DEV → QA → PROD
- Rollback: disable flag; revert to v1 auth path
```

### Artifact 2.2 — High-Level Design (HLD)

**Filename:** `docs/02-planning/High-Level-Design.md`

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

### Artifact 2.3 — Logging/Observability Plan (optional, but you’ll regret skipping it)

**Filename:** `docs/02-planning/Observability-Plan.md`

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

## Phase 3 — Data Architecture & Detailed Architecture

### Artifact 3.1 — Data Contracts

**Filename:** `docs/03-architecture-data/Data-Contracts.md`

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
````

## 3) Validation Rules

*   Rule 1:
*   Rule 2:

## 4) Compatibility rules

*   Backward compatibility:
*   Deprecation policy:

````

---

### Artifact 3.2 — Architecture Overview (LLD-lite)
**Filename:** `docs/03-architecture-data/Architecture-Overview.md`

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
````

### Artifact 3.3 — ADRs (Decision Records)

**Filename:** `docs/adr/ADR-001-<title>.md`

```markdown
# ADR-001: <Decision title>

- **Status:** Proposed | Accepted | Superseded
- **Date:** YYYY-MM-DD
- **Owners:** <names>

## Context
What problem are we solving? What constraints force this decision?

## Decision
State the decision clearly.

## Consequences
### Positive
- 
### Negative
- 

## Alternatives considered
- Option A:
- Option B:

## Links
- Related requirements:
- Related design docs:
- PRs/issues:
```

#### Example snippet

```markdown
## Decision
We will use OAuth2 client credentials flow via the corporate IdP.

## Consequences
### Positive
- Centralized token governance and rotation
### Negative
- Requires IdP availability; must implement backoff and caching
```

## Phase 4 — Execution

Execution artifacts are not “docs only” — the primary output is code. But you still need **traceability documents**, otherwise your pipeline breaks.

### Artifact 4.1 — Implementation Notes (PR-ready)

**Filename:** `docs/04-execution/Implementation-Notes.md`

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

### Artifact 4.2 — Change Log (Release notes seed)

**Filename:** `docs/04-execution/Change-Log.md`

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

## Phase 5 — Testing & Validation

### Artifact 5.1 — Test Plan

**Filename:** `docs/05-testing/Test-Plan.md`

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

### Artifact 5.2 — Traceability Matrix (requirements → tests)

This is **super valuable** when working with AI because it forces alignment.

**Filename:** `docs/05-testing/Traceability.md`

```markdown
# Traceability — Requirements to Tests

| Requirement ID | Description | Test Case ID(s) | Status |
|---|---|---|---|
| FR-001 |  | TC-001 | Planned |
| NFR-001 |  | TC-005 | Planned |
```

### Artifact 5.3 — Validation Report / Test Summary

**Filename:** `docs/05-testing/Validation-Report.md`

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

## Phase 6 — Documentation & Knowledge Capture

### Artifact 6.1 — System Overview (for humans)

**Filename:** `docs/06-documentation/System-Overview.md`

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

### Artifact 6.2 — Runbook (Operations)

**Filename:** `docs/06-documentation/Runbook.md`

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

### Recover from IdP outage
Steps...

## Post-incident checklist
- [ ] Root cause documented
- [ ] Preventative action created
```

### Artifact 6.3 — Onboarding Notes (“Day 1 doc”)

**Filename:** `docs/06-documentation/Onboarding.md`

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

## The “chain” (how to use these as next-phase context)

Here’s the **minimum set** of docs you should pass forward:

### Scoping → Requirements

*   `Problem-Statement.md`
*   `Stakeholder-Map.md` (optional)

### Requirements → Planning/Design

*   `Requirements.md`
*   `Constraints-Register.md`

### Planning/Design → Architecture/Data

*   `Delivery-Plan.md`
*   `High-Level-Design.md`
*   Draft ADRs

### Architecture/Data → Execution

*   `Architecture-Overview.md`
*   `Data-Contracts.md`
*   Accepted ADRs

### Execution → Testing

*   `Implementation-Notes.md`
*   `Change-Log.md`

### Testing → Documentation

*   `Validation-Report.md`
*   `Traceability.md`

## Critical guidance (this is where most teams screw up)

1.  **Don’t over-document.** If these templates become “paperwork”, people will bypass them. Keep them short and enforced via PR checks.
2.  **Constraints Register is the AI safety rail.** If there’s only ONE doc you ensure is always current, make it that.
3.  **ADRs are mandatory for irreversible decisions.** Otherwise you accumulate architectural drift and future engineers (or AI) will unknowingly break the system.
