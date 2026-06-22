---
name: devops-architecture-kit
description: "Generate Architecture Decision Records (ADRs), RFCs, Runbooks, and team documentation from context. Built by CodeBlueprint."
version: 1.0.0
author: CodeBlueprint
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [devops, documentation, adr, rfc, runbook, architecture, team]
    examples:
      - "Create an ADR for choosing our database"
      - "Write a runbook for production incident response"
      - "Generate an RFC for the new microservices migration"
---

# DevOps Architecture Documentation Kit

> **Brand:** CodeBlueprint | **Version:** 1.0.0  
> **Compatible with:** Hermes Agent, Claude Code, any LLM agent  
> **Format:** Markdown (Git, Notion, Obsidian, Confluence compatible)

This skill provides battle-tested templates for technical documentation. Use it when you need to record architectural decisions, propose changes, create operational runbooks, or establish team documentation standards.

---

## TRIGGERS

Invoke automatically when the user asks to:
- Document an architectural decision
- Create an ADR (Architecture Decision Record)
- Write an RFC (Request for Comments)
- Create a runbook
- Write a post-mortem
- Create a tech spec
- Standardize team documentation
- Record "why did we choose this?"

---

## ADR — Architecture Decision Record

### Standard ADR Template

Use this when documenting a significant technical decision:

```markdown
# ADR-{NUMBER}: {Title}

**Status:** Proposed | Accepted | Deprecated | Superseded by ADR-{N}

**Date:** {YYYY-MM-DD}

**Context:**
{Describe the situation and forces at play, including technological, organizational, and project constraints.}

**Decision:**
{Describe the response to these forces. Explain the decision in full sentences, as if you were explaining it to someone who wasn't part of the original conversation.}

**Consequences:**
{Describe the resulting context after applying the decision. Include positive and negative consequences.}

**Alternatives Considered:**
- **{Alternative 1}:** {Description} — {Why rejected}
- **{Alternative 2}:** {Description} — {Why rejected}

**Related ADRs:**
- ADR-{N}: {Title}
```

### ADR-001: Technology Stack Selection

```markdown
# ADR-001: Technology Stack Selection

**Status:** Accepted

**Date:** 2024-01-15

**Context:**
We need to build a new customer-facing API that will serve 10,000+ requests per day. The team is 5 developers with strong Python background. We require high availability, easy deployment, and quick iteration cycles.

**Decision:**
We will use FastAPI with PostgreSQL, deployed on Railway with a managed PostgreSQL instance. Redis will be used for caching and session management.

**Consequences:**
- Positive: FastAPI provides automatic OpenAPI docs, async support, and Pydantic validation out of the box
- Positive: Railway offers simple git-push deploy with managed databases
- Positive: Team can ship features quickly with Python's ecosystem
- Negative: FastAPI's async patterns require discipline to avoid blocking calls
- Negative: Railway costs scale with usage; estimated $20-50/month for our scale

**Alternatives Considered:**
- **Node.js/Express:** Faster ecosystem for web, but team's Python expertise outweighs this — Rejected
- **Django:** More batteries-included, but adds unnecessary complexity for an API service — Rejected
- **Go:** High performance, but longer development cycle for the team — Rejected
```

### ADR-002: Database Selection

```markdown
# ADR-002: Database Selection

**Status:** Accepted

**Date:** 2024-01-15

**Context:**
We need a primary database for transactional data with strong consistency requirements. The data model includes user accounts, subscriptions, and usage logs.

**Decision:**
PostgreSQL 15 with pgbouncer connection pooling.

**Consequences:**
- Positive: ACID compliance ensures data integrity for financial transactions
- Positive: Rich indexing (GIN, GiST, BRIN) for performance
- Positive: JSONB support for semi-structured data
- Positive: pgbouncer handles connection pooling efficiently
- Negative: Requires careful schema migrations management
- Negative: Vertical scaling has limits; horizontal sharding would require significant refactoring
```

