# PRDs-Parallel: AI-Powered Research Automation Suite

## Solo Developer Edition

This repository contains Product Requirements Documents for three AI-powered research automation products built on the **Parallel API**, targeting the **Indian market**.

**Important**: This guide is optimized for a **solo developer** building these products. The approach prioritizes:
- MVP-first strategy
- Simple, proven tech stack
- Sequential development (one product at a time)
- Getting to revenue quickly
- Avoiding over-engineering

---

## The Three Products

| Product | Target Users | Core Value | Complexity | Revenue Potential |
|---------|-------------|------------|------------|------------------|
| **Recruiter Candidate Briefs** | Recruiters, hiring managers | 3-min candidate research | ⭐⭐ Low | ⭐⭐⭐ High |
| **Influencer Vet + Brief Builder** | Brand marketers, agencies | 5-min influencer briefs | ⭐⭐⭐ Medium | ⭐⭐⭐⭐ High |
| **Share-of-Conversation Sentinel** | PR/Comms teams | 2-hour narrative detection | ⭐⭐⭐⭐ High | ⭐⭐⭐ Medium |

---

## Solo Developer Strategy: Which Product to Build First?

### Recommendation: Start with **Recruiter Candidate Briefs**

**Why this product first:**
1. **Simplest scope** - Just 2 main sources (LinkedIn + GitHub)
2. **Clear user flow** - Input URL → Get brief → Export
3. **Fastest to MVP** - Can launch in 4-6 weeks
4. **Proven market** - Recruiters pay for time-saving tools
5. **Easy validation** - Show to 5 recruiters, get feedback immediately
6. **Lower API costs** - Fewer searches per brief than other products

**After validation, build:**
- **Option A**: Influencer Vet (if Recruiter product shows traction)
- **Option B**: Pivot to one of the others if market feedback suggests it

---

## MVP Tech Stack (Solo Developer Friendly)

Keep it simple. Use tools you know or can learn quickly.

### Frontend
- **Framework**: Next.js 14 with TypeScript
- **UI**: Tailwind CSS + shadcn/ui (copy-paste components)
- **Forms**: React Hook Form + Zod validation
- **State**: Built-in React hooks (no Redux/Zustand needed for MVP)
- **Deployment**: Vercel (free tier, zero config)

### Backend
- **Framework**: Next.js API Routes (same repo as frontend)
- **Alternative**: If you prefer Python, use FastAPI
- **Job Queue**: Start with simple polling, add BullMQ later if needed
- **File Storage**: Vercel Blob or Cloudflare R2

### Database
- **Primary**: PostgreSQL via Vercel Postgres or Supabase (generous free tier)
- **ORM**: Prisma (TypeScript) or Drizzle ORM
- **Alternative**: If you prefer Python, use SQLAlchemy

### Authentication
- **Start**: Simple email/password with NextAuth.js
- **Later**: Add OAuth (Google) when you have paying customers

### Payments
- **Stripe** - Industry standard, great docs, start with Checkout (easiest)

### Monitoring
- **Free tier**: Vercel Analytics + Sentry for errors
- **Upgrade later**: PostHog (product analytics) when you have users

### Parallel API Integration
- **SDK**: Use Parallel's official SDK (Node.js or Python)
- **Rate limiting**: Simple in-memory counter initially, Redis later

---

## MVP Architecture (Recruiter Candidate Briefs)

```
┌─────────────────────────────────────────┐
│         Next.js Application             │
│  ┌───────────────────────────────────┐  │
│  │  Frontend (React Components)      │  │
│  │  - Candidate input form           │  │
│  │  - Brief viewer                   │  │
│  │  - Export buttons                 │  │
│  └───────────────────────────────────┘  │
│  ┌───────────────────────────────────┐  │
│  │  API Routes                       │  │
│  │  /api/candidates/create           │  │
│  │  /api/briefs/generate             │  │
│  │  /api/briefs/export               │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
                  │
                  ▼
        ┌─────────────────┐
        │ Vercel Postgres │
        │ - candidates    │
        │ - briefs        │
        │ - users         │
        └─────────────────┘
                  │
                  ▼
         ┌────────────────┐
         │  Parallel API  │
         │  - Search      │
         │  - Extract     │
         │  - Task        │
         └────────────────┘
```

