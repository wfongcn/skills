# Section 8: Crosscutting Concepts

## Purpose

Document concepts and rules that apply across multiple building blocks. These are overarching concerns that don't fit in a single component.

## When to Document

Include concepts that:
- Apply to multiple components
- Need consistent implementation
- Are fundamental to the architecture
- Would be duplicated if documented per component

## Common Crosscutting Concepts

### Technical Concepts
- **Security**: Authentication, authorization, encryption
- **Persistence**: ORM patterns, transaction handling, caching
- **Communication**: API design, error handling, retries
- **Logging**: Structured logging, correlation IDs
- **Monitoring**: Metrics, health checks, tracing

### Domain Concepts
- **Domain Model**: Core entities, value objects
- **Validation Rules**: Cross-field validation
- **Business Rules**: Invariants that span components

### Architectural Concepts
- **Transaction Management**: Saga patterns, consistency
- **Error Handling**: Global exception handling
- **Configuration**: Externalized configuration
- **Testing**: Test strategies, test data

## Format

```markdown
## 8. Crosscutting Concepts

### 8.1 [Concept Name]

**Motivation:** [Why this concept matters]

**Concept Description:**
[Detailed explanation]

**Implementation:**
- [How it's implemented]
- [Code examples or patterns]

**Constraints:**
- [Rules that must be followed]

**Affected Components:**
- [Which components use this concept]
```

## Input Questions

- What concepts span multiple components?
- What needs to be consistent across the system?
- What security patterns are used?
- How is error handling standardized?
- What is the domain model?
- What testing approaches are used?
- What logging/monitoring standards exist?

## Quality Checklist

- [ ] Important crosscutting concepts are documented
- [ ] Each concept has clear motivation
- [ ] Implementation guidance is provided
- [ ] Constraints/rules are stated
- [ ] Affected components are listed
- [ ] Examples are included where helpful

## Common Mistakes

❌ **Documenting everything** (only crosscutting concerns)  
❌ **Implementation details** (should be in code docs)  
❌ **Concepts that belong in one component**  
❌ **Missing motivation** (why does this concept exist?)  
❌ **Not stating constraints** (what must developers do?)

## Example

```markdown
## 8. Crosscutting Concepts

### 8.1 Security

**Motivation:** All services must implement consistent security measures for authentication, authorization, and data protection.

**Authentication:**
- JWT tokens issued by Auth0
- Tokens expire after 1 hour
- Refresh tokens valid for 7 days
- All services validate tokens via JWKS endpoint

**Authorization:**
- RBAC (Role-Based Access Control)
- Roles: CUSTOMER, ADMIN, WAREHOUSE_STAFF
- Permissions checked at API Gateway and service level
- Service-to-service calls use mTLS

**Data Protection:**
- PII encrypted at rest (AES-256)
- TLS 1.3 for all communications
- Credit card data: PCI DSS compliant, tokenized by Stripe

**Affected Components:** All services, API Gateway

---

### 8.2 Domain Model

**Motivation:** Consistent domain language across all bounded contexts.

**Core Entities:**

```
┌─────────────┐       ┌─────────────┐       ┌─────────────┐
│   Order     │◄──────│ OrderItem   │──────►│   Product   │
├─────────────┤       ├─────────────┤       ├─────────────┤
│ id: UUID    │       │ id: UUID    │       │ id: UUID    │
│ status: Enum│       │ quantity:Int│       │ name: String│
│ total: Money│       │ price: Money│       │ sku: String │
│ customerId  │       │ orderId: FK │       │             │
└─────────────┘       └─────────────┘       └─────────────┘
```

**Value Objects:**
- Money: amount (BigDecimal) + currency (ISO code)
- Address: street, city, postalCode, country

**Business Rules:**
- Order total = sum of item quantities × prices
- Cannot cancel shipped orders
- Quantity must be positive

**Affected Components:** Order Service, Inventory Service

---

### 8.3 Error Handling

**Motivation:** Consistent error responses across all APIs for client compatibility and debugging.

**Error Response Format:**
```json
{
  "error": {
    "code": "INSUFFICIENT_INVENTORY",
    "message": "Not enough stock for product SKU-123",
    "details": {
      "productId": "SKU-123",
      "requested": 10,
      "available": 5
    },
    "correlationId": "abc-123-def",
    "timestamp": "2024-01-15T10:30:00Z"
  }
}
```

**HTTP Status Codes:**
- 400: Validation errors
- 401: Authentication required
- 403: Permission denied
- 404: Resource not found
- 409: Business rule violation
- 500: Internal server error

**Exception Hierarchy:**
- DomainException → Business rule violations (400/409)
- NotFoundException → Resource not found (404)
- InfrastructureException → External service failures (502/504)

**Correlation IDs:**
- Generated at API Gateway
- Passed in X-Correlation-ID header
- Logged with all requests
- Included in error responses

**Affected Components:** All services, API Gateway

---

### 8.4 Logging

**Motivation:** Observable system with structured logs for debugging and monitoring.

**Log Levels:**
- ERROR: Exceptions, failures requiring action
- WARN: Degraded functionality, retries
- INFO: Business events (order created, payment processed)
- DEBUG: Detailed diagnostics (disabled in prod)

**Structured Log Format (JSON):**
```json
{
  "timestamp": "2024-01-15T10:30:00Z",
  "level": "INFO",
  "service": "order-service",
  "correlationId": "abc-123",
  "message": "Order created",
  "context": {
    "orderId": "ORD-456",
    "customerId": "CUST-789",
    "amount": 99.99
  }
}
```

**Required Fields:**
- timestamp (ISO 8601)
- level
- service name
- correlationId
- message

**Affected Components:** All services
```
