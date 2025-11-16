# PRDs-Parallel: AI-Powered Research Automation Suite

## Overview

This repository contains Product Requirements Documents and implementation planning for three AI-powered research automation products built on the **Parallel API**, targeting the **Indian market**:

1. **Influencer Vet + Brief Builder** - Automated influencer research and vetting across Indian platforms
2. **Recruiter Candidate Briefs** - Automated candidate research and briefing for talent teams
3. **Share-of-Conversation Sentinel** - Real-time narrative monitoring and competitive intelligence

All three products share a common technical foundation and can be developed in parallel or sequentially.

---

## Product Portfolio Summary

| Product | Target Users | Core Value | Launch Timeline |
|---------|-------------|------------|----------------|
| Influencer Vet | Brand marketers, agencies | 5-min multi-platform influencer briefs | 12 weeks |
| Candidate Briefs | Recruiters, hiring managers | 3-min candidate research automation | 12 weeks |
| Conversation Sentinel | PR/Comms teams, growth PMs | 2-hour narrative detection | 12 weeks |

---

## Technical Architecture

### Core Stack (Shared Across All Products)

```
┌─────────────────────────────────────────────────────────┐
│                    Frontend Layer                        │
│  • React/Next.js web application                        │
│  • Responsive UI with dashboard, briefs, comparison     │
│  • Real-time notifications & updates                    │
└─────────────────────────────────────────────────────────┘
                           │
┌─────────────────────────────────────────────────────────┐
│                  API & Orchestration Layer               │
│  • Node.js/Python backend (REST + GraphQL)              │
│  • Job queue (Bull/Celery) for async processing        │
│  • Webhook handlers for integrations                    │
└─────────────────────────────────────────────────────────┘
                           │
┌─────────────────────────────────────────────────────────┐
│                  Parallel API Integration                │
│  • Search API - Multi-source web research              │
│  • Extract API - Content extraction & dedup            │
│  • Task API - Structured analysis & briefs             │
└─────────────────────────────────────────────────────────┘
                           │
┌─────────────────────────────────────────────────────────┐
│                    Data & Storage Layer                  │
│  • PostgreSQL - Entities, jobs, briefs, users          │
│  • Redis - Caching, rate limiting, sessions            │
│  • S3/Cloud Storage - Extracted content, exports       │
└─────────────────────────────────────────────────────────┘
                           │
┌─────────────────────────────────────────────────────────┐
│                  Integration Layer                       │
│  • ATS/CRM webhooks (Greenhouse, Lever, Workday)       │
│  • Slack/Teams bots                                     │
│  • Notion/Google Workspace APIs                         │
│  • Email/SMS notification services                      │
└─────────────────────────────────────────────────────────┘
```

### Technology Recommendations

**Backend:**
- **Framework**: Node.js (Express/Fastify) or Python (FastAPI)
- **Job Queue**: Bull (Node) or Celery (Python) with Redis
- **Language Processing**: Google Cloud Translation API + Indic NLP libraries

**Frontend:**
- **Framework**: Next.js 14+ with TypeScript
- **UI Library**: Tailwind CSS + shadcn/ui or Material-UI
- **State Management**: React Query + Zustand
- **Charts**: Recharts or Chart.js

**Database:**
- **Primary**: PostgreSQL 15+ with JSONB support
- **Cache**: Redis 7+
- **Storage**: AWS S3 or Google Cloud Storage

**Infrastructure:**
- **Hosting**: Vercel (frontend) + AWS/GCP (backend)
- **Container**: Docker + Kubernetes or AWS ECS
- **CI/CD**: GitHub Actions
- **Monitoring**: Datadog/New Relic or open-source (Grafana/Prometheus)

---

## Implementation Roadmap

### Phase 0: Foundation (Weeks 1-2)
**Objective**: Set up shared infrastructure for all products

