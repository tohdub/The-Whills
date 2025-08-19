# The Whills: A Meta‑OS

*A governance‑first orchestration layer for agents, knowledge, and workflows — written as a technical framework with a quiet myth inside.*

---

## Purpose
**The Whills** is a meta‑operating system: a lightweight framework that coordinates multiple agentic roles, versioned knowledge, and auditable workflows. It is designed to scale with real‑world use, resist drift, and remain explainable. The language is plain. The architecture is modular. The story is there if you look for it.

> Subtext: a council that remembers (past), shapes (present), and projects (future).

---

## Core Idea
Map durable responsibilities onto clear operators:
- **Whills (Triad)** — Top‑level governance and direction.
  - **Archivist** (past): memory, provenance, continuity.
  - **Architect** (present): coherence, structure, policy.
  - **Auteur** (future): lessons → forecasts, goals, KPIs.
- **Orders (Execution)** — Independent operators with handoffs.
  - **Scribes**: turn briefs into documentation.
  - **Geeks**: turn docs into tools, workflows, prototypes.
  - **Stewards**: turn tools into lived practices and adoption.

Each part is small, testable, and replaceable. No single agent is “the system.”

---

## Information Flow
**Whills → Scribes → Geeks → Stewards → Whills**
1. **Call** (Whills): brief, scope, risks.
2. **Threshold** (Scribes): clarify, document, acceptance gate setup.
3. **Trials** (Geeks): build, test, resolve dependencies.
4. **Return to the World** (Stewards): adapt for humans, pilot, measure adoption.
5. **Return with the Elixir** (Whills): audit alignment, record lessons, set next goals.

*(Yes, the cycle nods to the Hero’s Journey; the code still ships.)*

---

## Governance Contracts
- **Acceptance Gates (AG1–AG5)**
  - AG1: frontmatter present
  - AG2: draft completeness
  - AG3: review verdict
  - AG4: normalization (schemas, style)
  - AG5: validation (tests, checks)
- **Narrative Checkpoints (NC1–NC3)**
  - NC1: purpose alignment
  - NC2: scope clarity
  - NC3: risk visibility
- **Routing Defaults**
  - briefs → **Scribes**
  - tooling blockers → **Geeks**
  - adoption issues → **Stewards**
  - audits/values → **Whills**

All gates/checkpoints are logged to the **Ledger**.

---

## Artifacts & Stores
- **Ledger** (`ledger/events.jsonl`) — append‑only events for rituals, reviews, decisions.
- **Knowledge Index** (`knowledge.index.md`) — curated, canonical references.
- **Rituals** (`rituals/`) — pipelines/workflows.
- **Writs** (`writs/`) — atomic actions (e.g., `calendar.create`).
- **Policies** (`governance/`) — acceptance, privacy, quality, risk.
- **Operator READMEs** — responsibilities, interfaces, artifacts.

---

## Repository Layout (suggested)
```
/ (root)
├─ README.md                          # this file
├─ whills/
│  ├─ archivist/README.md             # past: memory, provenance
│  ├─ architect/README.md             # present: coherence, policy
│  └─ auteur/README.md                # future: forecasts, KPIs
├─ orders/
│  ├─ scribes/README.md
│  ├─ geeks/README.md
│  └─ stewards/README.md
├─ governance/
│  ├─ acceptance-gates.md
│  ├─ narrative-checkpoints.md
│  └─ council-rules.md
├─ ledger/
│  └─ events.jsonl
├─ rituals/
├─ writs/
├─ integrations/
├─ registries/
├─ policies/
└─ knowledge.index.md
```

---

## Roles at a Glance
- **Archivist** — ingestion, indexing, curation, provenance, recall.
- **Architect** — schemas, manifests, policy enforcement, routing, CI checks.
- **Auteur** — retrospectives → goals; KPI dashboards as campaign maps.
- **Scribes** — briefs → documentation; clarity and completeness.
- **Geeks** — documentation → tools; stress tests and dependency maps.
- **Stewards** — tools → adoption; rituals, guides, chronicles.

All operators emit events to the **Ledger** for audit and learning.

---

## Anti‑Drift & Safety
- Retrieval‑first with provenance; abstain on low confidence.
- Freshness bias; canonical promotion via Curation.
- Data classes: `public | internal | restricted`.
- Two‑phase commit for destructive actions; human confirmation where needed.

---

## Getting Started
1. **Fork/clone** this repo.
2. Create `ledger/events.jsonl` and turn on event logging.
3. Add a simple **Ritual** (e.g., `rituals/daily-briefing.yaml`).
4. Run the cycle once: Whills brief → Scribes doc → Geeks prototype → Stewards pilot → Whills audit.
5. Commit artifacts; update `knowledge.index.md`.

If you prefer a guide, see `governance/acceptance-gates.md` and the operator READMEs.

---

## Contribution
- Proposals land as PRs with gate/checkpoint annotations.
- CI enforces schema validation and basic policy checks.
- The Council (maintainers) reviews purpose, scope, and risk.

> Small changes that improve clarity are favored. The legend grows by drops.

---

## License & Attribution
Choose a license that matches your goals (MIT/Apache‑2.0 recommended). Attribution to contributors is recorded in the Ledger and Git history.

---

## Footnote
Some frameworks shout. This one quietly keeps the fire. If you notice the myth under the mechanics, consider it a friendly nod from the Council.