**No Kubernetes, no Docker, no complex orchestration needed for MVP.**

---

## 6-Week MVP Roadmap (Recruiter Candidate Briefs)

### Week 1: Foundation
**Goal**: Working Next.js app with database, auth, and Parallel API integration

- [ ] Set up Next.js project with TypeScript
- [ ] Configure Tailwind CSS + shadcn/ui
- [ ] Set up Vercel Postgres + Prisma
- [ ] Create database schema (users, candidates, briefs)
- [ ] Integrate NextAuth.js (email/password only)
- [ ] Test Parallel API connection (Search, Extract, Task)
- [ ] Deploy to Vercel

**Deliverable**: Empty app with login, deployed to production

---

### Week 2: Core Brief Generation
**Goal**: Generate first candidate brief from LinkedIn URL

- [ ] Build candidate input form
- [ ] API route: parse LinkedIn URL, extract profile info
- [ ] Parallel Search integration (query for candidate name + company)
- [ ] Parallel Extract integration (fetch top 5-10 URLs)
- [ ] Basic Task API call with simple schema
- [ ] Display raw JSON output
- [ ] Save to database

**Deliverable**: Can input LinkedIn URL, see JSON brief

---

### Week 3: UI & Brief Viewer
**Goal**: Beautiful brief viewer instead of raw JSON

- [ ] Design brief layout (summary, experience, activity, citations)
- [ ] Build brief viewer component
- [ ] Add loading states & progress indicators
- [ ] Error handling & retry logic
- [ ] GitHub integration (optional for MVP, adds value)
- [ ] Brief history page (list all generated briefs)

**Deliverable**: Nice-looking brief viewer

---

### Week 4: Export & Sharing
**Goal**: Users can export and share briefs

- [ ] PDF export (using @react-pdf/renderer or Puppeteer)
- [ ] Markdown copy button
- [ ] Public share link (no login required)
- [ ] Email brief to hiring manager
- [ ] Simple analytics (track views, exports)

**Deliverable**: Full export functionality

---

### Week 5: Polish & Beta Testing
**Goal**: Recruit 5-10 beta testers, get feedback

- [ ] Add onboarding flow
- [ ] Improve error messages
- [ ] Add usage limits (e.g., 10 briefs/month free)
- [ ] Set up Stripe (payment page, no paywall yet)
- [ ] Create landing page
- [ ] Write help documentation
- [ ] Recruit beta testers (recruiters in your network)
- [ ] Implement top 3 feedback items

**Deliverable**: Beta-ready product

---

### Week 6: Launch Prep
**Goal**: Public launch with pricing

- [ ] Implement paywall (free: 5 briefs/month, paid: unlimited)
- [ ] Stripe payment flow
- [ ] Launch on Product Hunt / Twitter / LinkedIn
- [ ] Set up customer support (email or Intercom)
- [ ] Create demo video
- [ ] Monitor for bugs, fix critical issues
- [ ] Get first paying customer 🎉

**Deliverable**: Public product with at least 1 paying customer

---

## Database Schema (MVP - Recruiter Briefs Only)

