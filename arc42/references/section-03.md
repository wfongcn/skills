# Section 3: Context and Scope

## Purpose

Define what is IN the system and what is OUT. Show the system's boundary and its relationships with external entities.

## Subsections

### 3.1 Business Context

**Purpose:** Show the system from a business/domain perspective - who uses it and for what.

**Format:**
- Diagram: System in center, external actors/systems around it
- Table: Explaining each external entity

**Diagram Elements:**
- Center box: Your system (black box)
- Left side: External actors (users, roles)
- Right side: External systems
- Arrows: Information flow (labeled with data exchanged)

**Table Format:**
| External Entity | Description | Responsibilities (theirs) | Input to System | Output from System |
|-----------------|-------------|--------------------------|-----------------|-------------------|
| [Name] | [What/who] | [What they do] | [Data they provide] | [Data they receive] |

**Input Questions:**
- Who are the users? (roles, personas)
- What external systems interact with this?
- What data comes into the system?
- What data goes out of the system?
- What are the main use cases from a business view?

---

### 3.2 Technical Context

**Purpose:** Show the system from a technical perspective - interfaces, protocols, technologies.

**Format:**
- Diagram: Similar to business context but with technical details
- Table: Technical interface specifications

**Diagram Elements:**
- Center box: Your system
- Surrounding boxes: External technical systems/interfaces
- Arrows: Labeled with protocol and data format

**Table Format:**
| Interface | Technology/Protocol | Data Format | Direction | Description |
|-----------|---------------------|-------------|-----------|-------------|
| [Name] | [REST/HTTP, gRPC, etc.] | [JSON, XML, etc.] | [In/Out/Both] | [Purpose] |

**Input Questions:**
- What APIs does the system expose?
- What external APIs does it call?
- What message queues/topics are used?
- What databases does it connect to?
- What file systems or storage?
- What authentication mechanisms?

## Quality Checklist

- [ ] System boundary is clearly defined
- [ ] All external actors are identified
- [ ] All external systems are identified
- [ ] Information flow is documented
- [ ] Both business and technical views are provided
- [ ] Diagrams have legends
- [ ] Tables are complete for all external entities

## Common Mistakes

❌ **Missing external systems** (only showing users)  
❌ **Showing internal details** (should be black box)  
❌ **Unclear what is in/out of scope**  
❌ **Missing data formats/protocols** (technical context)  
❌ **Confusing business and technical context**

## Example

```markdown
## 3. Context and Scope

### 3.1 Business Context

```
+----------------+         Orders         +----------------+
|   Customer     | ----------------------> |              |
|   (Web/Mobile) | <---------------------- |   E-Commerce |
+----------------+      Order Status      |   System     |
                                          |              |
+----------------+     Inventory Query    |   [Scope]    |
|   Warehouse    | <---------------------> |              |
|    Staff       |    Stock Updates       |              |
+----------------+                        +----------------+
       ^                                           |
       |           Shipping Requests               v
       +-----------------------------------+---------------+
                                           |  Shipping     |
                                           |  Provider     |
                                           +---------------+
```

| External Entity | Description | Input to System | Output from System |
|-----------------|-------------|-----------------|-------------------|
| Customer | End users via web/mobile app | Orders, payments | Order confirmation, tracking |
| Warehouse Staff | Internal fulfillment team | Stock updates | Pick lists, shipping requests |
| Shipping Provider | External logistics partner | Tracking updates | Shipping requests, labels |

### 3.2 Technical Context

| Interface | Protocol | Data Format | Direction | Description |
|-----------|----------|-------------|-----------|-------------|
| Customer API | REST/HTTPS | JSON | In/Out | Customer-facing API for orders |
| Payment Gateway | REST/HTTPS | JSON | Out | Stripe API for payments |
| Warehouse WMS | gRPC | Protobuf | Both | Real-time inventory sync |
| Shipping API | REST/HTTPS | JSON | Out | FedEx/UPS API for shipping |
| Email Service | SMTP | MIME | Out | Transactional emails via SendGrid |
| Database | PostgreSQL wire | SQL | Both | Primary data store |
| Cache | Redis | RESP | Both | Session and query caching |
```
