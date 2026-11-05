# Architecture Decision Records

ADRs are the shared architectural memory of this repo. Models do not share chat history — if a decision isn't in an ADR or spec, it isn't decided.

- **Owner:** DeepSeek (Lead Architect) writes and updates ADRs. MiMo and Grok may propose one via a question/finding, but don't author architectural decisions.
- **Format:** `docs/templates/ADR_TEMPLATE.md`.
- **Numbering:** `NNNN-kebab-title.md`, sequential from `0001`, never reused.
- **Immutability:** accepted ADRs aren't rewritten; supersede with a new ADR and update the old status.
- **When:** any decision affecting schemas, API contracts, workflow engine, model router, storage, security boundaries, dependencies/licences, or deployment topology.
- **Review:** Grok checks PRs against relevant ADRs; conflicts are architectural findings routed to DeepSeek.
- **Phase 0** (`BUILD_PLAN.md`) requires initial ADRs (e.g. monorepo layout, package manager, storage approach).
