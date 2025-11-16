# Recruiter Candidate Briefs – Product Requirements Document

## 1. Overview
- **Problem**: Talent teams juggle dozens of candidate profiles across LinkedIn, GitHub, publications, podcasts, and press. Manual research causes inconsistent narratives and slow outreach, especially when candidates update public profiles frequently.
- **Solution**: A recruiter cockpit powered by Parallel Search, Extract, and Task APIs that ingests candidate identifiers, continuously pulls public signals, and outputs standardized, citation-rich briefs viewable in a web app and synced to ATS/CRM systems.

## 2. Goals & Non-Goals
- **Goals**
  1. Produce a high-quality brief in <3 minutes from a LinkedIn URL or email domain.
  2. Refresh briefs weekly (or on-demand) with automatic change tracking and citations.
  3. Deliver export-ready output compatible with Greenhouse/Lever/Workday custom objects.
- **Non-Goals**
  - Automated outreach copy (handled by downstream tools).
  - Background checks / legal vetting.
  - Storing sensitive data beyond user-defined retention windows.

## 3. Target Users
- Sourcers building top-of-funnel lists.
- Recruiters prepping for intake calls.
- Hiring managers needing context before interviews.
- Exec recruiters preparing briefing books for stakeholders.

## 4. Input Interface Requirements
1. **Candidate Intake Form (web app)**
   - Fields: name, LinkedIn URL, GitHub/portfolio/blog links, company, role, priority, tags, preferred refresh cadence.
   - Smart lookup: auto-suggest candidate info when user pastes a URL (pull name/headline instantly).
   - Optional context: job requisition ID, competencies to emphasize (e.g., “LLM research”, “consumer fintech”).
2. **Bulk Upload & API**
   - CSV upload (up to 500 rows) with columns for identifiers; validation results shown inline.
   - REST endpoint to POST candidate payloads from ATS automations.
3. **Scheduling & Alerts**
   - Toggle for auto-refresh frequency (weekly, bi-weekly, manual) per candidate or requisition.
   - Notification routing (Slack/email/webhook) configuration for “brief ready” and “significant change detected.”

## 5. Output & Web Interface Requirements
- **Candidate Brief Page**
  - Hero section with summary, current company/title, location, languages, availability signals.
  - Tabs: `Snapshot` (structured fields), `Recent Activity` (timeline of updates), `Notable Work` (projects, talks, repos), `Risk Flags` (brand-safety or conflicting info), `Sources` (citations with preview snippets).
  - Change badges showing what’s new since last refresh (e.g., “New blog post – 2 days ago”).
- **Export Options**
  - One-click sync to ATS note (JSON via webhook), PDF download, Markdown copy, Slack share card.
  - Hiring manager briefing link with responsive layout for mobile.
- **Collaboration UX**
  - Commenting/mentions for recruiters + hiring managers.
  - Status pills (Drafted, Reviewed, Shared) mirrored to ATS.

## 6. Experience & Workflow
1. Recruiter submits candidate or bulk list via intake tools.
2. Backend spins Parallel Search with objectives tuned to candidate context (e.g., “Surface recent interviews or code contributions by {name}”).
3. Extract fetches referenced URLs (blogs, GitHub repos, podcasts, press). Dedup + store with timestamps.
4. Task API runs with schema capturing `summary`, `experience_snapshot`, `recent_activity`, `notable_work`, `risk_flags`, `citations`. Secondary run creates narrative brief for PDFs.
5. Web app renders structured output, highlights deltas vs. last version, and triggers notifications.
6. Users review, annotate, and sync to ATS or share link with hiring panel. Auto-refresh jobs rerun pipeline and update timeline.

## 7. Functional Requirements
- Candidate entity management with tags, owners, pipeline stage.
- Job orchestration with retry/backoff, cost tracking per candidate.
- Storage of raw artifacts + derived briefs; delta detection for updates.
- Integrations: outbound webhooks (ATS/CRM), Slack notifications, calendar links for interviews.
- Feedback capture (thumbs up/down, edit suggestions) to refine prompts.

## 8. Non-Functional Requirements
- Throughput: ≤50 concurrent briefs with <3 min median completion, <8 min P95.
- Reliability: 99% availability during business hours across regions.
- Security: OAuth SSO, per-workspace RBAC, encryption at rest, audit logs (who viewed/exported briefs).
- Compliance: configurable data retention (default 30 days), GDPR/CCPA deletion workflows.

## 9. Data & Schema
- `candidates`: workspace_id, candidate_id, identifiers{}, stage, owner_id, refresh_cadence, last_brief_at.
- `jobs`: candidate_id, status, started_at, completed_at, api_cost.
- `briefs`: candidate_id, summary, experience_snapshot{}, recent_activity[], notable_work[], risk_flags[], citations[].
- `notifications`: candidate_id, channel, delivered_at.

## 10. Success Metrics
- Median turnaround time (<3 min) & refresh (<2 min).
- % briefs synced to ATS without manual edits (>70%).
- Recruiter CSAT ≥4.5/5; reported prep time reduction ≥60%.
- Weekly active recruiters / total seats >65%.

## 11. Launch Plan
- **Alpha (Weeks 1-3)**: manual intake + JSON output, focus on LinkedIn/GitHub sources, internal recruiters only.
- **Private Beta (Weeks 4-7)**: add UI, PDF export, Slack alerts, limited ATS webhook integration.
- **GA (Weeks 8-12)**: bulk upload/API, change tracking, collaboration features, usage-based billing.

## 12. Risks & Mitigations
- **Outdated/false info**: show timestamps + citations, allow manual suppression of sources, require human approval before sharing.
- **PII handling**: restrict to public data, encrypt storage, honor deletion requests automatically.
- **Rate limits / blocked profiles**: respect robots.txt, allow manual document upload, fallback to user-provided PDFs.

## 13. Open Questions
- Should we parse resumes if recruiters upload them, or keep focus on public web data for v1?
- Do hiring managers need custom brief templates per department?
- What ATS should we prioritize beyond webhooks (Greenhouse vs. Lever vs. Workday)?