### ADR-003: API Style — REST vs GraphQL vs gRPC

```markdown
# ADR-003: API Style

**Status:** Accepted

**Date:** 2024-01-20

**Context:**
We need to expose our business logic to frontend clients and third-party integrations. Requirements: HTTP/1.1 support, easy debugging, broad client library support.

**Decision:**
RESTful API with JSON over HTTPS. OpenAPI 3.1 specification for documentation.

**Consequences:**
- Positive: Universal HTTP client support
- Positive: Easy to test with curl/browser devtools
- Positive: OpenAPI generates client SDKs automatically
- Negative: Over-fetching/under-fetching requires careful endpoint design
- Negative: No real-time capability without WebSockets or SSE
```

### ADR-004: Authentication Strategy

```markdown
# ADR-004: Authentication Strategy

**Status:** Accepted

**Date:** 2024-02-01

**Context:**
We need to secure API endpoints and manage user sessions. Third-party integrations require programmatic access. Users must be able to revoke access at any time.

**Decision:**
JWT tokens (access + refresh) with short-lived access tokens (15 min) and refresh tokens stored in httpOnly cookies. API keys for programmatic access with per-key permissions.

**Consequences:**
- Positive: Stateless authentication scales horizontally
- Positive: Short-lived access tokens limit exposure window
- Positive: API keys provide third-party integrations without exposing user credentials
- Negative: Token revocation requires blacklist or short expiry (we chose short expiry)
- Negative: JWT size adds overhead to every request
```

### ADR-005: Deployment Strategy

```markdown
# ADR-005: Deployment Strategy

**Status:** Accepted

**Date:** 2024-02-10

**Context:**
We need zero-downtime deployments with easy rollbacks. The team ships features multiple times per day. Infrastructure costs must be predictable.

**Decision:**
Containerized deployments on Railway with Docker. GitHub Actions for CI/CD pipeline. Blue-green deployments via Railway's built-in rollback mechanism.

**Consequences:**
- Positive: Docker ensures consistency from dev to production
- Positive: Railway handles deployment complexity automatically
- Positive: One-click rollback reduces deployment risk
- Positive: GitHub Actions provides free tier for open repos
- Negative: Docker build times add 2-5 minutes to CI
- Negative: Railway is not self-hostable; vendor lock-in
```

### ADR-006: Microservices vs Monolith

```markdown
# ADR-006: System Architecture — Monolith

**Status:** Accepted

**Date:** 2024-01-10

**Context:**
Team of 5 developers, need to ship MVP in 3 months. No prior microservices experience. Simple domain with clear boundaries inside a single product.

**Decision:**
Modular monolith architecture. Code is organized by domain modules (users, billing, notifications) but deployed as a single service.

**Consequences:**
- Positive: Faster initial development
- Positive: Simple debugging and profiling
- Positive: No network latency between modules
- Positive: Transactional consistency is straightforward
- Negative: Must deploy entire application for any change
- Negative: Scaling requires scaling everything, even low-traffic modules
```

### ADR-007: Caching Strategy

```markdown
# ADR-007: Caching Strategy

**Status:** Accepted

**Date:** 2024-03-01

**Context:**
We need to reduce database load and improve response times for frequently accessed data. Cache invalidation must be predictable to avoid stale data bugs.

**Decision:**
Redis for application-level caching with a 3-tier strategy:
- L1: In-memory cache (dict) for request-scoped data
- L2: Redis for session and short-lived data (TTL: 5-15 min)
- L3: Database (PostgreSQL) as source of truth

Cache-aside pattern with explicit invalidation on writes.

**Consequences:**
- Positive: Dramatically reduces database load for hot data
- Positive: Redis provides persistence and clustering
- Positive: Predictable invalidation via explicit cache.delete()
- Negative: Cache misses require database fallback
- Negative: Stale data risk if invalidation is missed
```

### ADR-008: Message Queue Selection

