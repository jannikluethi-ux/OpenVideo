# Local Development

Target macOS/Linux development. Use Docker Compose for PostgreSQL, Redis and optional object storage. GPU inference may run outside Docker; Linux with compatible NVIDIA GPU is likely target for demanding local video inference. App must run in mock mode without GPU.

Suggested monorepo: apps/web (React UI), apps/api (Fastify), workers/orchestrator (DAG/BullMQ), workers/media (FFmpeg), workers/audio (Python), workers/models (adapters), packages/contracts, packages/workflow-engine, packages/storage, packages/config, infra/docker-compose.yml, docs and prompts.

Modes: mock (no GPU); local (registered workers); remote (providers individually enabled, disabled by default, per-job approval). Create .env.example with DATABASE_URL, REDIS_URL, STORAGE_ROOT, SESSION_SECRET, APP_BASE_URL, optional COMFYUI_BASE_URL, optional local LLM endpoint and optional provider keys. Never require provider keys for startup. Document commands to start infrastructure, migrate/seed and start app. No keys, weights, media or credentials in seed data.