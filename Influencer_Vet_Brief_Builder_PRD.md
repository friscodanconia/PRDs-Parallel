# Influencer Vet + Brief Builder (India) – Product Requirements Document

## 1. Overview
- **Problem**: Indian marketers evaluating creators across Instagram, YouTube, Moj, ShareChat, Josh, LinkedIn, newsletters, and podcasts spend hours collecting scattered data, risk partnering with unsafe voices, and brief agencies with stale info.
- **Solution**: A Parallel-powered workspace that ingests influencer identifiers, automatically researches public signals across India-specific platforms, and produces standardized, citation-rich briefing packs ready for campaign planning.

## 2. Goals & Non-Goals
- **Goals**
  1. Generate a trustworthy multi-platform brief within 5 minutes of submitting a creator handle.
  2. Highlight authenticity, audience fit, and risk factors using live data (last 90 days) across English + key regional languages.
  3. Let marketers compare creators side-by-side and export briefs to agencies or internal tools.
- **Non-Goals**
  - Acting as an influencer marketplace or handling payments.
  - Guaranteeing platform API partnerships—service relies on publicly available data.
  - Managing long-term contracts or campaign execution workflows.

## 3. Target Users
- Brand and growth marketers at Indian D2C, fintech, OTT, food, and mobility companies.
- Agency strategists pitching creator lists to clients.
- Creator economy platforms needing due-diligence overlays.

## 4. Input Interface Requirements
1. **Submission panel** (web app):
   - Fields for creator name, Instagram/YouTube/Moj/Josh URLs, LinkedIn handle, optional keywords ("beauty", "tier-2", etc.), and preferred languages.
   - CSV upload + API endpoint for bulk up to 200 creators; validation checks duplicate handles, unreachable URLs, or private profiles.
   - Campaign context dropdown (product line, launch theme, target region) stored to steer Parallel objectives.
2. **Scheduling controls**:
   - Toggle to auto-refresh briefs weekly or only on-demand.
   - Notification settings (Slack, email) per workspace.

## 5. Output & Web Interface Requirements
- **Brief viewer**: responsive card showing summary, audience snapshot, engagement metrics, standout formats, recent collaborations, risk flags, and citations list—each anchored to source URLs/time.
- **Timeline tab**: chart of engagement spikes mapped to festivals/events (Diwali, IPL etc.).
- **Comparison mode**: select up to 3 creators, align key metrics + textual insights side-by-side with color-coded strengths.
- **Export actions**: Download PDF/PowerPoint-ready brief, copy Markdown/JSON, push to Notion/Google Slides via webhooks.
- **Source explorer**: expandable sections showing raw snippets from Search/Extract output, so users can verify context without leaving the app.

## 6. Experience & Workflow
1. User submits creator info + campaign context.
2. Scheduler launches Parallel Search calls targeting news, blogs, LinkedIn posts, Moj/Josh/ShareChat mentions (via keyword queries), plus YouTube transcript fetches; locale filters applied per language selection.
3. Parallel Extract retrieves selected URLs; dedup + store.
4. Task API runs twice: (a) structured schema (`summary`, `audience_profile`, `engagement_notes`, `risk_flags`, `collab_history`, `content_angles`), (b) narrative brief for export.
5. Web app displays results, notifies stakeholders, and allows feedback tags (accurate / needs fix).
6. Refresh jobs reuse stored identifiers, only fetching deltas since last run to control costs.

## 7. Functional Requirements
- Creator entity CRUD + tagging by product line, region, priority.
- Job orchestration pipeline with retries, platform-specific throttling, caching of Extracted content for 24h.
- Language detection + translation layer (Google/Indic NLP) before feeding into Task API.
- Risk detection heuristics (political keywords, controversial phrases) surfaced in schema.
- Feedback capture (thumbs up/down + comments) feeding prompt tuning backlog.

## 8. Non-Functional Requirements
- Throughput: process 25 creators concurrently with <5 min median latency.
- Availability: 99% during IST business hours.
- Data governance: respect robots.txt, purge stored snippets after 30 days unless user opts to retain.
- Security: OAuth login + SSO, per-workspace RBAC, encryption of API keys and notification tokens.

## 9. Data & Schema
- `creators`: id, handles{}, languages[], categories[], last_refresh_at.
- `jobs`: creator_id, status, started_at, completed_at, cost_estimate, platform_counts.
- `briefs`: creator_id, summary, metrics{}, risk_flags[], citations[], comparison_scores.
- `notifications`: job_id, channel, delivered_at.

## 10. Success Metrics
- Median time to first brief (<5 min) and refresh (<3 min).
- % of briefs exported/shared (proxy for usefulness) >70%.
- Reduction in manual vetting time (self-reported) ≥60%.
- Accuracy CSAT (thumbs-up rate) ≥4.5/5.

## 11. Launch Plan
- **Alpha (Weeks 1-3)**: single-handle intake, manual exports, internal brand beta.
- **Private Beta (Weeks 4-7)**: add bulk upload, comparison view, Hindi + English coverage.
- **GA (Weeks 8-12)**: extend to top 5 regional languages, add Slack/Notion pushes, billing + usage dashboard.

## 12. Risks & Mitigations
- **Platform blocking / rate limits**: rotate search queries, allow manual data uploads when needed.
- **Incomplete vernacular coverage**: prioritize Hindi/Tamil/Telugu first, add user-provided sources to supplement.
- **Hallucinated metrics**: enforce schema with numeric validations, require citations for each claim, show confidence scores.

## 13. Open Questions
- Should we auto-detect fake-follower likelihood via third-party APIs or derive heuristics internally?
- How deep should we go into sentiment on comment threads (requires advanced NLP) for v1?
- Do agencies need white-label exports (remove our branding) at GA?
