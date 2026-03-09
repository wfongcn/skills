# Section 12: Glossary

## Purpose

Define important domain and technical terms to ensure common understanding among all stakeholders. The glossary reduces misunderstandings and provides a ubiquitous language.

## What to Include

### Domain Terms
- Business concepts
- Domain entities
- Process terms
- Industry-specific terminology

### Technical Terms
- Architecture patterns
- Technology names
- Acronyms and abbreviations
- Internal project names

## Format

```markdown
## 12. Glossary

| Term | Definition | Context |
|------|------------|---------|
| [Term] | [Clear definition] | [Where used] |

### Domain Terms

| Term | Definition |
|------|------------|
| [Business term] | [Definition] |

### Technical Terms

| Term | Definition |
|------|------------|
| [Technical term] | [Definition] |

### Abbreviations

| Abbreviation | Full Form |
|--------------|-----------|
| [Short] | [Long form] |
```

## Input Questions

- What domain terms might be unclear?
- What technical terms need explanation?
- What acronyms are used?
- Are there terms with multiple meanings?
- What are the core business concepts?
- What is the ubiquitous language?

## Quality Checklist

- [ ] Domain terms are defined
- [ ] Technical terms are explained
- [ ] All abbreviations are expanded
- [ ] Definitions are clear and unambiguous
- [ ] Context is provided where needed
- [ ] Terms are consistent with the document

## Common Mistakes

❌ **Including obvious terms** (HTTP, "database")  
❌ **Vague definitions** (circular definitions)  
❌ **Missing important terms** (domain concepts)  
❌ **Inconsistent with document** (terms used differently)  
❌ **Too long** (definitions should be concise)  
❌ **No context** (where is this term used?)

## Example

```markdown
## 12. Glossary

### Domain Terms

| Term | Definition |
|------|------------|
| **Order** | A customer's request to purchase products, including items, quantities, shipping address, and payment information. |
| **Order Line** | A single product line within an order, specifying the product, quantity, and price at time of purchase. |
| **SKU** | Stock Keeping Unit - unique identifier for a product variant (e.g., "SHIRT-RED-L"). |
| **Inventory Reservation** | Temporary hold on inventory items while an order is being processed, preventing overselling. |
| **Fulfillment** | The process of picking, packing, and shipping an order to the customer. |
| **Backorder** | An order for items not currently in stock, to be fulfilled when inventory is available. |
| **Abandoned Cart** | A shopping cart with items that was not converted to an order within a defined time period. |
| **Payment Provider** | Third-party service that processes credit card and alternative payment transactions (e.g., Stripe, PayPal). |
| **Chargeback** | A reversal of a credit card transaction initiated by the customer through their bank. |

### Technical Terms

| Term | Definition |
|------|------------|
| **Microservice** | An independently deployable service that owns a specific business capability and communicates via APIs. |
| **Event Sourcing** | A pattern where state changes are stored as a sequence of events, allowing state reconstruction and audit trails. |
| **CQRS** | Command Query Responsibility Segregation - separating read and write operations to optimize each independently. |
| **Saga Pattern** | A sequence of local transactions where each updates data and publishes an event within a single service. |
| **Circuit Breaker** | A pattern that prevents cascading failures by stopping requests to a failing service and providing fallback behavior. |
| **Idempotency** | Property of an operation where multiple identical requests have the same effect as a single request. |
| **Eventual Consistency** | A consistency model where data changes propagate asynchronously, and all replicas converge to the same value over time. |
| **JWT** | JSON Web Token - compact, URL-safe token format used for authentication and claims transmission. |
| **Materialized View** | A precomputed view of data optimized for specific query patterns, updated asynchronously. |
| **Hot Path** | Code execution path that is frequently executed and has strict performance requirements. |

### Abbreviations

| Abbreviation | Full Form | Description |
|--------------|-----------|-------------|
| **API** | Application Programming Interface | Interface for programmatic access to services |
| **ADR** | Architecture Decision Record | Document capturing important architectural decisions |
| **ALB** | Application Load Balancer | AWS layer 7 load balancer |
| **CQRS** | Command Query Responsibility Segregation | Architectural pattern separating reads and writes |
| **CRUD** | Create, Read, Update, Delete | Basic data operations |
| **EKS** | Elastic Kubernetes Service | AWS managed Kubernetes service |
| **GDPR** | General Data Protection Regulation | EU data privacy regulation |
| **gRPC** | Google Remote Procedure Call | High-performance RPC framework |
| **HA** | High Availability | System design ensuring operational continuity |
| **HPA** | Horizontal Pod Autoscaler | Kubernetes auto-scaling mechanism |
| **ISO** | International Organization for Standardization | Standards body |
| **JSON** | JavaScript Object Notation | Lightweight data interchange format |
| **JWT** | JSON Web Token | Token format for secure claims transmission |
| **MFA** | Multi-Factor Authentication | Security requiring multiple verification methods |
| **MVP** | Minimum Viable Product | Minimum features to launch |
| **ORM** | Object-Relational Mapping | Technique for converting data between systems |
| **PCI DSS** | Payment Card Industry Data Security Standard | Security standard for card payments |
| **PII** | Personally Identifiable Information | Data that can identify individuals |
| **REST** | Representational State Transfer | Architectural style for networked applications |
| **RPO** | Recovery Point Objective | Maximum acceptable data loss in disaster |
| **RTO** | Recovery Time Objective | Maximum acceptable downtime in disaster |
| **RPC** | Remote Procedure Call | Protocol for executing code on remote servers |
| **SKU** | Stock Keeping Unit | Unique product identifier |
| **SLA** | Service Level Agreement | Commitment between provider and customer |
| **SNS** | Simple Notification Service | AWS pub/sub messaging service |
| **SQS** | Simple Queue Service | AWS managed message queue |
| **TLS** | Transport Layer Security | Cryptographic protocol for secure communication |
| **UUID** | Universally Unique Identifier | 128-bit unique identifier |
| **VPC** | Virtual Private Cloud | Isolated virtual network in AWS |
| **WMS** | Warehouse Management System | Software for managing warehouse operations |

### Project-Specific Terms

| Term | Definition |
|------|------------|
| **Q42** | arc42's quality model with 8 properties (reliable, flexible, efficient, usable, safe, secure, suitable, operable). |
| **Arc42** | Open-source template for software architecture documentation. |
| **Order Service** | Microservice responsible for order lifecycle management. |
| **Payment Service** | Microservice handling payment processing and refunds. |
| **Inventory Service** | Microservice managing stock levels and reservations. |
```

## Tips for Good Definitions

1. **Be concise**: One to three sentences maximum
2. **Be specific**: Avoid vague or circular definitions
3. **Use consistently**: Apply the same definition throughout the document
4. **Link related terms**: Reference other glossary terms where relevant
5. **Include context**: Note if term has different meanings in different contexts
6. **Review with domain experts**: Ensure accuracy of business terms
