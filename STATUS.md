# ai-governance.dk — project status

**Last updated:** 2026-06-01 (deploy + audit-driven refresh + dashboard viz + search upgrade)

## At a glance

| | |
|---|---|
| **Live URL** | https://ai-governance.dk (DNS propagated; Let's Encrypt cert provisioning in flight at last check — site reachable on HTTP, HTTPS auto-completes within ~30 min of DNS resolve) |
| **Netlify site** | ai-governance.netlify.app |
| **GitHub repo** | https://github.com/solution8-com/ai-governance |
| **Brand color** | Royal blue HSL(220°, 70%, 55%) ≈ #3C78E6 |
| **Topic** | "How do I run AI responsibly inside an organization?" (governance, broader than compliance) |
| **Status** | 🟢 Live — initial deploy 2026-06-01, content review cycles deferred to post-launch |

## Where we are

Build phase: ✅ Done (data file, Index.tsx, branding, favicon, og-image, SEO, build verified)
Review phase: ⏸ Deferred — Jacob signed off on outline; concrete content review will happen post-launch with the live site as the artifact
Deploy phase: ✅ Done — GitHub push, transferred to solution8-com, Netlify connected, GoDaddy DNS migrated, HTTPS provisioning auto

## Deploy facts

- **DNS migration:** GoDaddy A `@ → 75.2.60.5` + CNAME `www → ai-governance.netlify.app`. Migrated 2026-06-01.
- **Initial cert:** Let's Encrypt issued by Netlify after DNS resolved. Wildcard `*.netlify.app` cert visible briefly during provisioning.
- **Auto-deploy:** every `git push` to `main` triggers a Netlify rebuild — no manual deploy needed.

## Content scope

- **3 pillars:**
  1. **Organisering & Strategi** — roles, structure, policies, literacy, ethics (5 categories, 18 subcategories)
  2. **Udvikling & Leverance** — use case lifecycle → vendor → agent design → testing (5 categories, 21 subcategories)
  3. **Drift & Vedligehold** — monitoring, incidents, retraining, agent runtime, FinOps, audit (6 categories, 24 subcategories)
- **16 categories**
- **63 sub-items** total
- Cross-cutting theme: **agent & skill governance** — has its own dedicated category in each pillar (1.4, 2.4, 3.4). Category 3.4 (Agent runtime-governance) is the deepest single category at 6 subcategories — this is the site's differentiator vs. compliance/sikkerhed.

### Frameworks woven in
NIST AI RMF + GenAI Profile (AI 600-1) · ISO/IEC 42001 · ISO/IEC 23894 · EU AI Act (articles 4, 9, 10, 11, 12, 14, 15, 17, 26, 27, 50, 73) · OECD AI Principles (2024) · Council of Europe Framework Convention · Microsoft Responsible AI Standard v2 · Google SAIF · Anthropic Responsible Scaling Policy v3 · OWASP LLM Top 10 + Agentic Top 10 2026 + Agentic Security Initiative · MITRE ATLAS · Gartner AI TRiSM · MIT AI Risk Repository · WEF Presidio · CSA Non-Human Identity / Agentic AI Governance · Singapore AI Verify Foundation · FinOps for AI · MCP Authorization spec · Digitaliseringsstyrelsen · Datatilsynet · Finanstilsynet · DI strategic AI guide · GDPR.

## Key decisions locked in with Jacob

| Decision | Outcome |
|---|---|
| Pillar 2 naming: "Muligheder & Udvikling" vs "Udvikling & Leverance" | **"Udvikling & Leverance"** — signals lifecycle ownership over ideation |
| Agent governance treatment: cross-cutting or 4th pillar? | **Cross-cutting** — one dedicated category per pillar (1.4, 2.4, 3.4). 3 pillars total, parallel to sikkerhed/compliance. |
| Volume: ~90 sub-items target | Landed at 63 — comprehensive but not overstuffed. Can expand later. |

## Key technical bits

