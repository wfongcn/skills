# Section 1: Introduction and Goals

## Purpose

Introduce stakeholders to the system's fundamental driving forces and establish quality goals. This section sets the foundation for all architectural decisions.

## Subsections

### 1.1 Requirements Overview

**Content:**
- Brief summary of functional requirements (1 paragraph)
- Essential features (5-10 bullet points)
- Business context (value proposition)
- References to detailed requirements documents

**Rules:**
- Keep brief (< 1 page)
- Only architecturally relevant requirements
- Link to existing docs instead of duplicating
- Focus on THIS system only

**Input Questions:**
- What is the system's primary purpose?
- What problem does it solve?
- Who benefits from this system?
- What are the 5-10 essential features?
- Where are detailed requirements documented?

---

### 1.2 Quality Goals (MANDATORY)

**CRITICAL:** These are the top 3-5 quality requirements of highest importance. All architectural decisions must support these goals.

**Format:**

| Priority | Quality Goal | Concrete Scenario |
|:--------:|-------------|-------------------|
| **1** | [Q42 property] | [Measurable scenario with numbers] |
| **2** | [Q42 property] | [Measurable scenario with numbers] |
| **3** | [Q42 property] | [Measurable scenario with numbers] |

**Q42 Quality Properties:**
- **#reliable**: Available, fault-tolerant, accurate
- **#flexible**: Adaptable, maintainable, extensible
- **#efficient**: Fast response, high throughput, low resource
- **#usable**: Learnable, easy to operate, accessible
- **#safe**: Risk-free, fail-safe, hazard warnings
- **#secure**: Confidential, authentic, access-controlled
- **#suitable**: Functionally complete, correct, testable
- **#operable**: Easy to install, deploy, monitor

**Example Quality Goals:**

| Priority | Quality Goal | Concrete Scenario |
|:--------:|-------------|-------------------|
| **1** | #efficient | Response time for search queries < 200ms at 95th percentile under 1000 concurrent users |
| **2** | #reliable | System availability 99.9% (max 8.76 hours downtime/year), automatic failover < 30 seconds |
| **3** | #flexible | New payment provider integration possible within 2 weeks without core changes |

**Rules:**
- Maximum 3-5 goals (not more!)
- Must be concrete and measurable
- Use specific numbers, not vague terms
- Must be signed by stakeholders before architecture work
- These drive ALL architectural decisions

**Input Questions:**
- What are the top 3 things that must NOT fail?
- What performance numbers matter? (response time, throughput, users)
- How much downtime is acceptable?
- How quickly must the system adapt to changes?
- What security/compliance requirements exist?

---

### 1.3 Stakeholders

**Content:**

| Role/Name | Contact | Expectations from Architecture |
|-----------|---------|-------------------------------|
| [Role] | [Name/Contact] | [What they need from this doc] |

**Common Stakeholders:**
- **Product Owner**: Features, roadmap alignment
- **Development Team**: Implementation guidance, tech decisions
- **Operations**: Deployment, monitoring, troubleshooting
- **Security Team**: Compliance, threat model
- **Management**: Resource planning, risk assessment
- **End Users**: Performance, usability

**Rules:**
- Include all who need to understand/use this architecture
- Document their specific expectations
- Helps focus documentation on what matters

**Input Questions:**
- Who needs to understand this architecture?
- Who makes decisions based on this document?
- Who will implement/maintain this system?
- Who is responsible for operations?
- Are there external stakeholders (customers, regulators)?

## Quality Checklist

- [ ] Requirements overview fits on 1 page
- [ ] Quality goals are 3-5 items maximum
- [ ] Quality goals use Q42 properties or ISO 25010
- [ ] Quality goals have concrete, measurable scenarios
- [ ] Stakeholder table is complete
- [ ] All stakeholders have documented expectations
- [ ] Quality goals are ready for stakeholder sign-off

## Common Mistakes

❌ **Too many quality goals** (more than 5)  
❌ **Vague goals** ("high performance" without numbers)  
❌ **Project goals instead of architecture goals** ("finish by Q3")  
❌ **Skipping stakeholder table**  
❌ **Duplicating requirements documents** instead of linking

## Examples

### Good Quality Goal:
> "Response time for search queries < 200ms at 95th percentile under 1000 concurrent users"

### Bad Quality Goal:
> "High performance and user-friendly" (vague, not measurable)
