# Required Information for Implementation

This document outlines all the information, access credentials, decisions, and resources needed from your side to successfully build and launch the three products. Please fill in each section before development begins.

---

## 1. Parallel API Access & Configuration

### API Credentials
- [ ] **Parallel API Key**: _______________
- [ ] **Parallel Environment** (Production/Sandbox): _______________
- [ ] **Parallel Workspace ID** (if applicable): _______________
- [ ] **Budget/Rate Limits**: $_______________/month
- [ ] **Point of Contact** for Parallel API support: _______________

### API Tier & Capabilities
- [ ] Which Parallel APIs do you have access to?
  - [ ] Search API
  - [ ] Extract API
  - [ ] Task API
  - [ ] Other: _______________
- [ ] Current rate limits per API: _______________
- [ ] Any custom pricing or enterprise features enabled? _______________

---

## 2. Product Prioritization & Scope

### Primary Product Selection
Which product should we build and launch first?
- [ ] Influencer Vet + Brief Builder
- [ ] Recruiter Candidate Briefs
- [ ] Share-of-Conversation Sentinel
- [ ] All three in parallel (requires larger team)

### Scope Decisions

#### For Influencer Vet + Brief Builder:
- [ ] **Target platforms for v1** (check all that apply):
  - [ ] Instagram
  - [ ] YouTube
  - [ ] LinkedIn
  - [ ] Moj
  - [ ] ShareChat
  - [ ] Josh
  - [ ] Twitter/X
  - [ ] Podcasts
  - [ ] Newsletters
  - [ ] Other: _______________

- [ ] **Languages for v1**:
  - [ ] English only
  - [ ] English + Hindi
  - [ ] English + Top 3 regional (specify): _______________
  - [ ] All 5+ languages from launch

- [ ] **Must-have features for v1**:
  - [ ] Risk detection & brand safety
  - [ ] Side-by-side comparison
  - [ ] Auto-refresh scheduling
  - [ ] Export to PDF/PowerPoint
  - [ ] Notion/Google Slides integration
  - [ ] Other: _______________

#### For Recruiter Candidate Briefs:
- [ ] **Primary data sources for v1**:
  - [ ] LinkedIn
  - [ ] GitHub
  - [ ] Personal blogs
  - [ ] Publications/press
  - [ ] Podcasts
  - [ ] Stack Overflow
  - [ ] Other: _______________

- [ ] **Must-have features for v1**:
  - [ ] ATS integration (specify system below)
  - [ ] Change tracking on refresh
  - [ ] PDF export
  - [ ] Slack notifications
  - [ ] Collaboration/comments
  - [ ] Other: _______________

#### For Share-of-Conversation Sentinel:
- [ ] **Primary sources for v1**:
  - [ ] Mainstream news (ET, Mint, TOI, etc.)
  - [ ] LinkedIn
  - [ ] YouTube
  - [ ] ShareChat/Moj/Josh
  - [ ] Reddit India
  - [ ] Quora
  - [ ] Regulatory releases (RBI, SEBI, PIB)
  - [ ] Other: _______________

- [ ] **Languages for v1**:
  - [ ] English only
  - [ ] English + Hindi
  - [ ] Multi-language from launch (specify): _______________

- [ ] **Must-have features for v1**:
  - [ ] Real-time alerts (<2 hour SLA)
  - [ ] Narrative clustering
  - [ ] Sentiment analysis
  - [ ] Response planner
  - [ ] Custom watchlists
  - [ ] Other: _______________

---

## 3. Integration Requirements

### ATS/CRM Systems (for Recruiter Product)

**Primary ATS/CRM to integrate:**
- [ ] Greenhouse
- [ ] Lever
- [ ] Workday
- [ ] Ashby
- [ ] SmartRecruiters
- [ ] BambooHR
- [ ] Other: _______________

**Integration Details:**
- [ ] **Sandbox/Test Environment Access**:
  - URL: _______________
  - Credentials: _______________
  - API Key/Token: _______________
