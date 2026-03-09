# Section 6: Runtime View

## Purpose

Show the dynamic behavior of the system through concrete scenarios. This complements the static Building Block View by illustrating how components interact at runtime.

## When to Document

Document runtime scenarios that are:
- **Important use cases** (core business scenarios)
- **Critical error handling** (failure scenarios)
- **Performance-critical paths** (bottlenecks)
- **Complex interactions** (hard to understand from static view)
- **Security-critical flows** (authentication, authorization)

## Scenarios to Document

### Primary Scenarios (Happy Path)
- Main success scenarios
- Most frequent operations

### Error Scenarios
- Failure handling
- Recovery procedures
- Edge cases

### Special Scenarios
- Startup/shutdown
- Scaling events
- Data migration
- Batch processing

## Notation Options

1. **Sequence Diagram (Recommended)**
   - Shows temporal ordering
   - Clear lifelines
   - Good for complex interactions

2. **Activity Diagram**
   - Shows control flow
   - Good for decision logic
   - BPMN is an option

3. **Flowchart**
   - Simple and accessible
   - Good for basic scenarios

## Format

```markdown
### 6.1 [Scenario Name]

**Scope:** [What part of the system is shown]

**Level:** [Level of abstraction]

**Primary Actor:** [Who initiates]

**Precondition:** [What must be true before]

**Postcondition:** [What is true after]

```
[Diagram]
```

**Process:**
1. [Step 1 description]
2. [Step 2 description]
3. ...

**Exception Paths:**
- **[Exception 1]:** [What happens]
```

## Input Questions

- What are the most important use cases?
- What happens when things go wrong?
- Which scenarios are performance-critical?
- Are there complex multi-step processes?
- How is data consistency maintained across components?
- What are the security-critical flows?

## Quality Checklist

- [ ] Most important scenarios are documented
- [ ] Error scenarios are included
- [ ] Diagrams are clear and readable
- [ ] Participants match Building Block View
- [ ] Sequence/timing is correct
- [ ] Preconditions and postconditions are stated
- [ ] Exception paths are documented

## Common Mistakes

❌ **Documenting every use case** (focus on important/complex ones)  
❌ **Inconsistent with Building Block View** (different component names)  
❌ **Missing error scenarios**  
❌ **Too many scenarios** (5-10 is usually enough)  
❌ **Not showing the "why"** (just the "what")  
❌ **Overly complex diagrams** (split if needed)

## Example

```markdown
### 6.1 Place Order (Happy Path)

**Scope:** Order placement process

**Level:** Cross-service interaction

**Primary Actor:** Customer

**Precondition:** Customer authenticated; items in cart

**Postcondition:** Order created; payment initiated; inventory reserved

```
Customer     Order Svc    Payment Svc   Inventory Svc   DB
   |              |              |              |        |
   | 1. POST /orders             |              |        |
   |-------------➜|              |              |        |
   |              | 2. Validate cart             |        |
   |              |-------------➜|              |        |
   |              |              | 3. Reserve items      |
   |              |              |-------------➜|        |
   |              |              |              | 4. Update stock
   |              |              |              |------➜|
   |              |              | 5. Reserved  |        |
   |              |              |✜───|              |        |
   |              | 6. Process payment           |        |
   |              |-------------➜|              |        |
   |              |              | 7. Charge card        |
   |              |              |------➜| [Ext. Stripe]
   |              |              | 8. Success   |        |
   |              |              |✜───|              |        |
   |              | 9. Confirmed  |              |        |
   |              |✜───|              |              |        |
   | 10. 201 Created             |              |        |
   |✜───|              |              |              |        |
   |              | 11. Publish OrderCreated     |        |
   |              |------➜| Message Bus           |        |
```

**Process:**
1. Customer submits order via POST /orders
2. Order Service validates cart contents and prices
3. Order Service requests inventory reservation
4. Inventory Service updates database stock levels
5. Inventory confirms reservation
6. Order Service initiates payment processing
7. Payment Service charges customer's card via Stripe
8. Stripe confirms successful charge
9. Payment Service confirms to Order Service
10. Order Service returns 201 Created with order details
11. Order Service publishes OrderCreated event for downstream processing

**Exception Paths:**
- **6a. Insufficient Inventory:** Return 409 Conflict; no reservation made
- **8a. Payment Failed:** Return 402 Payment Required; release inventory reservation
- **8b. Payment Timeout:** Return 202 Accepted; async processing continues

### 6.2 Place Order (Payment Failure)

[Same format with failure scenario]

### 6.3 Order Cancellation

[Same format]
```
