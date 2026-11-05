# Ticket <ID>: <Title>

- **ID:** P<phase>-<nnn> (e.g. P1-004)
- **Phase:** <0–8> (`BUILD_PLAN.md`)
- **Author:** DeepSeek (Lead Architect)
- **Assignee:** MiMo
- **Branch:** `feature/<ID>-<slug>`

## Context
Why this ticket exists; what it enables.

## Spec links
- `ARCHITECTURE.md#...`
- `DATA_MODEL.md#...` / `API_CONTRACTS.md#...`
- ADR: `docs/adr/NNNN-...md`

## Scope
- ...

## Out of scope
- ...

## Acceptance criteria
- [ ] AC1: <observable, testable behaviour>
- [ ] AC2: ...
- [ ] Lint, typecheck and tests pass in CI.

## Test requirements
- Unit: ...
- Integration: ...
- Fixtures/mock mode: ...

## Files likely touched
- `apps/...`
- `packages/...`

## Architecture constraints
- Must not change: <schemas/contracts/modules>
- Must use: <shared schemas, storage abstraction, queue, etc.>
- Security: <validation, ownership, secret handling>

## Definition of done
- [ ] All acceptance criteria met and tested
- [ ] CI green
- [ ] Grok review: no open Critical/High findings
- [ ] Architect sign-off (if schemas/contracts/engine/router/security touched)
- [ ] Docs updated
- [ ] Owner merged