```markdown
# ADR-008: Message Queue

**Status:** Accepted

**Date:** 2024-03-15

**Context:**
We need async processing for email sending, webhook delivery, and report generation. These tasks should not block the main request/response cycle.

**Decision:**
Redis Streams (via BullMQ) for job queues. Webhook delivery uses a separate high-priority queue with retry logic.

**Consequences:**
- Positive: BullMQ provides job scheduling, retries, and priority queues
- Positive: Redis Streams offers persistence without separate infrastructure
- Positive: Job deduplication prevents duplicate processing
- Negative: Redis is not a dedicated message broker; lacks some Kafka features
- Negative: At very high scale (>100k jobs/day), may need dedicated broker
```

### ADR-009: Monitoring and Observability

```markdown
# ADR-009: Observability Stack

**Status:** Accepted

**Date:** 2024-04-01

**Context:**
We need visibility into application health, performance, and errors. Team needs alerts for production issues without alert fatigue.

**Decision:**
Structured JSON logging to stdout (Railway log drain). Sentry for error tracking. Health check endpoints (/health) for uptime monitoring.

**Consequences:**
- Positive: Railway's built-in log viewer is sufficient for development
- Positive: Sentry provides automatic error grouping and alerting
- Positive: /health endpoints integrate with Railway health checks
- Negative: No distributed tracing (may add OpenTelemetry in future)
- Negative: No APM for profiling (Sentry Performance is limited on free tier)
```

### ADR-010: Security Hardening

```markdown
# ADR-010: Security Hardening

**Status:** Accepted

**Date:** 2024-04-15

**Context:**
Application handles user data including email and subscription information. We must protect against common web vulnerabilities and comply with basic data protection practices.

**Decision:**
- All API endpoints require HTTPS
- Rate limiting: 100 req/min per IP, 1000 req/min per API key
- Input validation via Pydantic on all endpoints
- SQL injection prevented via parameterized queries (SQLAlchemy ORM)
- XSS prevented via template auto-escaping (Jinja2 default)
- CORS configured to allow only specific origins
- Security headers: HSTS, CSP, X-Frame-Options
- Secret scanning in CI (trufflehog)

**Consequences:**
- Positive: Defense in depth reduces attack surface
- Positive: Rate limiting prevents abuse and DoS
- Positive: Automated secret scanning catches accidental leaks
- Negative: CORS configuration requires maintenance as clients change
- Negative: Some rate limits may affect legitimate bulk operations
```

---

## RFC — Request for Comments

Use this for significant changes that need team discussion before implementation.

### RFC Template

```markdown
# RFC-{NUMBER}: {Title}

**Author:** {Name}

**Status:** Draft | Under Review | Approved | Rejected

**Created:** {YYYY-MM-DD}

**Last Updated:** {YYYY-MM-DD}

---

## Summary

{One paragraph: What is this change and why is it being proposed?}

## Motivation

{Why are we doing this? What problem does it solve?}

### Problem Statement

{Detailed description of the current problem}

### Proposed Solution

{Description of the proposed solution}

## Detailed Design

{Technical specification of the proposed solution}

### Data Model Changes

```sql
-- Any database schema changes
```

### API Changes

| Endpoint | Method | Change |
|----------|--------|--------|
| /api/v1/resource | GET | New endpoint |

### Implementation Plan

**Phase 1:** {Description} — Target: {Date}
**Phase 2:** {Description} — Target: {Date}

## Risks and Mitigations

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| {Risk description} | {H/M/L} | {H/M/L} | {Mitigation} |

## Alternatives

### Alternative 1: {Name}

{Description and why we didn't choose it}

## Open Questions

1. {Question 1}
2. {Question 2}

## Decision

{To be filled after RFC review}
```

### RFC-001: Microservices Migration

