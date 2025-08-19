# Feedback Loop — From Lived Events to Personalized Growth (with Optional Gamification)

> A practical spec for the Council’s learning heartbeat. Technical first; myth tucked between the lines.

---

## Objectives

* Convert **real‑world events** into **reliable telemetry**.
* Use Tutors to propose **measurable improvements** without drift.
* Let the Council approve changes via **Acceptance Gates (AG) / Narrative Checkpoints (NC)**.
* Update knowledge canon and future goals **automatically** (Archivist ⇄ Auteur).
* Offer an **optional, skinnable gamification layer** that never distorts reality.

---

## Lifecycle (System View)

1. **Act** → User completes or declines an action (Stewards domain: career/family/development/learning).
2. **Log** → Emit event to `ledger/events.jsonl` (append‑only NDJSON).
3. **Learn** → Tutors batch/analyze; generate proposals (prompts, thresholds, retrieval params, nudges).
4. **Review** → Council applies NC/AG checks; approve, amend, or reject.
5. **Promote** → Curation updates canon; Archivist indexes; Architect updates manifests if needed.
6. **Project** → Auteur recalculates KPIs/targets and publishes one‑page **Campaign Map**.

---

## Event Schema (NDJSON)

Each line in `ledger/events.jsonl` is a self‑contained JSON object.

```json
{
  "ts": "2025-08-19T15:04:05Z",
  "actor": "user|system|order.stewards|order.geeks|order.scribes",
  "type": "steward.embed|scribe.archive|geek.build|tutor.proposal|council.verdict|auteur.forecast",
  "domain": "career|family|development|learning|ops|archives|inquiry|curation",
  "artifact": {
    "id": "urn:artifact:ritual:daily_briefing:2025w34",
    "kind": "ritual|writ|doc|tool|report"
  },
  "payload": {
    "summary": "string",
    "metrics": {"kpi_name": 12.3},
    "links": ["/rituals/daily-briefing.yaml", "/orders/stewards/README.md"]
  },
  "privacy": "public|internal|restricted",
  "provenance": {"source": "github|api|cli", "hash": "sha256:..."}
}
```

**Conventions**

* Never edit old lines; corrections are new events with `type: correction`.
* Use `privacy` to gate downstream visibility.
* Use `provenance.hash` for audit integrity.

---

## Tutor Proposals

Tutors convert telemetry into safe change proposals.

```json
{
  "ts": "2025-08-19T15:30:00Z",
  "actor": "tutor",
  "type": "tutor.proposal",
  "domain": "learning",
  "payload": {
    "change": "retrieval.top_k -> 8 (was 5)",
    "reason": "answer docs now denser; precision holding, recall rising",
    "evidence": ["urn:artifact:report:kqa_eval:2025w33"],
    "risk": "low",
    "rollout": {"scope": "self", "ttl_days": 14}
  }
}
```

**Gate Mapping**

* **NC1** purpose alignment, **NC2** scope clarity, **NC3** risk visibility.
* **AG3** review verdict, **AG4** normalization to schema, **AG5** validation (checks/tests).

---

## KPIs & Campaign Map (Auteur)

The Auteur publishes a single page per cycle (week/month):

* **Headline KPIs** (objective, target, current, delta vs. last cycle/year).
* **Lessons Carried Forward** (1–3 bullet summaries from retrospectives).
* **Next Quests** (approved goals framed plainly; myth optional).
* **Links** → to proposals, rituals, and evidence.

Location: `/whills/auteur/campaign-map.{yyyy-w##|yyyy-mm}.md`.

---

## Personalization

* **Prefs**: `stores/prefs/user.json` (tone, channel, cadence, quiet hours, challenge level).
* **Herald/Butler** reads prefs, shapes delivery (cards, chat, voice) and nudge rate.
* **Tutors** consider prefs when proposing changes (e.g., fewer prompts at high load).

Example prefs:

```json
{
  "tone": "professional",
  "delivery": ["chat","dashboard"],
  "quiet_hours": ["21:00","07:00"],
  "nudge_per_day_max": 3,
  "challenge": "standard"
}
```

---

## Gamification (Optional Skin)

Kept strictly separate from truth. It *reflects* progress; it never invents it.

* **XP**: derived from verified events (weight by effort/impact).
* **Badges**: auto‑issued on Council‑approved milestones (e.g., 4 consecutive weekly Campaign Maps).
* **Quests**: aliases for approved goals; same IDs, prettier names.
* **Lore Artifacts**: optional mirrors of reports as “Relics/Scrolls”.

Skin mapping lives in `skins/{theme}/mapping.yaml`.

---

## Privacy & Safety

* Data classes: `public|internal|restricted`.
* Redaction on ingest (`policies/privacy.redaction.yaml`).
* Human confirmation for destructive actions (two‑phase commit).
* Right‑to‑forget honored via `archive.request_redaction` events with Council oversight.

---

## Interfaces & Ownership

* **Producers**: Stewards (real‑world events), Geeks (build/test), Scribes (docs), Tutors (proposals), Council (verdicts), Auteur (maps).
* **Consumers**: Archivist (index/recall), Herald (UX), Evaluations (benchmarks).
* **Owner**: Council → Whills; day‑to‑day: Archivist + Tutors.

---

## Quickstart Checklist

* [ ] Create `ledger/events.jsonl` (append‑only).
* [ ] Emit 3 starter events (scribe.archive, geek.build, steward.embed).
* [ ] Enable Tutors to read ledger; output one `tutor.proposal`/week.
* [ ] Add `governance/acceptance-gates.md` + `narrative-checkpoints.md`.
* [ ] Have the Whills publish the first **Campaign Map**.
* [ ] (Optional) Add a skin: `skins/plain/` or `skins/fellowship/`.

---

## Note on Tone

These docs are intentionally technical. Any myth you find here is an easter egg, not a requirement. The work is the work; the story is for those who enjoy it.