```sql
-- Users (handled by NextAuth.js mostly)
CREATE TABLE users (
  id TEXT PRIMARY KEY,
  email TEXT UNIQUE NOT NULL,
  name TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Candidates
CREATE TABLE candidates (
  id TEXT PRIMARY KEY,
  user_id TEXT REFERENCES users(id),
  name TEXT,
  linkedin_url TEXT,
  github_url TEXT,
  status TEXT DEFAULT 'pending', -- pending, processing, completed, failed
  created_at TIMESTAMP DEFAULT NOW()
);

-- Briefs
CREATE TABLE briefs (
  id TEXT PRIMARY KEY,
  candidate_id TEXT REFERENCES candidates(id),
  user_id TEXT REFERENCES users(id),
  content JSONB NOT NULL, -- structured brief data
  citations JSONB, -- array of source URLs
  api_cost DECIMAL(10,4), -- track Parallel API costs
  processing_time_ms INTEGER,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Usage tracking (for billing)
CREATE TABLE usage (
  id TEXT PRIMARY KEY,
  user_id TEXT REFERENCES users(id),
  action TEXT, -- brief_generated, pdf_exported
  created_at TIMESTAMP DEFAULT NOW()
);

-- Subscriptions (Stripe)
CREATE TABLE subscriptions (
  id TEXT PRIMARY KEY,
  user_id TEXT REFERENCES users(id),
  stripe_customer_id TEXT,
  stripe_subscription_id TEXT,
  plan TEXT, -- free, pro
  status TEXT, -- active, canceled, past_due
  created_at TIMESTAMP DEFAULT NOW()
);
```

---

## Parallel API Integration Pattern

Here's a simple, repeatable pattern for each brief:

```javascript
// /app/api/briefs/generate/route.ts
import { ParallelClient } from '@parallel/sdk';

export async function POST(req: Request) {
  const { candidateName, linkedinUrl } = await req.json();

  // 1. SEARCH for candidate info
  const searchResults = await parallel.search({
    objective: `Find recent blog posts, talks, and projects by ${candidateName}`,
    maxResults: 10
  });

  // 2. EXTRACT content from URLs
  const extractedContent = await parallel.extract({
    urls: searchResults.urls
  });

  // 3. TASK to create structured brief
  const brief = await parallel.task({
    objective: 'Create a candidate brief',
    context: extractedContent,
    schema: {
      summary: 'string',
      experience_snapshot: 'string',
      recent_activity: 'array',
      notable_work: 'array',
      risk_flags: 'array',
      citations: 'array'
    }
  });

  // 4. Save to database
  await db.brief.create({
    data: {
      candidateId,
      content: brief,
      apiCost: calculateCost(searchResults, extractedContent, brief)
    }
  });

  return Response.json(brief);
}
```

**Keep it simple. You can optimize later.**

---

## Pricing Strategy (Recruiter Briefs MVP)

### Free Tier
- 5 candidate briefs per month
- Basic exports (PDF, Markdown)
- Public share links
- Email support (48hr response)

**Goal**: Get users in the door, validate product

### Pro Tier - $49/month
- Unlimited candidate briefs
- Priority processing
- Auto-refresh (weekly updates)
- Slack notifications
- Email support (24hr response)
- API access (future)

**Goal**: Convert power users (agency recruiters, hiring managers)

### Usage-Based Alternative - $2 per brief
- No monthly commitment
- Pay only for what you use
- Good for occasional users

**Goal**: Capture people who don't want subscriptions

**Recommended**: Offer both subscription AND pay-per-use. Let users choose.

---

## Cost Breakdown (Solo Developer)

### Development Phase (Weeks 1-6)
- **Parallel API**: ~$200-500 (testing + beta users)
- **Hosting**: $0 (Vercel free tier)
- **Database**: $0 (Vercel Postgres free tier)
- **Domain**: $12/year
- **Total**: ~$212-512

### Post-Launch (Monthly)
- **Parallel API**: $500-2000 (depends on usage)
- **Hosting**: $20-50 (Vercel Pro after free tier)
- **Database**: $20 (once you exceed free tier)
- **Email service**: $10 (SendGrid, Resend)
- **Monitoring**: $0-25 (Sentry free tier)
- **Total**: ~$550-2105/month

**Break-even**: ~11-42 customers at $49/month

---