**Tasks:**
- [ ] Set up monorepo structure (Turborepo or Nx)
- [ ] Configure development environments
- [ ] Establish PostgreSQL schema (multi-tenant architecture)
- [ ] Integrate Parallel API SDK
- [ ] Build authentication & authorization (OAuth SSO)
- [ ] Set up job orchestration framework
- [ ] Create CI/CD pipelines
- [ ] Configure monitoring & logging
- [ ] Implement rate limiting & cost tracking

**Deliverables:**
- Working development environment
- Database migrations & seed data
- Parallel API integration working
- Basic user authentication flow

---

### Product 1: Influencer Vet + Brief Builder

#### Alpha (Weeks 3-5)

**Scope:**
- Single-handle manual intake
- Instagram + YouTube coverage only
- English language support
- Basic brief viewer UI
- Manual PDF export
- Internal team testing only

**Implementation Tasks:**
1. **Data Models** (Week 3)
   - `creators` table with handles, categories, languages
   - `jobs` table for Parallel API orchestration
   - `briefs` table for structured output

2. **Backend Services** (Week 3-4)
   - Creator intake endpoint
   - Parallel Search integration for Instagram/YouTube
   - Parallel Extract pipeline for content retrieval
   - Parallel Task API for structured brief generation
   - Manual export service (PDF generation)

3. **Frontend** (Week 4-5)
   - Creator submission form
   - Brief viewer with tabs (summary, metrics, citations)
   - Export button
   - Admin dashboard for job monitoring

**Alpha Success Criteria:**
- Generate brief for single creator in <5 minutes
- 100% of briefs have valid citations
- PDF export works correctly

#### Private Beta (Weeks 6-8)

**Scope:**
- CSV bulk upload (up to 200 creators)
- Add Moj, ShareChat, Josh, LinkedIn coverage
- Hindi + English language support
- Comparison mode (up to 3 creators)
- Notion/Google Slides export
- 10-20 external beta testers

**Implementation Tasks:**
1. **Enhanced Backend** (Week 6)
   - Bulk upload parser & validator
   - Multi-platform search strategies
   - Language detection & translation layer
   - Comparison score calculation
   - Webhook integrations (Notion, Google Slides)

2. **Advanced Features** (Week 7)
   - Timeline visualization (engagement vs. events)
   - Risk detection heuristics
   - Source explorer with raw snippets
   - Auto-refresh scheduling

3. **Beta Readiness** (Week 8)
   - Feedback collection system
   - Usage analytics
   - Performance optimization
   - Beta tester onboarding flow

**Beta Success Criteria:**
- Process 25 creators concurrently
- <5 min median latency
- 70% of briefs exported/shared
- Beta tester CSAT >4/5

#### GA (Weeks 9-12)

**Scope:**
- Top 5 regional languages (Hindi, Tamil, Telugu, Bengali, Marathi)
- Slack notifications
- Weekly auto-refresh
- Billing & usage dashboard
- Full customer onboarding

**Implementation Tasks:**
1. **Scale & Polish** (Week 9-10)
   - Multi-language NLP pipeline
   - Advanced caching strategies
   - Cost optimization
   - Security hardening (SOC2 prep)

2. **Billing & Ops** (Week 10-11)
   - Stripe integration
   - Usage metering & limits
   - Customer workspace management
   - Admin panel for support

3. **Launch Prep** (Week 11-12)
   - Documentation & help center
   - Marketing site
   - Customer success playbooks
   - GA launch checklist

**GA Success Criteria:**
- 99% uptime during IST business hours
- Accuracy CSAT ≥4.5/5
- 60% reduction in manual vetting time (self-reported)

---

### Product 2: Recruiter Candidate Briefs

#### Alpha (Weeks 3-5)

**Scope:**
- Manual intake via web form
- LinkedIn + GitHub sources only
- JSON output (no UI brief viewer yet)
- Internal recruiters only

**Implementation Tasks:**
1. **Data Models** (Week 3)
   - `candidates` table with identifiers, stage, refresh cadence
   - `jobs` table for orchestration
   - `briefs` table with structured candidate data

