# Section 2: Constraints

## Purpose

Document boundaries that the architecture cannot change. Constraints limit design freedom and must be respected.

## Types of Constraints

### Technical Constraints

- **Existing systems**: Must integrate with legacy systems
- **Technology stack**: Mandated languages, frameworks, platforms
- **Standards**: Industry standards, company standards
- **Infrastructure**: Cloud provider, hardware limitations
- **Data formats**: Must support specific protocols/formats

### Organizational Constraints

- **Team structure**: Skills available, team size, locations
- **Timeline**: Hard deadlines, milestones
- **Budget**: Cost limitations
- **Processes**: Required methodologies (Agile, etc.)
- **Organizational structure**: Department boundaries, reporting lines

### Political Constraints

- **Internal politics**: Department boundaries, turf issues
- **External regulations**: GDPR, HIPAA, SOX compliance
- **Contracts**: Third-party licensing, SLAs
- **Strategic decisions**: Made by executives, non-negotiable

## Format

```markdown
## 2. Constraints

### Technical Constraints
| Constraint | Impact on Architecture |
|-----------|----------------------|
| [Constraint description] | [How it limits design] |

### Organizational Constraints
| Constraint | Impact on Architecture |
|-----------|----------------------|
| [Constraint description] | [How it limits design] |

### Political/Regulatory Constraints
| Constraint | Impact on Architecture |
|-----------|----------------------|
| [Constraint description] | [How it limits design] |
```

## Input Questions

**Technical:**
- What existing systems must be integrated?
- Are there mandated technologies?
- What standards must be followed?
- What infrastructure is provided?

**Organizational:**
- What skills does the team have?
- Are there hard deadlines?
- What is the budget range?
- What processes must be followed?

**Political:**
- Are there regulatory requirements (GDPR, HIPAA)?
- Are there licensing constraints?
- Are there strategic decisions already made?
- Are there political sensitivities to consider?

## Quality Checklist

- [ ] All hard constraints are documented
- [ ] Impact on architecture is explained
- [ ] Constraints are verifiable (not assumptions)
- [ ] Distinguish between constraints and assumptions
- [ ] Document who imposed each constraint

## Common Mistakes

❌ **Confusing constraints with goals** (constraints are fixed, goals are desired)  
❌ **Documenting assumptions as constraints**  
❌ **Not explaining the impact** (why does this constraint matter?)  
❌ **Missing organizational constraints** (often overlooked)  
❌ **Documenting constraints that can be changed**

## Example

```markdown
## 2. Constraints

### Technical Constraints
| Constraint | Impact |
|-----------|--------|
| Must integrate with legacy COBOL system | Requires message queue adapter; async communication only |
| Company standard: AWS cloud only | Cannot use Azure/GCP services; must use AWS-native solutions |
| Must support IE11 for internal users | Limits frontend framework choices; requires polyfills |
| Data must remain in EU (GDPR) | AWS eu-west-1 region only; no global CDN |

### Organizational Constraints
| Constraint | Impact |
|-----------|--------|
| Team: 4 backend, 2 frontend developers | Microservices only for clear boundaries; shared database acceptable |
| Hard deadline: 6 months to production | MVP scope; defer non-essential features |
| Budget: $50K/year infrastructure | Cost optimization is key; serverless preferred |

### Political/Regulatory Constraints
| Constraint | Impact |
|-----------|--------|
| GDPR compliance required | Data encryption at rest and in transit; right to erasure |
| PCI DSS for payment processing | Card data never touches application servers |
```
