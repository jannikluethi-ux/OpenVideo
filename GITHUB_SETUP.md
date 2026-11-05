# GitHub Repository Setup

1. Create a private GitHub repository named `local-first-ai-video-studio` (or choose another name).
2. Extract this package into the repository root.
3. Review the specifications and adjust the product name.
4. Commit the builder package before asking a coding agent to implement anything.
5. Keep the repository private while architecture, security and licensing are being established.
6. Add branch protection after the first CI workflow exists.
7. Never commit `.env`, API keys, model weights, generated media, private footage, databases or backups.

Suggested initial commit:

`docs: add local-first AI video studio builder package`

Suggested branches:
- `main` — stable, reviewed work.
- `develop` — integration branch if needed.
- `feature/*` — isolated implementation work.

Suggested GitHub Issues:
- Phase 0 — Foundation
- Phase 1 — Core app
- Phase 2 — Asset bible
- Phase 3 — Music/director workflow
- Phase 4 — Workflow engine
- Phase 5 — Local model workers
- Phase 6 — Review/timeline/render
- Phase 7 — Optional remote APIs
- Phase 8 — Hardening

Do not ask an agent to implement all phases in a single prompt. Start with `prompts/MASTER_BUILDER_PROMPT.md`, then execute one phase prompt at a time.