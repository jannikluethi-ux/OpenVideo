# Architecture and Environment Split

## Recommended split

Do not build this as one giant application process. Split it into five logical environments. They can initially run on one computer with Docker Compose, then move independently as workloads grow.

```text
                 USER / BROWSER
                       |
                WEB STUDIO (UI)
                       |
                CONTROL PLANE API
           /           |             \
      PostgreSQL     Redis        Object Storage
                         |
                    JOB WORKER
                         |
                 MODEL ROUTER
                 /     |      \
          ComfyUI   Local Video  Optional Remote APIs
          (GPU)       Worker       (paid, opt-in)
                 \     |      /
                   MEDIA PIPELINE
                  FFmpeg / Remotion
                         |
                  PROJECT OUTPUTS
```

### Environment 1 — Studio / Control Plane
**Responsibility:** User-facing product and orchestration API.

Components:
- Web UI: React + TypeScript + Vite.
- Workflow canvas: React Flow (or another appropriately licensed graph editor).
- API: Fastify + TypeScript.
- Authentication: local single-user mode first; add OIDC later.
- Project, shot, asset and workflow management.
- Prompt editor and generation history.
- Cost/approval interface.

Runs comfortably on a Mac or standard workstation. It should not require a GPU.

### Environment 2 — Data / Queue / Storage
**Responsibility:** Durable state, job coordination and media storage.

Components:
- PostgreSQL: projects, users, workflows, shots, jobs, metadata and audit trail.
- Redis: queue state, locks, progress events and short-lived coordination.
- BullMQ: asynchronous job processing.
- MinIO or filesystem-backed storage for local development; S3-compatible object storage as a deployment option.
- A storage abstraction so the application is not coupled to one storage vendor.

Use persistent Docker volumes. Never store important project metadata only in Redis.

### Environment 3 — Inference / Model Workers
**Responsibility:** Run models and expose a stable internal interface.

Components:
- ComfyUI adapter first for image workflows.
- Local video worker adapter(s), selected only after hardware and model licence checks.
- Local LLM adapter via Ollama or vLLM for structured planning and prompt assistance.
- Optional audio analysis worker using Python libraries.
- Optional remote-provider adapters, disabled by default.

Keep model runtimes isolated from the main API. A GPU worker may run on a separate Linux machine and register itself with the control plane. The Mac can remain the control centre.

### Environment 4 — Media Pipeline / Rendering
**Responsibility:** Inspect, transform, assemble and render media.

Components:
- FFmpeg/ffprobe for media inspection, transcoding, proxy creation, audio extraction, clip trimming and final muxing.
- Remotion for programmatic compositions and titles where useful.
- Timeline manifest as the source of truth for clip order, in/out points, transitions and audio.
- Render workers should be separate from API processes to avoid blocking the application.

### Environment 5 — Optional External Providers
**Responsibility:** Connect to commercial services only when explicitly enabled.

Examples:
- Seedance, Veo, Kling or other provider APIs, only where official API access exists.
- Provider adapters must be isolated behind the same internal model interface.
- API keys are encrypted at rest and never returned to the browser.
- A user must see provider, model, estimated cost, expected duration and data-transfer notice before approving a remote job.
- No silent fallback from local to paid remote inference.

## Deployment topology

### Development (single machine)
Docker Compose:
- `web`
- `api`
- `postgres`
- `redis`
- `worker`
- `storage` (optional MinIO)
- `comfyui` (may be external process or separate profile)
- `render-worker`

GPU model containers should be optional profiles. Do not force users without compatible GPUs to pull multi-gigabyte model images.

### Recommended eventual topology
- Mac: web studio, API, database, queue, storage control, project management.
- Linux GPU workstation: ComfyUI and video model workers.
- Optional NAS: media archive and backups.
- Optional remote provider adapters: opt-in only.

## Internal service boundaries

1. **Studio API** owns projects, assets, workflows, shots, prompts and approvals.
2. **Orchestrator** validates a workflow DAG, resolves dependencies and schedules jobs.
3. **Model Router** chooses a compatible local worker or an approved remote provider.
4. **Worker Adapter** translates the internal job schema to a model-specific request.
5. **Media Service** probes, normalizes and renders media.
6. **Storage Service** owns paths, checksums, retention and signed/local access.
7. **Event Service** emits job progress and completion events to the UI.

Do not let frontend code call model runtimes directly. All generation goes through the API, queue and model adapter.

## Workflow execution

- Workflows are directed acyclic graphs (DAGs).
- Nodes declare input/output types and execution requirements.
- Validate graph shape and types before queueing.
- Persist a workflow version snapshot when execution starts.
- Each run gets immutable input references and a run ID.
- Nodes run only after dependencies succeed.
- Retry transient errors with bounded backoff.
- Do not automatically retry invalid prompts, invalid media or cost-approval failures.
- A failed node should not erase successful upstream outputs.
- Support cancellation and resumable runs where technically safe.

## Key design decision

Build a **workflow orchestrator**, not a model zoo UI. The differentiator is the repeatable production process: music analysis → creative direction → shot planning → asset consistency → generation → review → edit → export.