- [ ] **Required scopes/permissions**: _______________
- [ ] **Point of contact** for ATS admin access: _______________
- [ ] **Custom fields** available for storing brief data? (Yes/No): _______________
- [ ] **Webhooks** supported? (Yes/No): _______________

### Collaboration Tools

**Slack:**
- [ ] Workspace URL: _______________
- [ ] Preferred channels for notifications: _______________
- [ ] Admin contact for bot installation: _______________
- [ ] App installation allowed? (Yes/No): _______________

**Microsoft Teams:**
- [ ] Tenant ID: _______________
- [ ] Preferred channels: _______________
- [ ] Admin contact: _______________
- [ ] App installation allowed? (Yes/No): _______________

**Notion:**
- [ ] Workspace URL: _______________
- [ ] Integration token: _______________
- [ ] Target databases/pages: _______________

**Google Workspace:**
- [ ] Organization domain: _______________
- [ ] Service account required? (Yes/No): _______________
- [ ] Target Google Drive folders: _______________

**Jira/Asana (for Sentinel Response Planner):**
- [ ] System: _______________
- [ ] Project/Board for tasks: _______________
- [ ] API credentials: _______________

---

## 4. Example Data & Test Cases

### For Influencer Product:
Please provide 5-10 example influencers/creators for prompt tuning and testing:

| Name | Instagram | YouTube | Other Handles | Category | Notes |
|------|-----------|---------|---------------|----------|-------|
| 1. | | | | | |
| 2. | | | | | |
| 3. | | | | | |
| 4. | | | | | |
| 5. | | | | | |

**Criteria for good/bad influencers:**
- What makes a creator high-quality in your eyes? _______________
- What are red flags or deal-breakers? _______________
- Specific brand safety keywords to flag: _______________

### For Recruiter Product:
Please provide 5-10 example candidate profiles for testing:

| Name | LinkedIn URL | GitHub | Role/Expertise | Notes |
|------|-------------|--------|----------------|-------|
| 1. | | | | |
| 2. | | | | |
| 3. | | | | |
| 4. | | | | |
| 5. | | | | |

**Key competencies to emphasize:**
- List 5-10 skills/competencies your team cares about: _______________

### For Sentinel Product:
Please provide watchlist examples:

**Competitors to monitor:**
1. _______________
2. _______________
3. _______________
4. _______________
5. _______________

**Keywords/Topics to track:**
1. _______________
2. _______________
3. _______________
4. _______________
5. _______________

**Known narratives you're currently tracking manually:**
1. _______________
2. _______________
3. _______________

---

## 5. Design & Brand Guidelines

### Brand Assets
- [ ] **Logo files** (SVG, PNG): _______________
- [ ] **Color palette**:
  - Primary: _______________
  - Secondary: _______________
  - Accent: _______________
- [ ] **Typography**:
  - Heading font: _______________
  - Body font: _______________
- [ ] **Brand guidelines document**: _______________

### Design Preferences
- [ ] **UI framework preference**:
  - [ ] Material Design (Google)
  - [ ] Tailwind CSS + shadcn/ui
  - [ ] Custom design system
  - [ ] Other: _______________
- [ ] **Existing dashboards** to align with (provide screenshots/URLs): _______________
- [ ] **Component library** (if any): _______________

### Accessibility & Localization
- [ ] **Accessibility requirements**:
  - [ ] WCAG 2.1 Level AA compliance
  - [ ] Screen reader support
  - [ ] Keyboard navigation
  - [ ] High contrast mode
  - [ ] Other: _______________
- [ ] **Localization needs**:
  - [ ] RTL support required? (Yes/No): _______________
  - [ ] Date/time format preferences: _______________
  - [ ] Number format preferences: _______________

---

## 6. Team & Roles

### Development Team

**Backend Engineers:**
- Name: _______________ | Email: _______________ | Focus area: _______________
- Name: _______________ | Email: _______________ | Focus area: _______________
- Name: _______________ | Email: _______________ | Focus area: _______________

**Frontend Engineers:**
- Name: _______________ | Email: _______________ | Focus area: _______________
- Name: _______________ | Email: _______________ | Focus area: _______________

