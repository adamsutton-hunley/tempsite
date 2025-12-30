# AGENTS

Quick orientation for anyone (human or agent) working in this repository.

## Layout
- `SpecSuccessReleaseMaker/` – PowerShell automation for Salesforce managed package releases. Entry script: `scripts/CreateRelease.ps1`; configs in `config/`.
- `spec-ai-lambda-functions/` – AWS SAM project with Lambda functions for the SpecSuccess AI document enrichment pipeline (job kickoff, doc fetch, result delivery, DLQ handling). Start at `README.md`.
- `spec-dashboard-jobs/` – AWS SAM project for the CloudWatch dashboard widget Lambda that summarizes client jobs/projects/results. Entry point: `src/lambda_function.py`.
- `tempsite/` – portfolio content; generated assets belong in `tempsite/generated/`.

## Common Tasks
- **Discover**: `rg --files` to locate files; `rg "<term>"` to search contents.
- **Python SAM projects**: create a venv (`python -m venv .venv && source .venv/bin/activate`), install dev deps (`pip install -r requirements-dev.txt` when present), then `sam build` / `sam local invoke` / `sam deploy`.
- **PowerShell release maker**: run `./scripts/CreateRelease.ps1 -Help` for supported actions. Use `-ConfigFile <name>` to target a specific package and branch.
- **Tests**: In `spec-ai-lambda-functions`, run `pytest` (coverage configured). For `spec-dashboard-jobs`, use `sam validate`, `sam build`, and `sam local invoke` with sample events under `events/`.

## Conventions
- Keep edits ASCII-only unless the file already uses other characters.
- Prefer `rg` for searches. Avoid destructive git commands; never reset user changes.
- Place any new portfolio copy or assets under `tempsite/generated/`.

## If Stuck
- Note the exact command and error, plus whether you ran inside a virtual environment.
- For AWS SAM issues, run `sam validate` first to catch template problems before build/deploy.
