# Share-of-Conversation Sentinel (India) – Product Requirements Document

## 1. Overview
- **Problem**: Indian categories (fintech, EVs, OTT, D2C beauty) experience narrative swings driven by regional media, regulators, creators, and vernacular chatter. Teams react late because monitoring is manual and English-only.
- **Solution**: A monitoring and response command center powered by Parallel that ingests competitor + keyword watchlists, continuously scans India-specific sources, clusters emerging narratives, and recommends counter-actions with localized guidance.

## 2. Goals & Non-Goals
- **Goals**
  1. Detect new/accelerating narratives within 2 hours of crossing a relevance threshold.
  2. Provide actionable guidance (earned, owned, paid tactics) tailored to region/language.
  3. Visualize narrative share trends and surface raw evidence for trust.
- **Non-Goals**
  - Becoming a generic social listening tool focused on vanity metrics.
  - Automated media buying; we only recommend tactics.
  - Deep sentiment analysis for every dialect at launch (phased rollout).

## 3. Target Users
- Brand, PR, and comms leads at Indian startups/enterprises.
- Agency war rooms handling multiple clients.
- Growth PMs responsible for narrative-based acquisition.

## 4. Input Interface Requirements
1. **Watchlist Builder**
   - UI wizard to add brands, product keywords, regulatory terms, Hindi/vernacular spellings, and custom boolean rules.
   - Sliders for sensitivity (mentions/day), region focus (national vs. state-level), and priority level.
   - Option to upload CSV of keywords + category tags; API for programmatic setup.
2. **Source Controls**
   - Toggles for media classes: mainstream news (ET, Mint, TOI), business TV transcripts, YouTube channels, LinkedIn posts, ShareChat/Moj/Josh hashtags, Reddit India subs, Quora threads, industry newsletters.
   - Ability to whitelist/blacklist specific domains and add custom RSS or sitemap feeds.
3. **Alert Preferences**
   - Choose channels (Slack, Teams, email, webhook) and quiet hours (IST).
   - Set roles who receive “critical narrative” vs. “daily digest.”

## 5. Output & Web Interface Requirements
- **Narrative Dashboard**: stacked area chart showing share-of-voice per topic over time, filters by region/language/source type.
- **Narrative Cards**: each card includes summary, why it’s spiking, top sources, sentiment tilt, recommended actions (press pitch idea, LinkedIn thought-leadership angle, regional influencer to brief), plus Parallel citations.
- **Evidence Drawer**: click-through to view raw excerpts/snippets, sorted by recency and source credibility, with quick copy buttons.
- **Response Planner**: lightweight board where comms teams assign tasks (draft blog, prep spokesperson) and mark status; integrates with Jira/Asana via webhooks.
- **Digest Emails/Slack Alerts**: formatted with top 3 narratives, share changes, and CTA buttons linking back to dashboard.

## 6. Experience & Workflow
1. User configures watchlists + alert rules.
2. Scheduler runs Parallel Search queries per rule set (Hindi/English/regional keywords) hitting news, regulator releases (RBI, SEBI, PIB), local blogs, ShareChat tags, YouTube transcripts, LinkedIn posts.
3. Extract fetches full articles/posts; dedup and tag by source type + language.
4. Task API clusters mentions into narratives (e.g., “XYZ wallet gains UPI Lite approval”), calculates velocity, sentiment, impacted personas, and crafts recommended playbook.
5. Dashboard updates every hour; alerts fire when narrative velocity surpasses threshold.
6. Users review evidence, assign internal owners, and log response outcomes, feeding back into effectiveness metrics.

## 7. Functional Requirements
- Multi-language keyword expansion + transliteration (e.g., Devanagari ↔ Latin).
- Narrative clustering engine (L2 from Task API output) with manual merge/split controls.
- Versioned history of narrative metrics for trend analysis and export (CSV/JSON).
- Integration hooks: Slack/Teams bots, webhook for BI tools, optional Notion page sync.
- Role-based access + per-client workspaces for agencies.

## 8. Non-Functional Requirements
- Data freshness SLA: <60 min from publication to dashboard for tracked sources.
- Scalability: support 100 concurrent watchlists, 10k documents/day.
- Compliance: respect paywalled content policies, store only summaries for restricted sites.
- Security: SOC2-ready logging, encryption at rest, SSO.

## 9. Data & Schema
- `watchlists`: workspace_id, ruleset, sensitivity, regions, sources[].
- `documents`: url, source_type, language, first_seen_at, embeddings, watchlist_ids[].
- `narratives`: id, label, score, share_percent, velocity, sentiment, recommendations[], citations[].
- `alerts`: narrative_id, severity, delivered_channels, acknowledged_at.

## 10. Success Metrics
- Median detection-to-alert time (<2h) for critical narratives.
- % of narratives with executed response tasks logged (>60%).
- User-reported improvement in narrative preparedness (survey ≥4/5).
- Retention of watchlists (monthly active watchlists / total >80%).

## 11. Launch Plan
- **Alpha (Weeks 1-4)**: English-only, limited sources (ET, Mint, LinkedIn), manual narrative labeling.
- **Private Beta (Weeks 5-8)**: add Hindi + key regional portals, Slack alerts, auto clustering with manual overrides.
- **GA (Weeks 9-12)**: extend to ShareChat/Moj/Josh, add Response Planner + exports, roll out billing + agency workspaces.

## 12. Risks & Mitigations
- **Noise / false positives**: allow user feedback to down-rank sources, include confidence scores.
- **Regulatory content gaps**: partner with data providers or let users upload official PDFs for monitoring.
- **Alert fatigue**: user-tuned sensitivity + digest modes, plus AI summarization to highlight why it matters.

## 13. Open Questions
- Should we integrate ASR for regional YouTube channels at launch or treat as stretch goal?
- How granular should sentiment be (positive/negative vs. multi-class) per language?
- Do agencies need multi-client white-label dashboards on day one?