**DevOps/Infrastructure:**
- Name: _______________ | Email: _______________ | Focus area: _______________

**Prompt Engineering/AI:**
- Name: _______________ | Email: _______________ | Focus area: _______________

**Product Manager:**
- Name: _______________ | Email: _______________

**Designer:**
- Name: _______________ | Email: _______________

**QA/Testing:**
- Name: _______________ | Email: _______________

### Stakeholders & Decision Makers

**Project Sponsor/Approver:**
- Name: _______________ | Email: _______________ | Role: _______________

**Product Decision Maker:**
- Name: _______________ | Email: _______________

**Technical Decision Maker:**
- Name: _______________ | Email: _______________

**Beta Testers Coordinator:**
- Name: _______________ | Email: _______________

---

## 7. Timeline & Milestones

### Key Dates

**Project Start Date:** _______________

**Milestone Dates:**
- [ ] Phase 0 (Foundation) complete: _______________
- [ ] Alpha launch (internal): _______________
- [ ] Private Beta start: _______________
- [ ] GA launch target: _______________
- [ ] Other milestones: _______________

### Sprint Schedule
- [ ] **Sprint length**: _______________ weeks
- [ ] **Sprint planning day/time**: _______________
- [ ] **Demo/review day/time**: _______________
- [ ] **Retrospective day/time**: _______________

### Availability Constraints
- [ ] Any planned PTO/holidays affecting the team? _______________
- [ ] Blackout periods (no deploys)? _______________
- [ ] Major events/conferences that affect timeline? _______________

---

## 8. Infrastructure & Hosting

### Cloud Provider Preference
- [ ] AWS
- [ ] Google Cloud Platform
- [ ] Microsoft Azure
- [ ] Other: _______________
- [ ] No preference

### Existing Infrastructure
- [ ] **Do you have existing cloud accounts?** (Yes/No): _______________
  - If yes, account ID: _______________
  - Billing contact: _______________
- [ ] **Existing databases** we should use: _______________
- [ ] **Existing monitoring tools**: _______________
- [ ] **CI/CD pipelines** in place: _______________

### Domain & SSL
- [ ] **Domain name** for the application: _______________
- [ ] **Who manages DNS?** _______________
- [ ] **SSL certificate** provider: _______________

### Environment Strategy
- [ ] Development environment URL: _______________
- [ ] Staging environment URL: _______________
- [ ] Production environment URL: _______________

---

## 9. Security & Compliance Requirements

### Authentication
- [ ] **Preferred auth method**:
  - [ ] Email/password
  - [ ] OAuth (Google, Microsoft, etc.)
  - [ ] SSO/SAML (Enterprise)
  - [ ] Magic link
  - [ ] Other: _______________

### SSO/Identity Provider (for Enterprise)
- [ ] **Identity Provider**: _______________
- [ ] **SAML metadata URL**: _______________
- [ ] **Admin contact**: _______________

### Data Compliance
- [ ] **Regions you operate in**: _______________
- [ ] **Compliance requirements**:
  - [ ] GDPR (Europe)
  - [ ] CCPA (California)
  - [ ] SOC 2
  - [ ] HIPAA
  - [ ] ISO 27001
  - [ ] Other: _______________

### Data Retention
- [ ] **Default data retention period**: _______________ days
- [ ] **User data deletion workflow**: _______________
- [ ] **Backup retention policy**: _______________

### Security Scanning
- [ ] **Required security tools**:
  - [ ] Snyk
  - [ ] Dependabot
  - [ ] SonarQube
  - [ ] Other: _______________
- [ ] **Penetration testing required?** (Yes/No): _______________
- [ ] **Bug bounty program?** (Yes/No): _______________

---

## 10. Budget & Cost Controls

### Development Budget
- [ ] **Total development budget**: $_______________
- [ ] **Monthly operating budget** (after launch): $_______________

### API/Service Budgets
- [ ] **Parallel API monthly budget**: $_______________
- [ ] **Translation API budget** (Google Cloud): $_______________
- [ ] **Infrastructure budget** (hosting, DB, storage): $_______________
- [ ] **Third-party services** (monitoring, email, etc.): $_______________

