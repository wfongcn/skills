# Section 4: Solution Strategy

## Purpose

Summarize the fundamental decisions and solution approaches at a high level. This section provides the strategic foundation that explains WHY the architecture is the way it is.

## Content

**What to include:**
1. **Top-level decomposition** - How is the system divided?
2. **Key architectural patterns** - What patterns are used and why?
3. **Technology stack overview** - Main technologies and rationale
4. **Strategies for achieving quality goals** - How each quality goal is addressed
5. **Organizational decisions** - Team structure, development approach

## Format

```markdown
## 4. Solution Strategy

### 4.1 Overview
[2-3 paragraph summary of the overall approach]

### 4.2 Architectural Patterns
| Pattern | Application | Rationale |
|---------|-------------|-----------|
| [Pattern name] | [Where applied] | [Why chosen] |

### 4.3 Technology Decisions
| Category | Technology | Rationale |
|----------|------------|-----------|
| [Backend/Frontend/DB/etc.] | [Choice] | [Why] |

### 4.4 Achieving Quality Goals
| Quality Goal | Strategy |
|--------------|----------|
| [Goal from Section 1.2] | [How architecture addresses it] |
```

## Input Questions

- What is the top-level decomposition of the system?
- What architectural patterns are used (microservices, layered, hexagonal, etc.)?
- Why were these patterns chosen?
- What are the main technologies and why?
- How does the architecture address each quality goal?
- Are there any innovative or unusual aspects?
- What alternatives were considered and rejected?

## Key Decisions to Document

### Structural Decisions
- Monolith vs. Microservices vs. Modular Monolith
- Layered vs. Hexagonal vs. Clean Architecture
- Synchronous vs. Asynchronous communication

### Technology Decisions
- Programming languages
- Frameworks
- Databases
- Message systems
- Infrastructure

### Organizational Decisions
- Team structure (Conway's Law)
- Repository strategy (mono vs. poly repo)
- Deployment approach

## Quality Checklist

- [ ] Overall strategy is explained in 2-3 paragraphs
- [ ] Key patterns are documented with rationale
- [ ] Technology decisions have justification
- [ ] Each quality goal from Section 1.2 has a strategy
- [ ] Alternatives considered are mentioned (briefly)
- [ ] Decisions are consistent with constraints (Section 2)

## Common Mistakes

❌ **Listing technologies without rationale**  
❌ **Missing the "why"** (only describing "what")  
❌ **Not linking to quality goals**  
❌ **Being too detailed** (save details for Section 5+)  
❌ **Inconsistent with constraints**  
❌ **Not mentioning rejected alternatives**

## Example

```markdown
## 4. Solution Strategy

### 4.1 Overview
The E-Commerce Platform uses a microservices architecture with clear bounded contexts aligned to business capabilities. Services communicate asynchronously via events for loose coupling, with synchronous REST APIs for user-facing operations. The system follows a hexagonal architecture pattern within each service to maintain testability and allow technology changes.

### 4.2 Architectural Patterns

| Pattern | Application | Rationale |
|---------|-------------|-----------|
| Microservices | Service per bounded context (Orders, Inventory, Payments) | Supports independent deployment and scaling; aligns with team structure |
| Hexagonal Architecture | Inside each service | Enables testing without external dependencies; allows swapping infrastructure |
| CQRS | Order service: separate read/write models | Optimizes for different access patterns; supports complex queries |
| Event Sourcing | Inventory service | Complete audit trail; supports temporal queries for stock levels |
| Saga Pattern | Distributed transactions | Maintains consistency across services without 2PC |

### 4.3 Technology Decisions

| Category | Technology | Rationale |
|----------|------------|-----------|
| Backend | Kotlin + Spring Boot | Team expertise; excellent async support; mature ecosystem |
| Frontend | React + TypeScript | Component reuse; strong typing; large talent pool |
| Database | PostgreSQL (primary) | ACID compliance; JSON support; proven reliability |
| Cache | Redis | Sub-millisecond latency; pub/sub for events |
| Message Queue | RabbitMQ | Mature; excellent routing; team familiarity |
| Infrastructure | Kubernetes on AWS | Auto-scaling; self-healing; infrastructure as code |

### 4.4 Achieving Quality Goals

| Quality Goal | Strategy |
|--------------|----------|
| Response time < 200ms | Redis caching; read replicas; CDN for static assets; async processing |
| 99.9% availability | Multi-AZ deployment; circuit breakers; graceful degradation; health checks |
| New payment provider in 2 weeks | Payment service abstraction; strategy pattern; plugin architecture |
```

## Relationship to Other Sections

- **Section 1.2**: Links quality goals to strategies
- **Section 2**: Ensures decisions respect constraints
- **Section 5**: Provides context for building block decisions
- **Section 9**: References detailed ADRs for major decisions