2. **Backend Services** (Week 3-4)
   - Candidate intake endpoint with LinkedIn URL parsing
   - Parallel Search for LinkedIn posts, GitHub repos, publications
   - Parallel Extract for blog posts, podcasts, press mentions
   - Task API with schema for `summary`, `experience_snapshot`, `recent_activity`, `notable_work`, `risk_flags`, `citations`

3. **Basic Frontend** (Week 4-5)
   - Candidate submission form
   - Job status monitor
   - JSON output viewer

**Alpha Success Criteria:**
- Generate brief in <3 minutes
- 100% briefs have LinkedIn + GitHub data
- Valid JSON schema output

#### Private Beta (Weeks 6-8)

**Scope:**
- Full brief viewer UI
- PDF export
- Slack alerts
- Limited ATS webhook (Greenhouse or Lever)
- Change tracking on refresh
- 10-15 external recruiting teams

**Implementation Tasks:**
1. **UI Development** (Week 6)
   - Candidate brief page with tabs
   - Timeline of recent activity
   - Change badges (delta highlighting)
   - Export options (PDF, Markdown, ATS sync)

2. **Integrations** (Week 7)
   - Slack notification system
   - Greenhouse/Lever webhook implementation
   - Auto-refresh scheduler
   - Delta detection algorithm

3. **Collaboration Features** (Week 8)
   - Comments & mentions
   - Status tracking (Drafted, Reviewed, Shared)
   - Hiring manager share links

**Beta Success Criteria:**
- <3 min median, <8 min P95 completion time
- 70% of briefs synced to ATS without edits
- Beta tester CSAT ≥4/5

#### GA (Weeks 9-12)

**Scope:**
- Bulk upload & REST API
- All major ATS integrations (Greenhouse, Lever, Workday)
- Usage-based billing
- Full collaboration suite

**Implementation Tasks:**
1. **API & Scale** (Week 9-10)
   - REST API with auth
   - Bulk CSV upload (500 rows)
   - Multi-ATS connector framework
   - Performance optimization

2. **Enterprise Features** (Week 10-11)
   - SSO & RBAC
   - Audit logs
   - GDPR/CCPA deletion workflows
   - Data retention controls

3. **Launch** (Week 11-12)
   - Billing integration
   - Customer documentation
   - Support playbooks
   - GA marketing

**GA Success Criteria:**
- Weekly active recruiters >65% of seats
- Prep time reduction ≥60%
- Recruiter CSAT ≥4.5/5

---

### Product 3: Share-of-Conversation Sentinel

#### Alpha (Weeks 3-6)

**Scope:**
- English-only monitoring
- Limited sources (ET, Mint, LinkedIn)
- Manual narrative labeling
- Basic dashboard
- Internal brand beta

**Implementation Tasks:**
1. **Data Models** (Week 3)
   - `watchlists` table with rulesets, keywords, regions
   - `documents` table for tracked content
   - `narratives` table for clusters
   - `alerts` table for notifications

2. **Monitoring Pipeline** (Week 3-5)
   - Watchlist rule engine
   - Scheduled Parallel Search queries
   - Document extraction & deduplication
   - Manual narrative clustering interface

3. **Dashboard V1** (Week 5-6)
   - Narrative cards with summaries
   - Evidence drawer with source snippets
   - Share-of-voice chart (basic)
   - Alert configuration panel

**Alpha Success Criteria:**
- Detect narratives from 3 sources
- <60 min data freshness
- Manual clustering works for 20+ documents

#### Private Beta (Weeks 7-10)

**Scope:**
- Hindi + key regional sources
- Slack/Teams alerts
- Auto-clustering with manual overrides
- Timeline visualization
- 5-10 brand/agency beta testers

**Implementation Tasks:**
1. **Language Expansion** (Week 7-8)
   - Multi-language keyword expansion
   - Transliteration support (Devanagari ↔ Latin)
   - Regional news sources integration
   - Language-specific sentiment

2. **Auto-Clustering** (Week 8-9)
   - Task API narrative clustering
   - Velocity & sentiment calculation
   - Recommendation engine (earned/owned/paid tactics)
   - Confidence scoring

