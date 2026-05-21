# ADR Template

Use this template when creating Architecture Decision Records. ADRs can be created in any phase when significant or irreversible decisions are made.

## Numbering Convention

- Sequential: ADR-001, ADR-002, ADR-003...
- Filename: `docs/adr/ADR-NNN-<short-title>.md` (e.g., `ADR-001-use-oauth2.md`)

## Status Lifecycle

```
Proposed → Accepted → [Superseded by ADR-NNN]
                    → [Deprecated]
```

## Template

```markdown
# ADR-NNN: <Decision title>

- **Status:** Proposed | Accepted | Superseded | Deprecated
- **Date:** YYYY-MM-DD
- **Owners:** <names>

## Context

What problem are we solving? What constraints force this decision?

## Decision

State the decision clearly in one or two sentences.

## Consequences

### Positive
- 

### Negative
- 

## Alternatives considered

| Option | Pros | Cons | Why rejected |
|--------|------|------|-------------|
| Option A | | | |
| Option B | | | |

## Links
- Related requirements: FR-xxx, NFR-xxx
- Related design docs:
- PRs/issues:
```

## When to Create an ADR

Proactively suggest an ADR when ANY of these occur:

1. **Technology choice** — Picking a framework, library, or platform
2. **Architecture pattern** — Choosing microservices vs monolith, event-driven vs sync, etc.
3. **Security approach** — AuthN/AuthZ method, encryption strategy
4. **Data model choice** — Schema design that's hard to change later
5. **Integration approach** — How to connect to external systems
6. **Trade-off decision** — Explicitly trading one quality for another (e.g., consistency for availability)
7. **Constraint acceptance** — Accepting a limitation that affects future work

## ADR Quality Checklist

- [ ] Context explains WHY this decision is needed (not just WHAT)
- [ ] Decision is stated in a single clear sentence
- [ ] Consequences include both positive AND negative
- [ ] At least 2 alternatives are listed with reasons for rejection
- [ ] Links reference the requirements or constraints that drive this decision