```markdown
# RFC-001: Microservices Migration

**Author:** {Name}

**Status:** Under Review

**Created:** 2024-05-01

---

## Summary

Propose migrating from the modular monolith to a microservices architecture to improve team autonomy and scaling.

## Motivation

**Problem:** The current monolith requires coordinated deployments. A single bug in the billing module can delay feature work in the notifications module.

**Goals:**
- Independent team deployments
- Independent scaling of high-traffic modules
- Technology diversity for specific use cases

## Detailed Design

### Proposed Services

1. **user-service:** User accounts, authentication, profiles
2. **billing-service:** Subscriptions, payments, invoices
3. **notification-service:** Email, push notifications
4. **api-gateway:** Auth validation, routing

### Communication Pattern

- Synchronous: REST for user-facing requests
- Asynchronous: Redis Streams for cross-service events

## Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Distributed system complexity | High | Invest in observability first |
| Data consistency | High | Event sourcing for billing |

## Open Questions

1. Should each service own its database or share one?
2. How do we handle cross-service transactions?
3. What is our rollback strategy for failed deployments?
```

---

## PRODUCTION RUNBOOKS

### Runbook Template

```markdown
# Runbook: {Title}

**Last Updated:** {Date}

**Owner:** {Team/Person}

**On-Call:** {Escalation path}

---

## Overview

{One paragraph describing what this runbook covers.}

## Prerequisites

- Access to production environment
- Required tools: {List}
- Required permissions: {List}

## Step-by-Step Procedure

### Step 1: {Action}

{Description of the action to take}

```bash
# Commands to run
command --flag value
```

### Step 2: {Action}

{Description}

## Verification

After completing the procedure, verify:
- [ ] {Check 1}
- [ ] {Check 2}
- [ ] {Check 3}

## Rollback

If something goes wrong:

```bash
rollback-command
```

## Contact

- Primary: {Name/Channel}
- Escalation: {Name/Channel}
```

### Runbook-001: Incident Response

```markdown
# Runbook: Production Incident Response

**Last Updated:** 2024-06-01

**Owner:** Engineering Team

**On-Call:** PagerDuty → #incidents Slack channel

---

## Overview

This runbook guides the on-call engineer through detecting, responding to, and resolving production incidents.

## Severity Levels

| Severity | Definition | Response Time | Example |
|----------|------------|---------------|---------|
| P0 | Complete outage, data loss risk | Immediate | Site down |
| P1 | Major feature broken | < 15 min | Checkout broken |
| P2 | Degraded experience | < 1 hour | Slow search |
| P3 | Minor issue | Next business day | Typo in UI |

## Incident Response Procedure

### Step 1: Detect
- Monitor: Check Datadog/Railway dashboard
- Alert: PagerDuty page or user report in #alerts

### Step 2: Acknowledge
```bash
# Acknowledge in PagerDuty
pd incident ack {incident_id}
```

### Step 3: Assess
```bash
# Check recent deployments
heroku releases --app production-app

# Check error rates
curl -s "https://api.datadog.com/v1/metric" | jq '.series[0].point[-1]'

# Check database connections
SELECT count(*) FROM pg_stat_activity;
```

### Step 4: Communicate
1. Post in #incidents: "Investigating elevated error rates on /api/checkout"
2. Update status page if P0/P1
3. Set expectation for next update (15 min)

### Step 5: Mitigate
```bash
# Rollback last deployment
railway rollback

# Or disable feature flag
railway env set FEATURE_NEW_CHECKOUT=false
```

### Step 6: Resolve
1. Verify errors return to baseline
2. Update #incidents with resolution
3. Close PagerDuty incident
4. Update status page

## Verification

- [ ] Error rate < 0.1% for 5 minutes
- [ ] Response time P95 < 500ms
- [ ] No PagerDuty alerts firing

## Post-Incident

- Create post-mortem within 48 hours
- Use template: Runbook-005: Post-Mortem
```

### Runbook-002: Database Failover

```markdown
# Runbook: Database Failover

**Last Updated:** 2024-06-01

**Owner:** Platform Team

---

## Overview

Procedure to manually failover to database replica when primary is unhealthy.

## Prerequisites

- Railway Pro plan (required for failover)
- Database admin credentials
- Backup verification

## Procedure

### Step 1: Verify Primary is Down

```sql
-- Connect to primary
psql $DATABASE_URL