3. **Alerts & Integrations** (Week 9-10)
   - Slack/Teams bot
   - Email digest formatting
   - Webhook for BI tools
   - Alert threshold tuning

**Beta Success Criteria:**
- <2 hour detection-to-alert time
- Auto-clustering accuracy >75%
- Beta tester preparedness rating ≥4/5

#### GA (Weeks 11-14)

**Scope:**
- ShareChat/Moj/Josh integration
- YouTube ASR for regional channels
- Response Planner module
- Agency workspaces
- Billing

**Implementation Tasks:**
1. **Platform Expansion** (Week 11)
   - ShareChat/Moj/Josh API/scraping
   - YouTube transcript extraction
   - Reddit India & Quora integration

2. **Response Planner** (Week 12)
   - Task assignment board
   - Jira/Asana integration
   - Response tracking & effectiveness metrics

3. **Multi-Tenancy & Billing** (Week 13)
   - Agency workspace isolation
   - White-label dashboard options
   - Usage-based billing
   - Cost allocation per watchlist

4. **Launch** (Week 14)
   - Documentation
   - Customer success training
   - Marketing & sales enablement

**GA Success Criteria:**
- Support 100 concurrent watchlists
- 80% monthly active watchlist retention
- 60% of narratives have logged response tasks

---

## Shared Infrastructure Components

### Authentication & Authorization
- OAuth 2.0 / OIDC integration (Google, Microsoft)
- JWT-based session management
- RBAC with workspace-level permissions
- SSO for enterprise customers (SAML)

### Job Orchestration
- Priority queue (critical, high, normal, low)
- Retry logic with exponential backoff
- Dead letter queue for failed jobs
- Cost tracking per job
- Parallel API rate limit management

### Notification System
- Multi-channel delivery (Slack, Teams, Email, Webhook)
- Template engine for messages
- Delivery status tracking
- User preferences & quiet hours

### Export Engine
- PDF generation (Puppeteer or wkhtmltopdf)
- Markdown/JSON formatters
- PowerPoint/Google Slides API integration
- Webhook delivery for ATS/CRM systems

### Language Processing
- Google Cloud Translation API integration
- Indic NLP library for vernacular languages
- Language detection
- Transliteration utilities

### Monitoring & Observability
- Application metrics (latency, throughput, errors)
- Parallel API usage & cost tracking
- User activity analytics
- Alerting for SLA violations

---

## Development Approach

### Option 1: Sequential Launch
**Timeline**: 36 weeks total (12 weeks per product)

**Pros:**
- Focus entire team on one product at a time
- Faster time-to-market for first product
- Learn from each launch before next

**Cons:**
- Longer total timeline
- Delayed revenue from other products

**Recommended if:**
- Small team (<5 engineers)
- Limited Parallel API budget
- Want to validate market fit first

---

### Option 2: Parallel Development
**Timeline**: 14 weeks total (all products in parallel)

**Approach:**
- Weeks 1-2: Shared foundation (entire team)
- Weeks 3-12: Three parallel tracks (split team)
  - Track A: Influencer Vet (2 engineers)
  - Track B: Candidate Briefs (2 engineers)
  - Track C: Conversation Sentinel (2 engineers)
  - Shared: 1 frontend engineer, 1 DevOps engineer
- Weeks 13-14: Integration & launch prep (entire team)

**Pros:**
- Fastest time-to-market for all three
- Maximize revenue opportunity
- Shared infrastructure amortized

**Cons:**
- Requires larger team (7+ engineers)
- Higher coordination overhead
- Greater initial Parallel API spend

**Recommended if:**
- Team ≥7 engineers
- Sufficient capital for parallel development
- High confidence in all three product directions

---

### Option 3: Staged Parallel (Recommended)
**Timeline**: 18 weeks total

**Approach:**
- Weeks 1-2: Foundation (entire team)
- Weeks 3-8: Start with Product 1 (Influencer) + Product 2 (Recruiter) in parallel
  - 3 engineers on Influencer (Alpha → Beta)
  - 3 engineers on Recruiter (Alpha → Beta)
  - 1 shared frontend, 1 DevOps