## What to Skip for MVP (Add Later)

### Skip Initially:
- ❌ Multi-tenancy / workspaces (single user accounts only)
- ❌ Team collaboration features
- ❌ ATS integrations (Greenhouse, Lever, etc.)
- ❌ Auto-refresh / scheduling
- ❌ Comparison mode
- ❌ Advanced analytics dashboard
- ❌ SSO / SAML
- ❌ Mobile app
- ❌ Bulk upload (CSV)
- ❌ API for external integrations
- ❌ White-labeling
- ❌ Multiple languages (English only)

### Add After Validation:
- ✅ Slack integration (top user request)
- ✅ One ATS integration (which one do users request most?)
- ✅ Bulk upload (when users ask for it)
- ✅ Auto-refresh (when users pay for it)

**Rule**: Only add features that paying customers explicitly request.

---

## After MVP Success: Building Products 2 & 3

### If Recruiter Briefs Gets Traction (10+ paying customers):

**Option 1: Double down on Recruiter product**
- Add ATS integrations
- Build collaboration features
- Raise prices, go upmarket
- Target recruiting agencies (10-100 seat plans)

**Option 2: Leverage infrastructure to build Influencer product**
- Reuse 80% of codebase (same patterns)
- Different data sources (Instagram, YouTube vs LinkedIn, GitHub)
- Target different market
- Cross-sell to existing users if applicable

**Option 3: Build Conversation Sentinel**
- Most complex of the three
- Only build if you have clear customer demand
- Consider this year 2+ product

### Solo Developer Reality Check

**One Product Done Well > Three Products Half-Built**

It's better to have:
- 100 customers on one solid product
- Than 10 customers spread across three mediocre products

Focus on one, get to $10K MRR, then decide what's next.

---

## Time Investment (Solo Developer)

### Weekly Time Commitment Options:

**Part-time (20hrs/week)**
- MVP: 12 weeks
- Getting to $5K MRR: 6-12 months
- Realistic if you have a day job

**Full-time (40hrs/week)**
- MVP: 6 weeks
- Getting to $5K MRR: 3-6 months
- Only if you can afford to focus full-time

**Recommended**: Start part-time, validate, then go full-time if traction is clear.

---

## Success Milestones

### Week 6: MVP Launch
- [ ] Product is live
- [ ] 10+ beta users have tried it
- [ ] At least 50 briefs generated
- [ ] Stripe payment flow works

### Month 3: Validation
- [ ] 5+ paying customers
- [ ] $245+ MRR (5 × $49)
- [ ] <20% churn
- [ ] Clear feature requests from users

### Month 6: Product-Market Fit
- [ ] 20+ paying customers
- [ ] $1,000+ MRR
- [ ] Organic word-of-mouth growth
- [ ] Users renewing subscriptions

### Month 12: Sustainable Business
- [ ] $5,000-10,000 MRR
- [ ] Can cover your living expenses
- [ ] 100+ total customers
- [ ] Decide: scale this, or build next product

---

## Marketing Strategy (Solo Developer)

You can't outspend competitors. You need to be scrappy.

### Pre-Launch (Weeks 1-5)
- [ ] Build in public on Twitter/LinkedIn
- [ ] Share progress screenshots weekly
- [ ] DM 20 recruiters, ask about their pain points
- [ ] Join recruiting Slack communities
- [ ] Create simple landing page with email capture

### Launch Week
- [ ] Product Hunt launch (prep Tues, launch Wed)
- [ ] Post on LinkedIn, Twitter, Reddit (r/recruiting)
- [ ] Email your network (anyone who knows recruiters)
- [ ] Offer lifetime deal for first 10 customers ($99 one-time)
- [ ] Collect testimonials immediately

### Post-Launch (Ongoing)
- [ ] SEO content: "How to research candidates faster" style blog posts
- [ ] LinkedIn posts showing before/after examples
- [ ] Ask happy users for referrals
- [ ] Join recruiting podcasts as guest (cheap marketing)
- [ ] Cold outreach to recruiting agencies (10 emails/day)