-- Check connection
SELECT 1;

-- Expected: ERROR: connection refused (if primary is down)
```

### Step 2: Promote Replica

```bash
# In Railway dashboard:
# 1. Go to your PostgreSQL database
# 2. Settings → Replicas → Promote Replica
# 3. Confirm promotion

# Or via CLI
railway run pg_ctl promote -D /var/lib/postgresql/data
```

### Step 3: Update Connection String

```bash
# Get new connection string from Railway
railway variables | grep DATABASE

# Update application
railway env set DATABASE_URL="postgresql://new-url"
```

### Step 4: Verify

```sql
-- Connect to new primary
psql $DATABASE_URL

-- Check replication lag (should be 0)
SELECT now() - pg_last_xact_replay_timestamp() AS replication_lag;

-- Test write
INSERT INTO health_check (ts) VALUES (NOW());
```

## Verification

- [ ] Write operations succeed
- [ ] Application connects without errors
- [ ] No data loss (compare row counts with backup)

## Rollback

```bash
# If issues with new primary, rollback to point-in-time
railway backup restore {backup_id}
```
```

### Runbook-003: Deployment Rollback

```markdown
# Runbook: Deployment Rollback

**Last Updated:** 2024-06-01

---

## Overview

Procedure to rollback a production deployment that introduced issues.

## Railway Rollback

```bash
# List recent deployments
railway deployments

# Get previous deployment ID
railway rollback --deployment {deployment_id}

# Or rollback to last working deployment
railway rollback
```

## Verification

- [ ] Health check passes: `curl https://api.app.com/health`
- [ ] Error rate returns to baseline
- [ ] Key user flows work

## After Rollback

1. Post in #incidents: "Rolled back deployment #{id}. Issue under investigation."
2. File bug report with deployment link
3. Do NOT redeploy until root cause identified
```

### Runbook-004: Security Incident

```markdown
# Runbook: Security Incident Response

**Last Updated:** 2024-06-01

---

## Overview

Procedure for responding to potential security incidents.

## Step 1: Isolate

```bash
# Block suspicious IP
ufw insert 1 deny from {suspicious_ip}

# Revoke compromised API key
curl -X DELETE https://api.app.com/admin/keys/{key_id}

# Rotate database password
psql $DATABASE_URL -c "ALTER USER postgres WITH PASSWORD 'new_password';"
railway env set DATABASE_URL="postgresql://postgres:new_password@..."
```

## Step 2: Assess

1. Check access logs for unauthorized access
2. Identify affected data/systems
3. Determine breach timeline

## Step 3: Contain

- Isolate affected services
- Preserve evidence (logs, database state)
- Update firewall rules

## Step 4: Notify

- Internal: Engineering lead, CTO
- External: Legal, affected users (if data breach)
- Documentation: Full incident timeline

## Step 5: Recover

1. Patch vulnerability
2. Restore from clean backup if needed
3. Monitor for re-exploitation
```

### Runbook-005: Post-Mortem Template

```markdown
# Post-Mortem: {Incident Title}

**Date:** {YYYY-MM-DD}

**Duration:** {X hours}

**Severity:** {P0/P1/P2/P3}

**Status:** {Draft/Review/Published}

---

## Summary

{One paragraph: What happened, impact, and how it was resolved.}

## Timeline (UTC)

| Time | Event |
|------|-------|
| 14:00 | User reports checkout error |
| 14:05 | On-call engineer acknowledges |
| 14:15 | Identified deployment #1234 as cause |
| 14:20 | Initiated rollback |
| 14:25 | Rollback complete, service restored |

## Root Cause

{Detailed explanation of why the incident occurred.}

## Impact

- **Users affected:** {Number}
- **Revenue impact:** {Estimated}
- **Duration:** {X minutes/hours}

## What Went Well

- Fast detection via alerting
- Quick rollback procedure

