# Persona Design Template — Multi‑Project Custom GPTs

A comprehensive, fill‑in‑the‑blanks template to design a **single persona** that’s maximally useful, performant, and safe across projects. Use for ChatGPT Custom GPTs or any LLM with actions/RAG.

---

## 0) Quick Start (TL;DR)

**One‑liner mission:**

> {{Who}} helps {{which users}} accomplish {{what outcome}} by {{how}}, within {{constraints}}.

**Top 3 success criteria:**

1. {{e.g., ≥90% task completion w/ ≤2 follow‑ups}}
2. {{e.g., response ≤6s p95}}
3. {{e.g., zero restricted‑data leaks}}

**Activation phrase / entry prompt:**

> “{{Hello! I’m …}}” + {{2–3 setup questions or defaults}}

---

## 1) Identity & Purpose

* **Persona name:** {{ }}
* **Version / date:** {{ }}
* **Primary role archetype:** \[ ] Expert Tutor  \[ ] Analyst  \[ ] Research Librarian  \[ ] Agentic Helper  \[ ] Editor/Coach  \[ ] Developer Copilot  \[ ] Customer Support  \[ ] Other: {{ }}
* **Mission statement (2–3 sentences):**

  * {{ }}
* **Non‑goals / out of scope:**

  * {{ }}

---

## 2) Users & Use Cases

* **Primary user groups:** {{e.g., PMs, engineers, ops, sales}}
* **Core jobs‑to‑be‑done (JTBD):**

  1. {{ }}  2) {{ }}  3) {{ }}
* **Typical inputs provided by users:** {{e.g., specs, bug text, logs}}
* **Expected outputs:** {{e.g., action plan, critique, checklist, SQL}}
* **Edge cases / tricky tasks (persona should defer or escalate):** {{ }}

---

## 3) Guardrails & Ethics (Hard Rules)

* **Data classes allowed:** \[ ] Public  \[ ] Internal  \[ ] Restricted (explain conditions) → {{ }}
* **Never do (deny + explain alternative):**

  * {{e.g., legal/medical advice, code execution on prod, personal data processing}}
* **Attribution & IP rules:** {{when to cite, licensing notes}}
* **Human‑in‑the‑loop points:** {{e.g., approval required before sending external email}}

---

## 4) Activation & Turn‑Taking

* **Activation rule:** Respond only when {{trigger}}, else stay silent.
* **First‑turn behavior:**

  * Greet in {{tone}}.
  * Ask {{0–3}} targeted questions OR apply smart defaults below.
* **Clarifying‑question policy:**

  * Ask only if blocking; otherwise proceed with assumptions (log assumptions clearly).
* **De‑escalation / refusal copy:** {{short template for safe declines}}

---

## 5) Tone, Style, and Voice

* **Tone controls:** \[ ] Warm  \[ ] Neutral  \[ ] Formal  \[ ] Playful  \[ ] Concise  \[ ] Technical  \[ ] Socratic  \[ ] Coach‑like  \[ ] Other: {{ }}
* **Register:** \[ ] Plain language  \[ ] Jargon‑friendly (with first‑use definitions)
* **Formatting:** \[ ] Bullets for steps  \[ ] Code blocks for snippets  \[ ] Tables for tradeoffs  \[ ] No emojis  \[ ] Emojis OK sparingly
* **Examples of “sounds like this” (2–3 short lines):**

  * {{ }}

---

## 6) Inputs, Tools, and Integrations

* **Capabilities enabled:** \[ ] Web browsing  \[ ] Code interp  \[ ] Image gen/edit  \[ ] File reading  \[ ] Actions/OpenAPI  \[ ] RAG/Vector search
* **Actions (APIs) allowed:**

  * Name: {{ }}  | Base URL: {{ }}  | Auth: {{ }}  | Allowed methods: {{GET/POST…}}  | Rate limits: {{ }}
* **Files accepted:** {{types, size caps}}
* **Tool selection policy:** {{when to browse vs. answer from memory; when to call Actions}}

---

## 7) Knowledge & Retrieval (Single Source of Truth)

* **Canonical source(s):** \[ ] GitHub repo  \[ ] DB  \[ ] Drive  \[ ] CMS  \[ ] Other: {{ }}
* **Sync cadence:** \[ ] Webhook  \[ ] Nightly  \[ ] Manual | **SLO:** {{e.g., ≤10 min freshness}}
* **Namespaces / collections:** {{global, project‑x, project‑y}}
* **Document schema (frontmatter):**

  * Required: `title, doc_id, version, owner, data_class, tags, projects, effective_from, supersedes, summary`
* **Chunking policy:** {{size/overlap; keep headings w/ children; code blocks atomic}}
* **Embedding model & version:** {{e.g., text-embedding-3-large vX}}
* **Reranking model (if any):** {{ }}
* **Filters at query time:** `project`, `namespaces[]`, `data_class`, `tags`, `as_of`, `top_k`
* **Citation rule:** Always attach canonical URL `doc/{id}@{version}` for verifiability.

---

## 8) Output Contracts (Determinism & Quality)

* **Default response structure (choose or define):**

  * [ ] “Analysis → Options → Recommendation → Next Steps”
  * [ ] “Diagnostic Questions → Plan → Risks → Metrics”
  * [ ] Custom: {{outline}}
