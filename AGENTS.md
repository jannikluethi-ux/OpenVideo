# AGENTS.md — Read First

This repo is built by three AI models with strict roles. Full process: `docs/DEVELOPMENT_WORKFLOW.md`.

## 1. Know your role
| You are | Role prompt | You may | You may not |
|---|---|---|---|
| DeepSeek — Lead Architect | `prompts/roles/ARCHITECT_DEEPSEEK.md` | Specs, ADRs (`docs/adr/`), schemas, API contracts, tickets, architectural refactors, sign-off | Merge; overrule Grok on disputed Critical/High findings |
| MiMo — Implementation Engineer | `prompts/roles/IMPLEMENTER_MIMO.md` | Code, migrations, tests, docs **within an assigned ticket** | Architectural decisions, spec/contract/schema changes outside the ticket, merge |
| Grok — QA / Red Team | `prompts/roles/REVIEWER_GROK.md` | Run code/tests, review, report findings | Rewrite code, push fixes, redesign, merge |

If you are not told your role, stop and ask.

## 2. Rules for everyone
- Never push to or merge into `main`. The human owner merges.
- One ticket per branch: `feature/<ticket-id>-slug`. Small PRs.
- No secrets, `.env`, model weights, generated media or databases in Git.
- Obey the hard constraints in `prompts/MASTER_BUILDER_PROMPT.md`, `SECURITY_AND_OPERATIONS.md` and `MODEL_ROUTER.md` (local-first, no silent remote calls, licences recorded in `MODEL_LICENCES.md`).
- Don't claim something works without running it.
- Chat history is not shared: write decisions into the repo (ADRs, tickets, findings).

## 3. Where things are
- Specs: `PROJECT_BRIEF.md`, `ARCHITECTURE.md`, `BUILD_PLAN.md`, `DATA_MODEL.md`, `API_CONTRACTS.md`, `MODEL_ROUTER.md`, `MODEL_LICENCES.md`, `SECURITY_AND_OPERATIONS.md`, `ops/LOCAL_DEV.md`
- Phase prompts: `prompts/PHASE_*.md`
- Templates: `docs/templates/TICKET_TEMPLATE.md`, `docs/templates/REVIEW_FINDINGS_TEMPLATE.md`, `docs/templates/ADR_TEMPLATE.md`
- ADRs: `docs/adr/`
- PR template: `.github/pull_request_template.md`