## What Went Wrong

- Missing integration test for checkout flow
- No canary deployment

## Action Items

| Action | Owner | Due Date |
|--------|-------|----------|
| Add checkout integration test | @dev | 2024-07-01 |
| Implement canary deployments | @devops | 2024-07-15 |

## Lessons Learned

{Key takeaways from this incident.}
```

---

## TEAM TEMPLATES

### Code Review Checklist

```markdown
# Code Review Checklist

## Functionality
- [ ] Code does what the PR description claims
- [ ] Edge cases are handled
- [ ] Error handling is appropriate
- [ ] No debug/console.log statements left

## Security
- [ ] No hardcoded secrets or credentials
- [ ] User input is validated
- [ ] SQL queries use parameterized statements
- [ ] Authentication/authorization is correct

## Performance
- [ ] No N+1 queries
- [ ] Large operations are paginated
- [ ] Caching is used appropriately
- [ ] No memory leaks

## Testing
- [ ] Unit tests for new logic
- [ ] Integration tests for API changes
- [ ] Test coverage maintained or improved

## Documentation
- [ ] Comments explain WHY, not WHAT
- [ ] Public APIs are documented
- [ ] README updated if needed

## Style
- [ ] Follows team style guide
- [ ] No linting errors
- [ ] Variable/function names are clear
```

### Tech Spec Template

```markdown
# Tech Spec: {Feature Name}

**Author:** {Name}

**Status:** Draft | In Review | Approved | Implemented

**Created:** {Date}

---

## Overview

{One paragraph summary of the feature}

## Goals

- {Goal 1}
- {Goal 2}

## Non-Goals (Out of Scope)

