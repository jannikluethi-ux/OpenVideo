# Project Brief

## Product

A self-hosted AI video production studio focused initially on music videos. It provides a visual workflow editor, project and asset management, song analysis, shot planning, model orchestration, generation queues, editing/rendering and export.

The system is local-first and provider-neutral. It should run on a user's own machine or private network. A separate GPU worker can be attached later. Optional commercial APIs are adapters, not the foundation.

## Primary user outcome

Turn a music track and creative direction into a repeatable production pipeline:

1. Create a project and import a track.
2. Analyse the track's duration, structure, tempo and energy.
3. Create a treatment, visual concept, storyboard and shot list.
4. Define reusable characters, locations, props, wardrobe and visual references.
5. Generate stills and video clips using local models by default.
6. Review, reject, revise and regenerate individual shots.
7. Assemble approved clips to the music timeline.
8. Render a final video and export project assets and metadata.

## Product principles

- Local-first, no mandatory credits, no hidden API calls.
- User owns project files and can export them.
- Every generation records model, version, prompt, seed (when available), parameters, input assets, output assets, runtime and cost.
- Reproducibility: a workflow can be saved, cloned, versioned and rerun.
- Human approval at important creative and cost gates.
- Model-agnostic adapters; no provider lock-in.
- Fail safely: queue errors, interrupted jobs and unavailable models must not corrupt a project.
- The UI must clearly distinguish local inference from paid remote inference.

## MVP scope

### Must have
- Authentication for local/private deployment (single-user mode first).
- Project CRUD and project-level asset library.
- Upload/import audio, images and video.
- Song metadata and waveform display.
- Manual song section markers and editable beat/section annotations.
- Treatment, scene, shot and prompt records.
- Visual asset bible: characters, locations, props and style references.
- Node-based workflow canvas with typed nodes and edges.
- Job queue, job status, retries and cancellation.
- ComfyUI adapter as the first local image-generation integration.
- Generic local video-model adapter interface; integrate only models that are actually runnable and licence-cleared.
- FFmpeg-based media inspection, proxy creation, concatenation and final export.
- Generation history and prompt/version tracking.
- Local storage with backup/export.
- Cost guard that blocks paid-provider jobs unless explicitly approved.

### Defer until after MVP
- Multi-user teams and billing.
- Marketplace or public hosted SaaS.
- Mobile app.
- Collaborative real-time editing.
- Full nonlinear editor comparable to Premiere/DaVinci.
- Automatic lip-sync and advanced motion capture.
- Training/fine-tuning models.
- Public sharing, social publishing and cloud asset hosting.

## Non-goals

- Recreating another product's code or protected interface.
- Bypassing provider billing, authentication, rate limits or terms.
- Claiming proprietary hosted models can run locally.
- Building a full professional NLE in the first release.
- Automatically publishing content to third-party platforms.

## Definition of done for MVP

A user can create a project, import a music track, create a shot list, generate or import clips, review them, assemble a timeline and render an export without purchasing platform credits. Local compute costs remain the user's responsibility. Remote APIs are disabled unless explicitly configured and approved.