### Cost Alerts
- [ ] **Alert threshold** for Parallel API usage: $_______________
- [ ] **Who receives cost alerts?** _______________
- [ ] **Hard spending cap?** (Yes/No): _______________
  - If yes, amount: $_______________

---

## 11. Third-Party Data & API Access

### Language Processing
- [ ] **Google Cloud Translation API**:
  - API Key: _______________
  - Enabled languages: _______________
- [ ] **Alternative translation provider** (if any): _______________

### Social Media APIs (if available)
These are optional but can improve data quality:

- [ ] **Instagram Graph API** access? (Yes/No): _______________
  - App ID: _______________
  - App Secret: _______________
- [ ] **YouTube Data API**:
  - API Key: _______________
- [ ] **LinkedIn API** access? (Yes/No): _______________
- [ ] **Twitter/X API**:
  - Bearer Token: _______________

### Additional Data Sources
- [ ] **Paid media monitoring service** (Meltwater, Brandwatch, etc.): _______________
  - API access: _______________
- [ ] **Influencer databases** (HypeAuditor, etc.): _______________
- [ ] **Fake follower detection** (SparkToro, etc.): _______________

---

## 12. User Research & Beta Testing

### Alpha Testers (Internal)
Please provide contact info for 5-10 internal team members who will test alpha versions:

| Name | Email | Role | Product to Test | Availability |
|------|-------|------|----------------|--------------|
| 1. | | | | |
| 2. | | | | |
| 3. | | | | |
| 4. | | | | |
| 5. | | | | |

### Beta Testers (External)
Please provide contact info for external beta testers (agencies, brands, recruiting firms):

| Organization | Contact Name | Email | Product Interest | Notes |
|-------------|--------------|-------|------------------|-------|
| 1. | | | | |
| 2. | | | | |
| 3. | | | | |
| 4. | | | | |
| 5. | | | | |

### Feedback Collection
- [ ] **Preferred feedback tool**:
  - [ ] In-app feedback widget
  - [ ] Google Forms
  - [ ] Typeform
  - [ ] Intercom
  - [ ] Other: _______________
- [ ] **Who reviews feedback?** _______________

---

## 13. Billing & Monetization

### Pricing Strategy
- [ ] **Business model**:
  - [ ] Freemium (free tier + paid plans)
  - [ ] Subscription only
  - [ ] Usage-based
  - [ ] Hybrid (base subscription + usage)
  - [ ] Enterprise/custom pricing only

### Payment Processing
- [ ] **Payment provider**:
  - [ ] Stripe
  - [ ] PayPal
  - [ ] Razorpay (India-focused)
  - [ ] Other: _______________
- [ ] **Account details**: _______________
- [ ] **Currencies to support**: _______________
- [ ] **Tax handling** (VAT, GST, etc.): _______________

### Plan Tiers (if applicable)
Please define your pricing tiers:

| Tier | Price/Month | Features | Limits |
|------|-------------|----------|--------|
| Free | | | |
| Pro | | | |
| Enterprise | | | |

---

## 14. Support & Documentation

### Customer Support
- [ ] **Support channels**:
  - [ ] Email
  - [ ] Intercom/chat
  - [ ] Slack Connect
  - [ ] Phone
  - [ ] Ticketing system: _______________
- [ ] **Support team members**: _______________
- [ ] **SLA for support response**: _______________

### Documentation
- [ ] **Documentation platform**:
  - [ ] Notion
  - [ ] GitBook
  - [ ] ReadMe.io
  - [ ] Custom docs site
  - [ ] Other: _______________
- [ ] **Who writes docs?** _______________
- [ ] **Who maintains docs?** _______________

### Help Resources
- [ ] **Video tutorials** required? (Yes/No): _______________
- [ ] **In-app onboarding** required? (Yes/No): _______________
- [ ] **FAQ/Knowledge base** required? (Yes/No): _______________

---

## 15. Monitoring & Alerts

### Application Monitoring
- [ ] **Monitoring tool preference**:
  - [ ] Datadog
  - [ ] New Relic
  - [ ] Sentry (errors)
  - [ ] LogRocket (session replay)
  - [ ] Grafana + Prometheus (open-source)
  - [ ] Other: _______________