- Weeks 9-14: Add Product 3 (Sentinel) while polishing 1 & 2
  - 2 engineers finish Influencer (GA prep)
  - 2 engineers finish Recruiter (GA prep)
  - 3 engineers start Sentinel (Alpha → Beta)
- Weeks 15-18: Final integration & launch (entire team)

**Pros:**
- Balanced timeline vs. team size
- Learn from first two before third
- Manageable complexity
- Earlier revenue from first two products

**Cons:**
- Requires coordination across teams
- Some engineers switch contexts mid-project

**Recommended if:**
- Team of 6-8 engineers
- Moderate budget constraints
- Want balance between speed and risk

---

## Database Schema (Core Tables)

```sql
-- Multi-tenant workspace
CREATE TABLE workspaces (
  id UUID PRIMARY KEY,
  name VARCHAR(255),
  plan VARCHAR(50), -- free, pro, enterprise
  created_at TIMESTAMP,
  settings JSONB
);

-- Users
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR(255) UNIQUE,
  name VARCHAR(255),
  created_at TIMESTAMP
);

-- User-Workspace relationship
CREATE TABLE workspace_members (
  workspace_id UUID REFERENCES workspaces(id),
  user_id UUID REFERENCES users(id),
  role VARCHAR(50), -- admin, member, viewer
  PRIMARY KEY (workspace_id, user_id)
);

-- Influencer Product
CREATE TABLE creators (
  id UUID PRIMARY KEY,
  workspace_id UUID REFERENCES workspaces(id),
  name VARCHAR(255),
  handles JSONB, -- {instagram, youtube, linkedin, etc.}
  categories TEXT[],
  languages TEXT[],
  refresh_cadence VARCHAR(50),
  last_refresh_at TIMESTAMP,
  created_at TIMESTAMP
);

-- Recruiter Product
CREATE TABLE candidates (
  id UUID PRIMARY KEY,
  workspace_id UUID REFERENCES workspaces(id),
  name VARCHAR(255),
  identifiers JSONB, -- {linkedin_url, github_url, email, etc.}
  stage VARCHAR(100),
  owner_id UUID REFERENCES users(id),
  refresh_cadence VARCHAR(50),
  last_brief_at TIMESTAMP,
  created_at TIMESTAMP
);

-- Sentinel Product
CREATE TABLE watchlists (
  id UUID PRIMARY KEY,
  workspace_id UUID REFERENCES workspaces(id),
  name VARCHAR(255),
  ruleset JSONB, -- keywords, regions, sources, sensitivity
  is_active BOOLEAN,
  created_at TIMESTAMP
);

-- Shared: Jobs table
CREATE TABLE jobs (
  id UUID PRIMARY KEY,
  workspace_id UUID REFERENCES workspaces(id),
  entity_type VARCHAR(50), -- creator, candidate, watchlist
  entity_id UUID,
  status VARCHAR(50), -- pending, running, completed, failed
  started_at TIMESTAMP,
  completed_at TIMESTAMP,
  api_cost_usd DECIMAL(10, 4),
  metadata JSONB,
  error TEXT
);

-- Shared: Briefs/Output table
CREATE TABLE briefs (
  id UUID PRIMARY KEY,
  entity_type VARCHAR(50),
  entity_id UUID,
  version INT,
  content JSONB, -- structured output from Task API
  narrative TEXT, -- formatted narrative
  citations JSONB,
  created_at TIMESTAMP
);

-- Shared: Notifications
CREATE TABLE notifications (
  id UUID PRIMARY KEY,
  workspace_id UUID REFERENCES workspaces(id),
  job_id UUID REFERENCES jobs(id),
  channel VARCHAR(50), -- slack, email, webhook
  payload JSONB,
  delivered_at TIMESTAMP,
  acknowledged_at TIMESTAMP
);
```

---

## Security & Compliance Checklist

