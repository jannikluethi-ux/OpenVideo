# Build Plan and Acceptance Gates

Build in phases. Do not ask an agent to generate the entire production application in one pass. That usually creates an impressive-looking but brittle shell.

## Phase 0 — Repository and engineering foundation
Deliver:
- Monorepo structure and package manager.
- TypeScript strict mode, linting, formatting and test runner.
- Environment configuration validation.
- Docker Compose for core services.
- CI workflow for lint, typecheck and tests.
- Architecture decision records (ADRs).

Acceptance:
- Fresh clone can start core services using documented commands.
- No secrets in source control.
- CI passes on a clean checkout.

## Phase 1 — Core application shell
Deliver:
- React app with navigation and responsive shell.
- Fastify API with health/readiness endpoints.
- PostgreSQL migrations and typed database access.
- Local single-user auth/session.
- Project CRUD.
- Storage abstraction and asset upload.

Acceptance:
- Create, rename, open and delete a project.
- Upload media; calculate checksum and persist metadata.
- Restart services without losing project data.

## Phase 2 — Production data model and asset bible
Deliver:
- Characters, locations, props, wardrobe, visual styles and reference assets.
- Scenes, shots, shot versions and prompt versions.
- Project-level asset library and search.
- Asset relationship linking (e.g. shot uses character + location + prop).

Acceptance:
- Create reusable entities and link them to shots.
- Every shot records the exact asset versions used.
- Export/import project metadata as JSON.

## Phase 3 — Music analysis and director workflow
Deliver:
- Audio ingest and technical metadata.
- Waveform and editable timeline markers.
- BPM/tempo estimate, duration, silence and energy features where feasible.
- Manual section editor (intro, verse, chorus, bridge, outro).
- Treatment → sequence → scene → shot planning workflow.
- Structured output schema and validation for AI-assisted planning.

Acceptance:
- User can map a song into sections and create an editable shot list.
- All AI-generated plans are drafts until user approves them.
- No unsupported claim that automatic beat detection is perfectly accurate.

## Phase 4 — Workflow canvas and orchestration
Deliver:
- Typed node graph editor.
- Node registry and schema definitions.
- DAG validation.
- Workflow versioning.
- BullMQ execution, progress, cancellation, retries and logs.
- Job history.

Acceptance:
- Run a multi-node workflow with deterministic mock nodes.
- Invalid graphs are rejected before execution.
- Reloading the UI preserves graph and run history.

## Phase 5 — Local model integrations
Deliver:
- ComfyUI adapter for image generation.
- Local LLM adapter for structured creative assistance.
- Local video adapter interface and first verified runnable model integration.
- Worker capability registry (VRAM, model availability, supported tasks, limits).
- Model/version metadata and output provenance.

Acceptance:
- A local image generation job can be queued, monitored and stored.
- Local model availability is checked before dispatch.
- Model licence and hardware notes are documented for the exact tested version.
- No remote API is called as fallback.

## Phase 6 — Review, timeline and rendering
Deliver:
- Shot review board: approve, reject, annotate, regenerate.
- Timeline manifest editor.
- FFmpeg media pipeline.
- Proxy generation and final render job.
- Export MP4 plus project manifest and assets.

Acceptance:
- Assemble approved clips against the imported music.
- Validate duration, frame rate, resolution and audio stream.
- Re-rendering the same manifest produces a predictable result within codec limitations.

## Phase 7 — Optional paid provider adapters
Deliver only if requested:
- Provider adapter interfaces and individual official API integrations.
- Secret management.
- Per-model cost estimates and usage capture.
- Approval gate before every paid job.
- Data-transfer disclosure.

Acceptance:
- Remote integrations are disabled by default.
- A remote job cannot execute without explicit user approval.
- If pricing is unknown, show “cost unknown” and require explicit acknowledgement.
- No silent provider substitution.

## Phase 8 — Hardening and release
Deliver:
- Backup/restore.
- Audit logs.
- Resource limits and worker isolation.
- Dependency and container scanning.
- Performance tests.
- User documentation and recovery runbook.

Acceptance:
- Restore a backup into a clean environment.
- A worker crash does not corrupt project state.
- Security review finds no exposed secrets or unrestricted arbitrary command execution.