# Loader Guide — Fresh Chat Deployment

## Goal
Spin up a fresh custom GPT with permanent memory and load this repo’s personas/routing cleanly.

## Steps
1. Start a new custom GPT (fresh chat).
2. Upload the repo or point the connector at the repo.
3. Load order:
   - Validate JSON (optional, but recommended).
   - Ingest `manifests/catalog.json`.
   - Ingest each path listed under `personas` and `routing`.
4. Sanity checks:
   - “Alfred, list available personas.” → Expect IDs from `catalog.json`.
   - “Alfred, load Software Support Desk to triage: ‘Obsidian Dataview empty on iOS.’”
   - “Alfred, convene Networking Corner + Notion Architect for: ‘Share DB between teams, limited perms.’”
5. Release notes:
   - Keep `docs/changelog.md` updated.
   - Bump `VERSION` and persona `version` fields on changes.

## Troubleshooting
- Persona not found → confirm path in `catalog.json`.
- Routing misses intent → add keywords/patterns; re-validate; reload.
- Scope creep → tighten persona `constraints` and add `handoff`.
