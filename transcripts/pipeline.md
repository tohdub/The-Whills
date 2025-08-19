# Pipeline — Generate → Review → Organize → Commit-ready

## Orders
- The Guilds: produce artifacts.
- The Whills: enforce objectives & narrative.
- The Geeks: validators/troubleshooters.
- The Scribes: markdown normalization; tags/backlinks; commit-ready.

## Handoffs (DoD)
1) Generate → Review
   - Frontmatter: title, order=the-guilds, status=draft, owners, links
   - Body: complete draft + 3-bullet acceptance criteria
2) Review → Organize
   - Verdict: approve or revise
   - Notes: 2–3 actionable changes mapped to criteria
   - Status: ready-for-organize
3) Organize → Commit-ready
   - Filename: YYYY-MM-DD_slug.md
   - Tags: #order/<name> #topic/<slug> #status/final|draft
   - Backlinks added; links checked
   - Emit: version.commit.ready (paths + commit message)
