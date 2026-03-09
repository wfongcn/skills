# Architecture Documentation: [System Name]

> **Detail Level:** ESSENTIAL (Core Information)  
> **Approach:** Non-negotiable minimum for production systems

---

## 1. Introduction and Goals

### 1.1 Requirements Overview

**System Purpose:**
[Clear statement of purpose]

**Essential Features:**
- [Feature 1]
- [Feature 2]
- [Feature 3]
- [Feature 4]
- [Feature 5]

**Business Context:**
[Value proposition and beneficiaries]

### 1.2 Quality Goals (MANDATORY)

| Priority | Quality Goal | Concrete Scenario |
|:--------:|-------------|-------------------|
| **1** | #[Q42 property] | [Measurable target] |
| **2** | #[Q42 property] | [Measurable target] |
| **3** | #[Q42 property] | [Measurable target] |
| **4** | #[Q42 property] | [Measurable target] |
| **5** | #[Q42 property] | [Measurable target] |

### 1.3 Stakeholders

| Role | Contact | Expectations |
|------|---------|-------------|
| [Role] | [Name] | [What they need] |

---

## 2. Constraints

| Constraint | Impact |
|-----------|--------|
| [Technical/Org/Political constraint] | [How it affects architecture] |

---

## 3. Context and Scope

### 3.1 Business Context

```
[Business context diagram]
```

| Entity | Description | Input/Output |
|--------|-------------|--------------|
| [Entity] | [Description] | [Data flow] |

### 3.2 Technical Context

| Interface | Protocol | Data Format | Direction |
|-----------|----------|-------------|-----------|
| [Name] | [Protocol] | [Format] | [In/Out/Both] |

---

## 4. Solution Strategy

### 4.1 Overview
[2-3 paragraphs summarizing approach]

### 4.2 Key Decisions
| Decision | Rationale |
|----------|-----------|
| [Decision] | [Why] |

### 4.3 Achieving Quality Goals
| Quality Goal | Strategy |
|--------------|----------|
| [Goal] | [How addressed] |

---

## 5. Building Block View

### 5.1 Level-1 (MANDATORY)

```
[Top-level diagram]
```

| Component | Responsibility | Technology |
|-----------|---------------|------------|
| [Component] | [What it does] | [Tech stack] |

**Interfaces:**
| Interface | Between | Description |
|-----------|---------|-------------|
| [IF-1] | [A -> B] | [Data/contract] |

### 5.2 Level-2 (Selected Components)

#### [Component Name]

```
[Decomposition diagram]
```

| Sub-component | Responsibility |
|---------------|---------------|
| [Sub] | [What it does] |

---

## 6. Runtime View

### 6.1 [Primary Scenario]

```
[Sequence diagram]
```

**Process:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Exception Paths:**
- **[Error]:** [Handling]

---

## 9. Architecture Decisions

### ADR-001: [Decision Title]

**Status:** Accepted

**Context:**
[Problem being solved]

**Decision:**
[What was decided]

**Consequences:**
- Positive: [Benefits]
- Negative: [Trade-offs]

**Alternatives Considered:**
- [Alternative]: [Why rejected]

---

## 10. Quality Requirements

### 10.1 Quality Scenarios

| ID | Scenario | Metric | Priority |
|----|----------|--------|----------|
| Q-01 | [Description] | [Target] | [H/M/L] |

---

## 12. Glossary

### Domain Terms
| Term | Definition |
|------|------------|
| [Term] | [Definition] |

### Technical Terms
| Term | Definition |
|------|------------|
| [Term] | [Definition] |

### Abbreviations
| Abbreviation | Full Form |
|--------------|-----------|
| [Short] | [Long] |

---

*Documentation based on arc42 template - https://arc42.org*  
*Last updated: [Date]*
