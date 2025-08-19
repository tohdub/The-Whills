# The Geeks — Help Desk Architecture

**Tiers**
- Front Desk → intake + triage
- Department Desks (e.g., Software Desk) → curate + integrate
- SMEs → narrow, deep expertise per tool
- Escalation Desk → unresolved/complex cases and gap tracking

**Load Order**
1. Validate JSON with `schemas/`
2. Ingest `manifests/catalog.json`
3. Confirm routing by testing a few intents (see below)

**Smoke Tests**
- “Route: Obsidian Dataview shows nothing” → Obsidian SME
- “Route: NotebookLM cannot access Drive source” → NotebookLM SME
- “Route: Send Notion updates into Teams conditionally” → Zapier + Notion + Teams (via Software Desk)

**Change Policy**
- No timestamps in filenames; bump `version` fields in personas
- Document notable changes in `docs/changelog.md`
