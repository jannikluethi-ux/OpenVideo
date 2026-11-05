# Model Router — Local First, Cost Controlled

## Policy

1. Local workers are preferred.
2. Remote providers are disabled by default.
3. No automatic fallback from local to remote.
4. Every remote job requires explicit per-job approval.
5. Every model entry must include a verified licence status and tested version.
6. A model is not “free” merely because its weights are downloadable.

## Internal task types

- `text.generate_structured`
- `audio.analyse`
- `image.generate`
- `image.edit`
- `video.generate`
- `video.extend`
- `video.upscale`
- `video.interpolate`
- `media.inspect`
- `media.transcode`
- `media.render`

## Model capability record

Each model adapter should declare:
- `model_id`, `version`, `provider`
- `execution_mode`: `local` or `remote`
- `task_types`
- accepted input/output formats
- max dimensions, duration and batch size
- VRAM/RAM requirements where known
- licence name, URL, commercial-use status and review date
- estimated runtime range where measured
- cost model (`zero_api_cost`, `metered`, `subscription`, `unknown`)
- supported parameters and defaults

## Routing logic

Rank eligible local workers by:
1. task compatibility,
2. required model/version availability,
3. hardware capacity,
4. estimated runtime,
5. output constraints.

If no local worker is eligible:
- Return a clear `NO_LOCAL_WORKER_AVAILABLE` error.
- Offer remote options only if the user has enabled providers.
- Never dispatch remotely without a separate approval action.

## Cost guard

For remote inference:
- Show provider and exact model.
- Show estimate or “unknown”.
- Show data that will leave the local environment.
- Require a user-defined maximum cost or explicit unknown-cost acknowledgement.
- Persist approval and actual provider usage.
- Stop if provider estimate exceeds approved ceiling.
- Never place API keys in browser code or workflow JSON.

## Initial integration order

1. ComfyUI for local image generation.
2. Ollama or vLLM for local LLM assistance (choose one initial runtime).
3. Python audio-analysis worker.
4. A verified local video model selected after hardware benchmark.
5. Optional official API adapters, only on request.

Do not promise a specific video model will run acceptably until tested on the target GPU. Model availability, memory requirements, speed and licence terms change by release.