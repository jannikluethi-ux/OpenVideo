# Local-First AI Video Studio — Builder Package

**Purpose:** Build a self-hosted, local-first AI video production environment for music videos. The system should orchestrate creative workflows, manage assets, run local models where practical, and optionally connect to paid model APIs through user-supplied keys.

**Core economic rule:** The platform itself must not sell or require credits. Local inference should be the default. External APIs are optional, explicitly costed, disabled by default, and never called without user approval.

## What this package contains

- `PROJECT_BRIEF.md` — product definition, non-goals and success criteria.
- `ARCHITECTURE.md` — recommended environment split and system design.
- `BUILD_PLAN.md` — staged implementation plan and acceptance gates.
- `DATA_MODEL.md` — initial entities and relationships.
- `API_CONTRACTS.md` — internal service boundaries and API expectations.
- `MODEL_ROUTER.md` — local-first model routing and cost controls.
- `SECURITY_AND_OPERATIONS.md` — secrets, sandboxing, backups and deployment.
- `prompts/MASTER_BUILDER_PROMPT.md` — the complete environment-level build prompt.
- `prompts/PHASE_*.md` — prompts to execute each build phase independently.
- `AGENTS.md` — rules every AI model must read first.
- `docs/DEVELOPMENT_WORKFLOW.md` — multi-model workflow (DeepSeek architect / MiMo implementer / Grok reviewer).
- `prompts/roles/` — role system prompts: `ARCHITECT_DEEPSEEK.md`, `IMPLEMENTER_MIMO.md`, `REVIEWER_GROK.md`.
- `docs/templates/` — ticket, review findings and ADR templates.
- `docs/adr/` — architecture decision records.
- `.github/pull_request_template.md` — PR checklist.
- `ops/LOCAL_DEV.md` — local development setup expectations.
- `.gitignore` — baseline exclusions for a GitHub repository.

**How we build:** see `docs/DEVELOPMENT_WORKFLOW.md`.

## Recommended repository name

`local-first-ai-video-studio`

Rename freely. Do not put API keys, generated media, model weights, private source footage or production databases in Git.

## Critical constraints

1. This is a **clean-room implementation**. Do not copy Nodaro source code, proprietary UI, protected implementation details, branding, or enterprise code. Use only independently designed code and dependencies with compatible licences.
2. Do not assume a model is free for commercial use because its weights are downloadable. Record and verify the licence for each model/version before enabling it.
3. “No credits” does not mean “zero cost”. Local inference consumes GPU time, electricity, storage and maintenance. Renting a GPU is still a cost.
4. Seedance, Veo and Kling are proprietary services. Their hosted versions require provider billing. This design must not pretend they can be run locally without authorised weights.
5. No external provider may be called unless the user explicitly enables that provider and confirms the estimated cost for the job.

## Build status

This is a specification and agent-builder package, not a completed application. The coding agent must implement the software, tests, deployment files and documentation phase by phase. It must not claim a feature is complete until it is implemented and tested.