- {What we're NOT doing}

## Background

{Context and history}

## Detailed Design

### Data Model

```python
class Resource(Base):
    id: UUID
    name: str
    created_at: datetime
```

### API Design

| Endpoint | Method | Description |
|----------|--------|-------------|
| /api/resources | GET | List all |
| /api/resources | POST | Create new |
| /api/resources/{id} | GET | Get one |
| /api/resources/{id} | PUT | Update |
| /api/resources/{id} | DELETE | Delete |

### User Flows

1. User navigates to /resources
2. Clicks "New Resource"
3. Fills form, submits
4. Sees success message

## Open Questions

1. {Question}
```

### Onboarding Template

```markdown
# Engineering Onboarding Guide

Welcome to the team! This guide will help you get up to speed.

## Day 1: Setup

### Required Tools
- [ ] Install VS Code
- [ ] Install Docker Desktop
- [ ] Clone the main repo
- [ ] Request access to: GitHub, Railway, Datadog, PagerDuty

### First Day Checklist
- [ ] Development environment running locally
- [ ] Can run `make test` successfully
- [ ] Can deploy to staging
- [ ] Joined Slack channels: #engineering, #incidents, #deployments

## Week 1: Learning

### Read These First
1. ARCHITECTURE.md — System overview
2. API.md — API documentation
3. DEPLOYMENT.md — How we deploy

### Pair with Someone On
- [ ] Walk through codebase structure
- [ ] Review a recent PR
- [ ] Debug an issue together

## First Month Goals
- Ship your first PR (any size)
- Attend one on-call rotation
- Participate in one architecture decision
```

---

## AI PROMPTS FOR DOCUMENTATION GENERATION

Use these prompts with any LLM to generate documentation:

### Prompt 1: Generate ADR from Context

```
Generate an Architecture Decision Record (ADR) for the following technical decision.

Context:
- Problem: {describe the problem}
- Options considered: {list options}
- Chosen solution: {describe solution}
- Team: {team size and expertise}

Generate a complete ADR with:
1. Clear problem statement
2. Decision made with rationale
3. Consequences (positive and negative)
4. Alternatives considered with reasons for rejection
5. Related ADRs if any

Use the standard ADR template. Include specific technical details.
```

### Prompt 2: Generate Runbook from Template

```
Create a production runbook for: {scenario}

Include:
1. Overview of the scenario
2. Step-by-step procedure with exact commands
3. Verification steps to confirm success
4. Rollback procedure if something goes wrong
5. Escalation contacts

Make commands copy-pasteable. Include expected output.
```

### Prompt 3: Generate RFC

```
Create a Request for Comments (RFC) document for: {change being proposed}

Structure:
1. Summary
2. Motivation (why are we doing this)
3. Detailed design with technical specs
4. Implementation plan (phased)
5. Risks and mitigations
6. Alternatives considered
7. Open questions for discussion

Make it detailed enough for the team to make an informed decision.
```

### Prompt 4: Generate Post-Mortem

```
Write a post-mortem for the following incident:

Incident: {description}
Duration: {time}
Impact: {users affected, revenue impact}
Timeline:
- {time}: {event}
- {time}: {event}
- {time}: {event}

Root cause: {identified root cause}

Include:
1. Executive summary
2. Detailed timeline
3. Root cause analysis (use 5 Whys technique)
4. What went well / what went wrong
5. Action items with owners and due dates
```

### Prompt 5: Generate API Documentation

```
Generate API documentation for the following endpoints:

Service: {name}
Description: {what it does}

Endpoints:
{list endpoints with method, path, description}

For each endpoint, provide:
1. Description
2. Request parameters (query, path, body)
3. Response codes and body examples
4. Error responses
5. Example request/response

Use OpenAPI 3.1 compatible format.
```

### Prompt 6: Generate Code Review Checklist

```
Create a code review checklist for a {language} project.

Include sections for:
1. Functionality (does it work correctly)
2. Security (common vulnerabilities)
3. Performance (N+1, memory, scalability)
4. Testing (coverage, edge cases)
5. Code style (team conventions)
6. Documentation (comments, README)

Tailor checks to {language} specific best practices and common mistakes.
```

### Prompt 7: Generate Tech Spec

```
Create a technical specification (tech spec) for: {feature}

Include:
1. Overview and goals
2. Non-goals (out of scope)
3. Background and context
4. Detailed design:
   - Data model
   - API design (all endpoints)
   - User flows
   - Edge cases
5. Open questions
6. Success metrics

Make it detailed enough for another developer to implement without asking questions.
```

---

## HOW TO USE THIS SKILL

### Hermes Agent

```bash
# This skill loads automatically when you mention architecture documentation
```

### Claude Code

Create `.claude/skills/architecture-docs.md`:

```markdown
# Claude — Architecture Documentation

When asked to document architectural decisions, create ADRs, RFCs, or runbooks, use the templates from the DevOps Architecture Kit.
[Copy relevant templates here]
```

### Manual Use

Copy templates to your project:

```bash
mkdir -p docs/adr docs/rfc docs/runbooks
# Copy templates to respective directories
```

---

## FORMATTING STANDARDS

- **ADR files:** `docs/adr/ADR-{number}-{title}.md`
- **RFC files:** `docs/rfc/RFC-{number}-{title}.md`
- **Runbooks:** `docs/runbooks/{title}.md`
- **Team templates:** `docs/templates/{type}.md`

### Frontmatter for Automation

```yaml
---
title: "{Title}"
status: "{Status}"
date: "{YYYY-MM-DD}"
author: "{Author}"
type: "{adr|rfc|runbook}"
---
```

---

## BEST PRACTICES

1. **ADRs are permanent records** — Write as if documenting for future engineers who weren't present
2. **ADRs are immutable once accepted** — Create a new ADR to supersede, don't edit
3. **RFCs are for discussion** — Leave space for alternatives, not just the preferred solution
4. **Runbooks are tested procedures** — If you can't follow your runbook under pressure, it needs work
5. **Post-mortems are blameless** — Focus on system failures, not individual mistakes
6. **Use Mermaid for diagrams** — Charts make documentation more engaging

---

*Built by CodeBlueprint — AI Agent Tools for Developers*
