# Section 11: Risks and Technical Debt

## Purpose

Document known risks, technical debt, and problems in the architecture. This creates transparency and helps prioritize remediation work.

## Risks vs. Technical Debt

**Risks:**
- Potential future problems
- Things that might go wrong
- Uncertainties

**Technical Debt:**
- Known suboptimal implementations
- Conscious shortcuts taken
- Areas needing refactoring

## Risk Format

```markdown
| ID | Risk | Probability | Impact | Mitigation | Owner |
|----|------|-------------|--------|------------|-------|
| R-XX | [Description] | [H/M/L] | [H/M/L] | [Strategy] | [Name] |
```

**Risk Assessment:**
- **Probability**: Likelihood of occurrence (High/Medium/Low)
- **Impact**: Severity if it occurs (High/Medium/Low)
- **Risk Level**: Combine P × I (Critical/High/Medium/Low)

## Technical Debt Format

```markdown
| ID | Debt | Location | Reason | Impact | Remediation | Priority |
|----|------|----------|--------|--------|-------------|----------|
| TD-XX | [Description] | [Component] | [Why taken] | [Consequence] | [How to fix] | [H/M/L] |
```

## Format

```markdown
## 11. Risks and Technical Debt

### 11.1 Risks

| ID | Risk | P | I | Mitigation | Owner |
|----|------|---|---|------------|-------|
| R-01 | [Description] | H | M | [Strategy] | [Name] |

**Risk Details:**

**R-01: [Title]**
- **Description:** [Detailed explanation]
- **Trigger:** [What would cause this]
- **Consequences:** [What happens if it occurs]
- **Mitigation:** [Current and planned actions]

### 11.2 Technical Debt

| ID | Debt | Location | Reason | Impact | Remediation | Priority |
|----|------|----------|--------|--------|-------------|----------|
| TD-01 | [Description] | [Where] | [Why] | [Effect] | [Fix plan] | H/M/L |

**Debt Details:**

**TD-01: [Title]**
- **Current State:** [What exists now]
- **Desired State:** [What it should be]
- **Reason for Debt:** [Why shortcut was taken]
- **Interest Paid:** [Ongoing costs]
- **Repayment Plan:** [When/how to fix]
```

## Common Risks to Consider

### Technical Risks
- Technology obsolescence
- Scalability limitations
- Security vulnerabilities
- Performance bottlenecks
- Single points of failure

### Organizational Risks
- Key person dependency
- Skill gaps
- Team turnover
- Vendor lock-in

### External Risks
- Regulatory changes
- Third-party service failures
- Market/competitive changes

## Input Questions

- What could go wrong with this architecture?
- What are we unsure about?
- What shortcuts have been taken?
- What needs refactoring?
- What are the single points of failure?
- What skills might we lack?
- What technologies might become obsolete?

## Quality Checklist

- [ ] Important risks are identified
- [ ] Risks have probability and impact ratings
- [ ] Mitigation strategies are documented
- [ ] Risk owners are assigned
- [ ] Technical debt is cataloged
- [ ] Debt has remediation plans
- [ ] Priorities are assigned

## Common Mistakes

❌ **Only documenting technical risks** (organizational too)  
❌ **No mitigation strategies** (just listing problems)  
❌ **Confusing risks and issues** (risks are future, issues are now)  
❌ **No priorities** (everything is critical)  
❌ **Hiding debt** (be transparent about shortcuts)  
❌ **No owners** (who is responsible?)

## Example

```markdown
## 11. Risks and Technical Debt

### 11.1 Risks

| ID | Risk | Probability | Impact | Level | Owner |
|----|------|-------------|--------|-------|-------|
| R-01 | Payment provider outage | Medium | High | Critical | Sarah (DevOps) |
| R-02 | Database performance degradation | Medium | Medium | High | Mike (Backend) |
| R-03 | Key developer departure | Low | High | Medium | Lisa (Manager) |
| R-04 | Redis cluster split-brain | Low | Medium | Low | Sarah (DevOps) |

**R-01: Payment Provider Outage**
- **Description:** Primary payment provider (Stripe) experiences extended outage
- **Probability:** Medium (occurred twice in industry in past year)
- **Impact:** High (cannot process orders, revenue loss)
- **Mitigation:**
  - Implemented: Circuit breaker pattern (fail fast)
  - Planned: Secondary payment provider (Q2 2024)
  - Planned: Queue orders for retry (Q1 2024)
- **Owner:** Sarah (DevOps Lead)
- **Status:** Monitoring, secondary provider evaluation in progress

**R-02: Database Performance Degradation**
- **Description:** Order table growth causes query slowdown
- **Probability:** Medium (table growing 1M rows/month)
- **Impact:** Medium (slow queries, potential timeouts)
- **Mitigation:**
  - Implemented: Query optimization, indexes
  - Planned: Table partitioning by date (Q1 2024)
  - Planned: Read replicas for analytics (Q2 2024)
- **Owner:** Mike (Backend Lead)
- **Trigger:** Query time > 500ms at 95th percentile

**R-03: Key Developer Departure**
- **Description:** Loss of senior developer with critical system knowledge
- **Probability:** Low (team stable, good culture)
- **Impact:** High (knowledge silo in Payment Service)
- **Mitigation:**
  - Implemented: Documentation of Payment Service
  - In Progress: Pair programming, knowledge sharing
  - Planned: Cross-training another developer
- **Owner:** Lisa (Engineering Manager)

---

### 11.2 Technical Debt

| ID | Debt | Location | Reason | Impact | Priority |
|----|------|----------|--------|--------|----------|
| TD-01 | Order service too large | Order Service | Time pressure at MVP | Slow development | High |
| TD-02 | No API versioning | Public API | Not needed initially | Breaking changes risk | Medium |
| TD-03 | Direct DB access from analytics | Inventory DB | Reporting urgency | Performance impact | Medium |
| TD-04 | Manual deployment steps | Payment Service | Complex setup | Deployment risk | Low |

**TD-01: Order Service Too Large (Monolith Component)**
- **Current State:** Order Service handles orders, payments, shipping logic (~15K lines)
- **Desired State:** Separate Payment and Shipping services
- **Reason for Debt:** Time pressure to launch MVP; team was small
- **Interest Paid:**
  - Slower development (tight coupling)
  - Risky deployments (large blast radius)
  - Testing complexity
- **Repayment Plan:**
  - Phase 1: Extract Payment Service (Q2 2024)
  - Phase 2: Extract Shipping Service (Q3 2024)
- **Priority:** High
- **Owner:** Mike (Backend Lead)

**TD-02: No API Versioning**
- **Current State:** Public API has no versioning scheme
- **Desired State:** URL versioning (/v1/, /v2/)
- **Reason for Debt:** Only internal clients initially
- **Interest Paid:** Risk of breaking mobile app on changes
- **Repayment Plan:** Implement versioning before next breaking change
- **Priority:** Medium
- **Owner:** Alex (API Lead)

**TD-03: Direct Database Access for Analytics**
- **Current State:** Analytics tools query production PostgreSQL directly
- **Desired State:** Read replica or data warehouse
- **Reason for Debt:** Urgent reporting needs at launch
- **Interest Paid:** Query performance impact on production
- **Repayment Plan:** Set up read replica (Q1 2024)
- **Priority:** Medium
- **Owner:** Sarah (DevOps)
```