- [ ] OAuth 2.0 / SSO implementation
- [ ] JWT token validation & rotation
- [ ] RBAC with workspace isolation
- [ ] Encryption at rest (database, file storage)
- [ ] Encryption in transit (TLS 1.3)
- [ ] API key management (secrets manager)
- [ ] Rate limiting per workspace
- [ ] Audit logging (who accessed what, when)
- [ ] GDPR compliance (data deletion, export)
- [ ] CCPA compliance
- [ ] Data retention policies
- [ ] Security headers (CSP, HSTS, etc.)
- [ ] Input validation & sanitization
- [ ] OWASP Top 10 mitigation
- [ ] Dependency vulnerability scanning
- [ ] SOC 2 Type II preparation (for enterprise sales)

---

## Cost Estimation & Budget Planning

### Parallel API Costs (Estimated per Product)

**Influencer Vet:**
- Search: ~500 searches/day × $0.05 = $25/day
- Extract: ~2000 extracts/day × $0.02 = $40/day
- Task: ~500 tasks/day × $0.10 = $50/day
- **Total**: ~$115/day = $3,450/month at moderate scale

**Recruiter Briefs:**
- Search: ~300 searches/day × $0.05 = $15/day
- Extract: ~1200 extracts/day × $0.02 = $24/day
- Task: ~300 tasks/day × $0.10 = $30/day
- **Total**: ~$69/day = $2,070/month

**Conversation Sentinel:**
- Search: ~1000 searches/day × $0.05 = $50/day
- Extract: ~5000 extracts/day × $0.02 = $100/day
- Task: ~500 tasks/day × $0.10 = $50/day
- **Total**: ~$200/day = $6,000/month

**Combined Monthly Parallel API Budget**: ~$11,500/month at moderate scale

### Infrastructure Costs (Estimated)

- **Hosting**: $500-1000/month (AWS/GCP)
- **Database**: $200-500/month (managed PostgreSQL)
- **Storage**: $100-300/month (S3/GCS)
- **Monitoring**: $200-400/month (Datadog or equivalent)
- **Translation API**: $500-1000/month (Google Cloud Translation)
- **Email/SMS**: $100-200/month (SendGrid, Twilio)

**Total Infrastructure**: ~$1,600-3,400/month

**Grand Total Operating Cost**: ~$13,100-14,900/month

---

## Success Metrics Dashboard

### Product Health Metrics
- Daily active workspaces
- Jobs processed per day
- Success rate (completed / total jobs)
- Median completion time
- P95 completion time
- API cost per brief
- Error rate by error type

### User Engagement Metrics
- Briefs generated per workspace
- Export/share rate
- Auto-refresh adoption rate
- Comparison usage (Influencer product)
- ATS sync rate (Recruiter product)
- Alert acknowledgment rate (Sentinel product)

### Business Metrics
- Monthly Recurring Revenue (MRR)
- Customer Acquisition Cost (CAC)
- Lifetime Value (LTV)
- Churn rate
- Net Revenue Retention (NRR)
- Usage-based revenue per customer

### Quality Metrics
- Customer Satisfaction (CSAT) score
- Net Promoter Score (NPS)
- Feedback thumbs-up rate
- Time saved (self-reported)
- Support ticket volume

---

## Next Steps

1. **Review this plan** with your team and stakeholders
2. **Fill out** `REQUIRED_INFORMATION.md` with your specific details
3. **Choose a development approach** (Sequential, Parallel, or Staged)
4. **Assemble your team** and assign track leads
5. **Set up Parallel API access** and test integration
6. **Begin Phase 0** (Foundation) development
7. **Schedule weekly syncs** to track progress

---

## Questions or Feedback?

This is a living document. As you gather more information and make decisions, update this README with:
- Chosen tech stack details
- Team assignments
- Timeline adjustments
- Integration specifics
- Launch dates

Refer to `Build_Kickoff_Inputs.md` for detailed pre-implementation checklist and `REQUIRED_INFORMATION.md` for what information you need to provide.