- [ ] **Existing monitoring accounts**: _______________

### Alerting
**Who should receive alerts for:**
- [ ] **Production errors**: _______________
- [ ] **Performance degradation**: _______________
- [ ] **Cost overruns**: _______________
- [ ] **Security incidents**: _______________

### Uptime Monitoring
- [ ] **Uptime SLA target**: _______________% (e.g., 99%, 99.9%)
- [ ] **Status page** required? (Yes/No): _______________
  - If yes, tool preference (StatusPage.io, etc.): _______________

---

## 16. Legal & Contracts

### Terms & Privacy
- [ ] **Do you have existing Terms of Service?** (Yes/No): _______________
  - If yes, link: _______________
- [ ] **Do you have a Privacy Policy?** (Yes/No): _______________
  - If yes, link: _______________
- [ ] **Legal counsel** contact for review: _______________

### Data Processing Agreements
- [ ] **DPA template** (for GDPR): _______________
- [ ] **Legal entity** providing the service: _______________

### Intellectual Property
- [ ] **Who owns the code/IP?**
  - [ ] Your company
  - [ ] Development agency
  - [ ] Joint ownership
  - [ ] Other: _______________

---

## 17. Open Questions & Risks

### Technical Questions
List any technical concerns or open questions:
1. _______________
2. _______________
3. _______________

### Business Questions
List any business/product questions:
1. _______________
2. _______________
3. _______________

### Known Risks
List any known risks or dependencies:
1. _______________
2. _______________
3. _______________

### Constraints
Any constraints we should know about?
- [ ] **Technical constraints**: _______________
- [ ] **Budget constraints**: _______________
- [ ] **Timeline constraints**: _______________
- [ ] **Team constraints**: _______________

---

## 18. Post-Launch Plans

### Marketing & Sales
- [ ] **Go-to-market strategy**: _______________
- [ ] **Launch channels**:
  - [ ] Product Hunt
  - [ ] Social media (which platforms): _______________
  - [ ] Email campaigns
  - [ ] Paid ads
  - [ ] Content marketing
  - [ ] Other: _______________
- [ ] **Marketing site** URL: _______________
- [ ] **Sales contact**: _______________

### Customer Success
- [ ] **Onboarding process** planned? (Yes/No): _______________
- [ ] **Customer success team** in place? (Yes/No): _______________
- [ ] **Quarterly business reviews** for enterprise? (Yes/No): _______________

### Product Roadmap
What features come after v1 launch?
1. _______________
2. _______________
3. _______________
4. _______________
5. _______________

---

## Submission Checklist

Before starting development, ensure you've filled out:

- [ ] Section 1: Parallel API Access
- [ ] Section 2: Product Prioritization
- [ ] Section 3: Integration Requirements
- [ ] Section 4: Example Data
- [ ] Section 5: Design & Brand
- [ ] Section 6: Team & Roles
- [ ] Section 7: Timeline & Milestones
- [ ] Section 8: Infrastructure & Hosting
- [ ] Section 9: Security & Compliance
- [ ] Section 10: Budget & Cost Controls
- [ ] Section 11: Third-Party Data & APIs
- [ ] Section 12: User Research & Beta Testing
- [ ] Section 13: Billing & Monetization
- [ ] Section 14: Support & Documentation
- [ ] Section 15: Monitoring & Alerts
- [ ] Section 16: Legal & Contracts
- [ ] Section 17: Open Questions & Risks
- [ ] Section 18: Post-Launch Plans

---

## Next Steps After Completing This Form

1. **Schedule kickoff meeting** with development team to review responses
2. **Set up development environments** based on infrastructure choices
3. **Create project board** (Jira, Linear, GitHub Projects) with initial backlog
4. **Begin Phase 0** (Foundation) development per README.md roadmap
5. **Schedule weekly syncs** to track progress and address blockers

**Questions about this form?**
Contact your project lead or refer to `Build_Kickoff_Inputs.md` for additional context.