- **Stack:** Vite + React + TS + Tailwind + shadcn/ui (cloned from ai-compliance template)
- **Data file:** `src/data/governanceData.ts` — domain-neutral types (matches compliance)
- **`SourceType` union:** 22 source types covering all frameworks
- **`getSourceBadgeClass` in Index.tsx:** color-coded by family (regulatory blue / standards cyan / industry amber / security red)
- **CTAs:** MailerLite form (shared with sikkerhed/compliance for now) + Calendly
- **Header reference links:** NIST AI RMF + ISO 42001 (replaced compliance's Digst + Datatilsynet — governance audience leans more on these)
- **6 source cards on dashboard:** NIST AI RMF, ISO/IEC 42001, EU AI Act, OWASP Agentic Top 10, OECD AI Principles, Microsoft RAI Standard v2

## Brand color rationale

The AI Governance logo's accent triangle is `#1E2A44` (HSV 221°, 55%, 26%) — a deep navy that's too dark to use directly on the site's dark navy background. Brightened to HSL(220°, 70%, 55%) — same hue family, vibrant enough to function as a UI accent on dark bg. This matches the approach taken with sikkerhed (logo orange → UI orange) and compliance (logo teal → UI teal).

## Build commands

```bash
npm install
npm run dev -- --port 8082
npm run build
```

## Audit-driven refresh (2026-06-01)

Web-verified `[verify]` items from the original research; updated source currency. All shipped in commit b805f49:

- **MCP_AUTH** — was pointing at `blog.modelcontextprotocol.io/` (blog landing). Replaced with canonical spec URL `https://modelcontextprotocol.io/specification/2026-03-15/basic/authorization`.
- **Anthropic RSP** — site cited "v3"; current is **v3.1** (released 2 April 2026). Updated label in 4 places. URL updated to canonical `https://www.anthropic.com/responsible-scaling-policy`.
- **Anthropic agent safety framework** (Aug 2025) — added as `ANTHROPIC_AGENT_FRAMEWORK` constant, cited in 3.4 `human-oversight-skala` alongside EU AI Act art. 14.
- **IIA AI Auditing Framework** (Sept 2024 update) — added as new `SourceType` ("IIA") + URL constant. Cited in 1.2 `tre-linjer` as the canonical 3LoD-for-AI reference. `getSourceBadgeClass` in Index.tsx extended to render IIA as industry-amber.
- **Finanstilsynet 1.2 tre-linjer source** — swapped PDF (`FINANSTILSYNET_AI`) for durable landing page `FINANSTILSYNET_GODPRAKSIS`.
- **DS 42001** — added `DS_42001` constant (Danish Standard adoption of ISO/IEC 42001:2023) for future Danish-context citations.
- **ISO/IEC 42005:2025** — added `ISO_42005` constant for future citations.
- **energi-co2** — severity bumped low → medium; description corrected: CSRD/ESRS E1 currently lacks AI-specific requirements but Scope 1-3 captures AI energy, and ESRS revisions for FY 2027 expected to add AI-specific reporting.
- **"SOC 2 for AI"** — fixed to "ISO/IEC 42001-certificering kombineret med SOC 2 / ISO 27001 (med AI-scope)".

`[verify]` items that did NOT need changes:
- Dansk Standard ISO 42001 adoption confirmed.
- IIA AI auditing framework: confirmed current Sept 2024 update.
- CSRD ESRS E1: confirmed no AI-specific reporting requirements yet — wording corrected to reflect this.
- Finanstilsynet most recent AI bulletin: still May 2024 god-praksis guidance; no 2025/2026 update yet.

## Post-launch items

- [ ] LinkedIn og-image preview test (use Post Inspector with cache-bust `?v=2`)
- [ ] Eventually: create governance-specific MailerLite form (currently shares form with compliance + sikkerhed). Swap `MAILERLITE_ACTION` in `src/pages/Index.tsx`.

## Identified content gaps (next round)

From audit — not yet shipped:

**Agent governance depth (the differentiator):**
- [ ] **Add 1.4.5 `a2a-policy` subcategory** — A2A is now Linux Foundation project (April 2025 Google donation). Cross-org agent communication policy, mutual auth via Verifiable Credentials, data flow review per A2A skill.
- [ ] **2.4: Add sandboxing/isolation as its own subcategory** — currently buried in `plan-validering` action 4. Container/microVM isolation is 2026 baseline.
- [ ] **2.4: Add agent observability** (OpenTelemetry GenAI semconv, released stable 2025) — completely missing.
- [ ] **2.4: Add agent evaluation harnesses** (agent-evals, distinct from model-evals).
- [ ] **3.4: Add agent rate-limiting at MCP/tool layer** — distinct from token cost.
- [ ] **3.4: Memory poisoning detection** — enhance `agent-memory` with poisoning-detection action.
- [ ] **3.4: Expand to enumerate non-MS/Anthropic platforms** in 1.4.1: n8n, Zapier AI agents, LangGraph, CrewAI.
- [ ] **3.4.6: Add tooling examples** — Microsoft Defender for Cloud Apps + Purview for agent DLP.

**Other governance gaps:**
- [ ] Open-source vs proprietary model decision framework
- [ ] Fine-tuning vs RAG vs prompt engineering governance differences
- [ ] EU AI Act art. 43 Conformity Assessment as dedicated subcategory
- [ ] AI-generated code governance (provenance, attribution, IP)
- [ ] Vendor model deprecation as its own subcategory
- [ ] Continuous EU AI Act re-classification monitoring
- [ ] AI-related M&A/divestment governance (art. 25 provider/deployer transfer)
- [ ] AI liability insurance coverage
- [ ] Public-sector specific: Digst FOTU/sagsbehandling guidance

**Visualizations:**
- [ ] AI governance operating model diagram (top of Pillar 1)
- [ ] Agent decision-class matrix (inside 1.4.4 `beslutnings-graenser`)
- [ ] Framework relationships diagram (NIST ↔ ISO ↔ EU AI Act ↔ OECD ↔ CoE)
- [ ] AI use case lifecycle Sankey (top of Pillar 2)
- [ ] Agent runtime control plane diagram (top of 3.4) — marquee visual
- [ ] Maturity radar/self-assessment tool (3.6 `modenhed`) — engagement magnet

## Items flagged `[verify]` during research

These are likely correct but were not web-verified during the research session (already noted by the research agent):
- Dansk Standard ISO 42001 adoption status
- IIA AI auditing framework current version (referenced briefly)
- CSRD ESRS E1 AI-specific reporting requirements (referenced in FinOps category)
- Finanstilsynet's latest AI bulletin

Worth a quick web check before final deploy.

## Files to inspect for review

When reviewing content, the heaviest files:
- `src/data/governanceData.ts` — all 63 subcategories. Suggested spot-checks:
  - Category 3.4 `agent-runtime` (6 subcats) — the marquee category
  - Category 1.4 `agent-skill-org` (4 subcats) — organizational angle on agents
  - Category 1.2 `roller-ansvar` (4 subcats) — AI Council / Model Owner / 3-line defense / whistleblower

## Next-session quick start

```bash
cd /Users/jacobsmacbookair/projects/websites/onepagers/ai-governance
npm run dev -- --port 8082
# Open http://localhost:8082
```

Open browsers tabs side-by-side with the other two sites to compare visual consistency:
- localhost:8080 → compliance (teal)
- localhost:8081 → sikkerhed (orange)
- localhost:8082 → governance (royal blue)
