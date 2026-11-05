# Initial Data Model

Use UUID primary keys, UTC timestamps and explicit project ownership. Prefer migrations over runtime schema mutation.

## Core entities

- `users`: local account identity and auth metadata.
- `projects`: name, description, aspect ratio, target resolution, frame rate, status.
- `project_members`: reserved for future collaboration; single-user mode can omit UI.
- `assets`: project, type, storage key, filename, MIME type, size, checksum, duration, dimensions, metadata, created timestamp.
- `asset_versions`: immutable replacement/version records.
- `creative_entities`: reusable character, location, prop, wardrobe or visual-style record.
- `creative_entity_versions`: immutable descriptions and reference links.
- `scenes`: project, sequence, title, narrative purpose, song section, order.
- `shots`: scene, shot number, duration target, framing, lens/camera movement, action, lighting, continuity notes, status.
- `shot_entity_links`: shot-to-character/location/prop/wardrobe/style relationships.
- `prompts`: prompt text, negative prompt, structured prompt JSON, version, author/source.
- `workflows`: project, name, description, graph JSON, version.
- `workflow_runs`: workflow snapshot, status, started/ended timestamps, error summary.
- `jobs`: run, node, task type, queue, status, progress, attempts, worker, cost estimate, actual cost, timestamps.
- `job_inputs`: immutable references to input assets and parameters.
- `job_outputs`: output asset references and metadata.
- `model_providers`: provider identifier, enabled flag, configuration reference (never raw secret).
- `model_catalog`: provider, model ID, version, task capabilities, local/remote, licence record, hardware requirements.
- `approvals`: user, job, approval type, approved cost ceiling, timestamp.
- `timeline_edits`: project, version, timeline manifest JSON.
- `renders`: timeline version, render settings, status, output asset, logs.
- `audit_events`: actor, action, target, timestamp and safe metadata.

## Important invariants

- Assets are never overwritten in place; create a new version.
- Workflow runs use immutable graph snapshots.
- A job records the exact model ID/version and parameter set.
- Every output records provenance and input references.
- Remote jobs require an approval record.
- Secrets never appear in `model_providers` JSON, logs or API responses.
- Deleting a project must be a deliberate operation with a retention/backup policy.