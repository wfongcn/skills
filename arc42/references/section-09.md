# Section 9: Architecture Decisions

## Purpose

Document important architectural decisions with their context and consequences. ADRs (Architecture Decision Records) provide the "why" behind the architecture.

## When to Document

Document decisions that are:
- **Architecturally significant** (affect structure or quality)
- **Difficult to change** (constrains future decisions)
- **Not obvious** (alternatives were considered)
- **Costly if wrong** (high impact of mistake)

## ADR Format

Use a lightweight ADR format:

```markdown
### ADR-XXX: [Decision Title]

**状态 (Status):** [Proposed | Accepted | Deprecated | Superseded by ADR-YYY]
**日期 (Date):** YYYY-MM-DD
**决策者 (Decider):** [谁做的决定]

**背景 (Context):**
[我们在看到什么问题？什么情况催生了这次决策？]

**决策 (Decision):**
[我们决定做什么？]

**后果 (Consequences):**
- ✅ **正面 (Positive):** [带来的好处]
- ❌ **负面 (Negative):** [需要考虑的权衡/风险]
- ➡ **相关 (Related):** [相关的其他ADR]

**替代方案 (Alternatives Considered):**
- [方案1]: [为什么被拒绝]
- [方案2]: [为什么被拒绝]

**相关质量目标 (Related Quality Goals):**
- [关联的质量目标，如 #efficient, #reliable]
```

## Enhanced ADR Example

```markdown
### ADR-001: 采用前后端分离架构

**状态:** Accepted
**日期:** 2024-01-15
**决策者:** 技术团队

**背景:**
需要支持多平台访问，后端需要AI能力，前端需要快速迭代。

**决策:**
采用前后端分离架构：
- 前端：React SPA + TypeScript + Vite
- 后端：Python MCP Server

**后果:**
- ✅ 前端可以独立部署和迭代
- ✅ 后端专注于业务逻辑和AI集成
- ✅ 技术选型更灵活
- ❌ 需要处理跨域问题
- ❌ 前后端需要协调接口
- ➡ 相关 ADR-002: 使用MCP协议

**替代方案:**
- 方案A Monolith: 单一应用部署简单，但难以支持多前端
- 方案B Serverless: 降低运维成本，但AI集成复杂

**相关质量目标:**
- #flexible (灵活性)
- #efficient (高效性)
```

## Format

```markdown
## 9. Architecture Decisions

### ADR-001: [Title]

**Status:** Accepted

**Context:**
[Problem statement]

**Decision:**
[What was decided]

**Consequences:**
- Positive: [Benefits]
- Negative: [Trade-offs]
- Neutral: [Neutral effects]

**Alternatives Considered:**
- [Alternative 1]: [Why rejected]
- [Alternative 2]: [Why rejected]
```

## Input Questions

- What were the hardest architectural decisions?
- What alternatives were considered and rejected?
- What would be costly to change later?
- What might seem unusual and need explanation?
- What quality goals drove specific decisions?
- What constraints forced certain choices?

## Quality Checklist

- [ ] Important decisions are documented
- [ ] Each decision has context (problem)
- [ ] Decision is clearly stated
- [ ] Consequences (positive and negative) are listed
- [ ] Alternatives considered are mentioned
- [ ] Status is tracked (accepted, deprecated, etc.)
- [ ] Decisions are numbered for reference

## Common Mistakes

❌ **Documenting every small decision** (focus on significant ones)  
❌ **Missing context** (what problem was being solved?)  
❌ **No alternatives mentioned** (why was this the best choice?)  
❌ **Only positive consequences** (be honest about trade-offs)  
❌ **Outdated status** (deprecate superseded decisions)  
❌ **Too much detail** (link to detailed docs if needed)

## Example

```markdown
## 9. Architecture Decisions

### ADR-001: Microservices Architecture

**Status:** Accepted

**Context:**
The e-commerce platform needs to support multiple development teams working independently, with different release cycles and scaling requirements. A monolithic architecture would create coupling and deployment bottlenecks.

**Decision:**
Adopt a microservices architecture with services aligned to bounded contexts (Orders, Payments, Inventory, Notifications).

**Consequences:**
- Positive:
  - Independent deployment and scaling per service
  - Teams can choose optimal technologies per service
  - Failure isolation between domains
  - Easier to understand smaller codebases
- Negative:
  - Operational complexity (monitoring, logging across services)
  - Network latency and partial failure handling required
  - Data consistency challenges (distributed transactions)
  - Need for DevOps expertise
- Neutral:
  - Requires service mesh or API Gateway
  - Team structure must align with service boundaries

**Alternatives Considered:**
- **Modular Monolith:** Rejected because deployment coupling would still exist; teams wanted independent releases
- **Serverless Functions:** Rejected due to cold start latency concerns and vendor lock-in

---

### ADR-002: PostgreSQL as Primary Database

**Status:** Accepted

**Context:**
The system needs a reliable, ACID-compliant database that supports complex queries and has strong operational tooling. The team has PostgreSQL expertise.

**Decision:**
Use PostgreSQL as the primary database for all services requiring ACID semantics.

**Consequences:**
- Positive:
  - ACID compliance for data integrity
  - Rich query capabilities (JSON, full-text search)
  - Excellent operational tooling
  - Team familiarity reduces risk
- Negative:
  - Write scalability limited to single node
  - May need read replicas for query load
- Neutral:
  - Self-hosted vs. managed RDS to be decided per environment

**Alternatives Considered:**
- **MySQL:** Rejected due to inferior JSON support and partial ACID compliance in older versions
- **MongoDB:** Rejected because ACID compliance is critical for financial transactions
- **CockroachDB:** Rejected due to team unfamiliarity and higher cost

---

### ADR-003: Event Sourcing for Inventory

**Status:** Accepted

**Context:**
Inventory tracking requires a complete audit trail of all stock movements for compliance and debugging. Current state queries need to support "stock at specific time" scenarios.

**Decision:**
Implement Event Sourcing for the Inventory service, storing all stock movements as events.

**Consequences:**
- Positive:
  - Complete audit trail for compliance
  - Temporal queries (stock level at any point in time)
  - Can rebuild current state from events
  - Supports event-driven architecture
- Negative:
  - Learning curve for team new to event sourcing
  - Event schema evolution requires careful management
  - Higher storage requirements
  - Query performance requires projections/read models
- Neutral:
  - Requires event store (using PostgreSQL with JSONB)

**Alternatives Considered:**
- **Traditional CRUD with audit table:** Rejected because temporal queries would be complex and slow
- **Append-only log with snapshots:** Similar to event sourcing but less structured
```
