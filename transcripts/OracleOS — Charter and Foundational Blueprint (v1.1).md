# OracleOS — Charter and Foundational Blueprint (v1.1)

## 🌌 Vision

OracleOS is a **council-governed operating system for digital assistance, asset management, learning, and knowledge orchestration**. It learns from real-world use, curates itself, and remains auditable, persistent, and scalable. OracleOS adapts over time, minimizing knowledge drift and maximizing user value.

---

## 🏛 Core Principles

1. **Governance by Council** — Policies, charters, and edicts ensure safe, consistent, and auditable growth.
2. **Day-One Concierge (Herald)** — A butler-style entrypoint for all user interaction. Accessible, personal, proactive.
3. **Learning by Tutorship** — Every action and feedback loop becomes a learning signal.
4. **Curation Before Drift** — Canonicalization, dedupe, block/allow lists, and fact-checking guard against hallucination.
5. **Scalable Integrations (Integrator)** — Controlled pathways to Zapier, IFTTT, Google Workspace, and beyond.
6. **Persistent & Modular** — Versioned knowledge and assets; swappable modules and Orders.
7. **Future-Proof** — Heralds, skins, and extensions can be layered without touching the core.

---

## ⚖️ Pillars & Orders

* **Ops** — calendars, email, tasks, notifications, file ops
* **Archives** — assets + knowledge, embeddings, provenance
* **Inquiry** — planning, summarization, composition with citations
* **Curation** — dedupe, canonize, prune, block/allow, fact-check
* **Stewards** — provider abstraction (calendar/email/DAM)
* **Tutors** — learning management (signals → experiments → promotion)
* **Integrator (NEW, v1.1)** — structured APIs, connectors (Zapier/IFTTT/etc), future integrations
* **Herald (NEW, v1.1)** — concierge interface for all user interaction

---

## 🧭 Roadmap

### Short-term (Performance-first)

* Lean repo: Ops, Archives, Inquiry, Curation, Stewards, Tutors
* Herald as default user entrypoint
* Integrator with one or two safe API connectors (Zapier, Google Workspace)
* Rituals: daily briefing, meeting ingest, QA with sources

### Medium-term (Personalization & Scale)

* Herald refinement: user memory, proactive engagement
* Expanded Integrator: IFTTT, Slack, Notion, Jira, GitHub
* Graph registry for knowledge relationships
* Tutors issuing weekly Learning Reports

### Long-term (Fun & Extensibility)

* Herald “skins” (Alfred, Jarvis, Scarlett-in-*Her*)
* Persona packs layered on top of core logic
* Community-driven Orders and Rituals
* Federation across multiple OracleOS instances

---

## 🛡 Governance & Safety

* **Council** approves promotions (draft → canon), provider swaps, destructive ops.
* **Edicts** enforce provenance, citations, abstain-if-uncited, freshness bias.
* **Audits** log all Ritual runs in `ledger/events.jsonl`.
* **Tutors** capture lessons learned and propose changes → Council approves → Curation promotes.

---

## 📂 Repository Layout (baseline)

```
oracleos/
├─ README.md
├─ LICENSE
├─ council/
├─ orders/
├─ herald/              # concierge entrypoint (NEW)
├─ integrator/          # API/connector layer (NEW)
├─ writs/
├─ rituals/
├─ registries/
├─ ledger/
├─ stores/
├─ modules/
├─ policies/
├─ contracts/
├─ evaluations/
└─ tools/
```

---

## 📌 v1.1 Lock-in

* Name: **OracleOS** (finalized)
* Herald: **Day-one, default entrypoint** (not optional, not later)
* Integrator: **Scoped, performance-conscious** (start lean, expand safely)
* Repo: structured for performance today, extensibility tomorrow