**Budget**: $0-100/month. Use your time, not money.

---

## Risk Mitigation (Solo Developer)

### Technical Risks
- **Risk**: Parallel API too expensive
  - **Mitigation**: Set hard monthly budget ($500), pause new briefs if exceeded
- **Risk**: Platform changes/breaks
  - **Mitigation**: Version lock APIs, have fallback plans
- **Risk**: Can't handle scale alone
  - **Mitigation**: Use managed services (Vercel, Supabase), automate everything

### Business Risks
- **Risk**: No one pays
  - **Mitigation**: Talk to 20 recruiters before building, validate problem is real
- **Risk**: Burn out
  - **Mitigation**: Set realistic hours, take weekends off, don't over-commit
- **Risk**: Big competitor launches same thing
  - **Mitigation**: Move fast, own a niche (e.g., India market), personal brand

---

## Development Tips for Solo Builders

### Avoid These Traps:
1. **Over-engineering** - Use boring, proven tech. No bleeding edge.
2. **Perfectionism** - Ship buggy MVP, fix later. Speed > polish initially.
3. **Feature creep** - Say no to 90% of ideas. Core workflow only.
4. **Building in isolation** - Show work weekly, get feedback constantly.
5. **Ignoring metrics** - Track everything from day 1 (signups, usage, revenue).

### Do These Things:
1. **Ship weekly** - Every Friday, deploy something new, even if small.
2. **Talk to users** - 30min user interview > 10hrs building features no one wants.
3. **Automate admin** - Use Stripe billing portal, not custom admin panels.
4. **Reuse code** - Every component should be reusable for products 2 & 3.
5. **Document as you go** - Future you will forget why you built things.

---

## When to Hire (Don't Rush This)

### Hire #1: Virtual Assistant ($5-15/hr) at $2K MRR
- Customer support emails
- Social media posting
- Data entry tasks
- Frees up 10hrs/week for you to code

### Hire #2: Part-time Developer ($50-100/hr) at $10K MRR
- Take over maintenance
- Build integrations
- You focus on product direction + sales

### Hire #3: Marketing Contractor at $20K MRR
- SEO content
- Paid ads
- Partnerships

**Don't hire too early. Bootstrap as long as possible.**

---

## Recommended Learning Resources

### If you're new to Next.js:
- Official Next.js tutorial (3 hours)
- Vercel's YouTube channel
- Lee Robinson's blog/videos

### If you're new to Parallel API:
- Read Parallel docs thoroughly
- Build 2-3 toy examples before MVP
- Join their Slack/Discord for support

### If you're new to SaaS:
- "The Mom Test" by Rob Fitzpatrick (customer interviews)
- "Traction" by Gabriel Weinberg (marketing channels)
- Indie Hackers podcast (solo founder stories)

---

## Next Steps

1. **Read `REQUIRED_INFORMATION.md`** and fill out sections 1-10 only (skip enterprise stuff)
2. **Validate the market**:
   - Talk to 10 recruiters this week
   - Ask: "How do you research candidates today?"
   - Ask: "Would you pay $49/month to save 5 hours/week?"
3. **Set up dev environment**:
   - Install Node.js, VS Code
   - Create Vercel account
   - Get Parallel API key
4. **Week 1 starts Monday** - follow the 6-week roadmap above
5. **Join communities**:
   - Indie Hackers
   - r/SaaS
   - Twitter: follow solo SaaS builders

---

## Final Advice

**Start small. Ship fast. Talk to users. Iterate.**

You don't need a team. You don't need VC funding. You don't need to build all three products.

Build ONE product that ONE type of customer loves. Get them to pay. Then decide what's next.

You've got this. 🚀

---

**Questions?** Refer to the original PRD files for detailed requirements, or reach out in the GitHub issues.
