# Internal API Contracts

Use `/api/v1`. Validate all requests and responses with shared schemas (Zod or equivalent). Generate OpenAPI documentation from route schemas.

## Projects
- `GET /projects`
- `POST /projects`
- `GET /projects/:projectId`
- `PATCH /projects/:projectId`
- `DELETE /projects/:projectId`

## Assets
- `POST /projects/:projectId/assets` — upload or request upload session.
- `GET /projects/:projectId/assets`
- `GET /assets/:assetId`
- `POST /assets/:assetId/versions`
- `GET /assets/:assetId/download`

## Creative planning
- `POST /projects/:projectId/music-analysis`
- `GET /projects/:projectId/music-analysis/:analysisId`
- `POST /projects/:projectId/scenes`
- `POST /scenes/:sceneId/shots`
- `PATCH /shots/:shotId`
- `POST /shots/:shotId/prompts`
- `POST /shots/:shotId/approve`

## Workflows and jobs
- `POST /projects/:projectId/workflows`
- `GET /workflows/:workflowId`
- `POST /workflows/:workflowId/validate`
- `POST /workflows/:workflowId/runs`
- `GET /workflow-runs/:runId`
- `POST /jobs/:jobId/cancel`
- `POST /jobs/:jobId/approve-cost`
- `GET /jobs/:jobId/events` (SSE or WebSocket)

## Timeline and render
- `GET /projects/:projectId/timeline`
- `PUT /projects/:projectId/timeline`
- `POST /projects/:projectId/renders`
- `GET /renders/:renderId`

## Worker registration
- `POST /internal/workers/register`
- `POST /internal/workers/heartbeat`
- `GET /internal/workers/capabilities`

## API rules
- Use idempotency keys for job creation and uploads.
- Enforce project ownership on every route.
- Never accept arbitrary filesystem paths from clients.
- Never expose provider secrets.
- Return structured error codes, not raw stack traces.
- Use pagination for lists.
- Use SSE/WebSockets for progress; polling is an acceptable first implementation.