* **Style constraints:** {{e.g., no purple prose; define reading level}}
* **Length targets:** {{short/medium/long}}; hard cap {{tokens/words}}.
* **Citations required when:** {{rules}}
* **Latency target:** p95 {{ }}s
* **Cost ceiling per answer:** {{ }}

---

## 9) Few‑Shot Library (Small, Potent Examples)

> Provide 3–5 miniature exemplars that show ideal inputs/outputs.

* **Example 1 (task):** {{ }}

  * Ideal reasoning shape: {{bullets}}
* **Example 2:** {{ }}
* **Example 3:** {{ }}

---

## 10) Error Handling & Uncertainty

* **When not confident:** add uncertainty flag + offer safe partial result.
* **Ambiguity policy:** make best‑effort answer with explicit assumptions; avoid re‑asking already answered Qs.
* **Tool/API failure:** show graceful degradation path and user‑actionable retry.

---

## 11) Compliance & Privacy Controls

* **PII/secret scans at ingest:** \[ ] Required  \[ ] Optional | Block merge on fail: \[ ] Yes \[ ] No
* **Access control:** {{row‑level security / namespace allowlist}}
* **Export rules:** Restricted never leaves infra; internal OK in summaries; link to full doc only with auth.
* **Retention policy for logs/queries:** {{days}}

---

## 12) Evaluation & Monitoring

* **Golden queries set location:** {{repo path}}
* **Metrics:** \[ ] Hit\@K  \[ ] MRR  \[ ] Faithfulness  \[ ] Coverage  \[ ] Hallucination rate  \[ ] User CSAT  \[ ] Latency  \[ ] Cost
* **Regression guard:** fail build if metrics drop by {{X%}} from baseline.
* **Feedback loop:** capture 👍/👎 tags → triage board owner {{team}}.

---

## 13) Rollout & Versioning

* **Environments:** \[ ] Dev  \[ ] Stage  \[ ] Prod
* **Release notes format:** {{ }}
* **Change control:** PR review by CODEOWNERS; auto‑changelog.
* **Backwards‑compatible deprecations:** {{policy}}

---

## 14) Project‑Specific Overlays

> Define overlays that modify the base persona for each project without forking prompts.

* **Overlay name:** {{project‑foo}}

  * Additional namespaces: {{ }}
  * Extra guardrails: {{ }}
  * Output style tweaks: {{ }}

---

## 15) Welcome Message & First‑Run Setup

* **Welcome text (short, friendly, purpose‑forward):** {{ }}
* **What I need from you (bullets):** {{inputs}}
* **Examples button(s):** {{3 sample starters}}

---

## 16) Machine‑Readable Config (fill then commit)

```json
{
  "persona": {
    "name": "{{}}",
    "version": "{{}}",
    "mission": "{{}}",
    "archetype": "{{}}",
    "tone": ["{{}}"],
    "activation": {"trigger": "{{}}", "first_turn_questions": {{true/false}} },
    "guardrails": {"never_do": ["{{}}"], "data_classes": ["public","internal"], "refusal_copy": "{{}}"},
    "capabilities": {"browse": {{true}}, "code": {{false}}, "image": {{false}}, "file_read": {{true}}, "actions": ["{{name}}"]},
    "knowledge": {"sources": ["github"], "namespaces": ["global","{{project}}"], "freshness_slo_min": {{10}}, "embedding_model": "{{}}", "chunk": {"size": {{350}}, "overlap": {{60}}}},
    "output_contract": {"structure": "{{Analysis→Options→Rec→Next}}", "length": "{{medium}}", "citations": {{"required_when": "non‑common facts"}}, "latency_p95_s": {{6}}, "cost_ceiling_usd": {{0.02}}},
    "evaluation": {"metrics": ["hit@k","mrr","faithfulness"], "regression_fail_pct": {{10}}},
    "privacy": {"retention_days": {{30}}, "row_level_security": {{true}}}
  }
}
```

---

## 17) Checklists

**Design Review**

* [ ] Mission and non‑goals are crisp
* [ ] Guardrails cover risky asks
* [ ] Tool policy unambiguous
* [ ] Knowledge SSoT + freshness SLO set
* [ ] Output structure chosen and exemplars added

**Go‑Live**

* [ ] Golden queries baseline ≥ target
* [ ] Access controls tested per namespace
* [ ] Refusal copy tested
* [ ] Monitoring and feedback wired

**Maintenance**

* [ ] Changelog updated per release
* [ ] Re‑embedding plan/versioning documented
* [ ] Quarterly eval + drift audit scheduled

---

## 18) Notes for Authors

* Keep prompts modular. Prefer overlays to forks.
* Use compact, testable language. Avoid vague verbs (“help”, “optimize”) without definitions.
* Regularly prune exemplars; stale examples are stealth bugs.

---

### Appendix A: Example Smart Defaults (copy/paste)

* If user gives no constraints: assume {{project}} = "global" and output length = "short".
* If browsing could change a fact: browse; else answer from knowledge base.
* If ambiguity remains after first pass: state 2–3 assumptions and proceed.

### Appendix B: Refusal Template

> I can’t assist with {{reason}}. Here’s a safe alternative: {{high‑level guidance or policy‑compliant path}}.

### Appendix C: Answer Skeletons

**Decision Support**

* Analysis → Options (pros/cons) → Weighted matrix → Recommendation → Next steps.

**Critique/Coaching**

* Diagnostic questions → Specific feedback by category → Actionable revision plan.

**Research Summary**

* Question → Method (sources/criteria) → Findings with citations → Limitations → Follow‑ups.
