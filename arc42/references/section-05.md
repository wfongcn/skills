# Section 5: Building Block View

## Purpose

Show the static decomposition of the system into building blocks (modules, components, classes, packages). This is the most important structural view of the architecture.

## Levels of Abstraction

### Level 1: System Overview (MANDATORY)
- The entire system as one black box
- Shows major subsystems/components
- Maximum 7±2 elements

### Level 2: Major Components
- Decomposition of Level 1 elements
- Shows internal structure
- Only decompose what's architecturally significant

### Level 3: Detailed Internals
- Rarely needed
- Only for complex components
- Usually better in code documentation

## Format

### Level 1 Template

```markdown
### 5.1 Building Block Level-1

```
+------------------+         +------------------+
|   [Component A]  |---------|   [Component B]  |
+------------------+         +------------------+
         |                            |
         |                            |
         v                            v
+------------------+         +------------------+
|   [Component C]  |---------|   [Component D]  |
+------------------+         +------------------+
```

**Responsibilities:**
| Component | Responsibility |
|-----------|---------------|
| Component A | [Single sentence description] |

**Interfaces:**
| Interface | Component | Description |
|-----------|-----------|-------------|
| IF-1 | Component A -> Component B | [What is exchanged] |
```

### Level 2 Template (for selected components)

```markdown
### 5.2 Building Block Level-2: [Component Name]

[Decomposition of one Level-1 component]
```

## Notation Options

1. **C4 Model (Recommended)**
   - Level 1 = System Context (系统上下文)
   - Level 2 = Container diagram (容器图)
   - Level 3 = Component diagram (组件图)

2. **UML Component Diagram**
   - Standard notation
   - Good tool support

3. **Simple Boxes and Lines**
   - ASCII art or drawing
   - Focus on clarity over notation

## C4 Model with Mermaid

### C4 Level-1: System Context Diagram (系统上下文图)

展示系统与外部实体之间的关系。

```mermaid
flowchart LR
    subgraph 外部实体
        User[小学生]
        Parent[家长]
        Teacher[教师]
    end

    subgraph 知识冒险岛系统
        App[Web应用]
    end

    subgraph 外部服务
        AI[Claude API]
        DeepSeek[DeepSeek API]
    end

    User -->|使用| App
    Parent -->|监督| App
    Teacher -->|管理| App
    App -->|调用| AI
    App -->|调用| DeepSeek
```

**Level-1 说明:**
- 显示系统边界
- 展示外部参与者（人）
- 展示外部系统
- 关系用动词描述

---

### C4 Level-2: Container Diagram (容器图)

展示系统内部的主要构建块（容器）。

```mermaid
flowchart TB
    subgraph 前端容器
        Browser[浏览器]
        SPA[React SPA]
        Router[路由]
        State[状态管理]
    end

    subgraph 后端容器
        MCP[MCP服务器]
        Tools[工具集]
    end

    subgraph 外部服务
        AI[Claude API]
    end

    Browser --> SPA
    SPA --> Router
    Router --> State
    State --> MCP
    MCP --> Tools
    Tools --> AI
```

**Level-2 说明:**
- 分解系统内部的主要进程/服务
- 每个容器独立运行
- 展示容器间通信
- 标注协议 (HTTP, JSON-RPC, etc.)

---

### C4 Level-3: Component Diagram (组件图)

展示一个容器的内部组件。

```mermaid
flowchart TB
    subgraph 前端组件
        App[App.tsx]
        Components[组件库]
        Pages[页面]
        Hooks[自定义Hooks]
        API[API客户端]
    end

    App --> Components
    App --> Pages
    App --> Hooks
    Hooks --> API
    API --> Components
```

**Level-3 说明:**
- 展示单个容器的内部结构
- 分解到类/模块级别
- 仅用于复杂容器
- 通常代码文档更合适

---

### 完整 C4 层级示例

#### Level-1: 系统上下文
```mermaid
flowchart TB
    subgraph 外部
        Student[学生] --> System
        Parent[家长] --> System
    end

    System[(知识冒险岛)] --> AI[AI服务]
```

#### Level-2: 容器
```mermaid
flowchart TB
    subgraph System
        Web[Web前端]
        API[API网关]
        Service[业务服务]
        DB[数据库]
    end

    Web --> API
    API --> Service
    Service --> DB
```

#### Level-3: 组件 (以Web前端为例)
```mermaid
flowchart TB
    subgraph Web前端
        App[App入口]
        Router[路由]
        Store[状态]
        UI[UI组件]
    end

    App --> Router
    App --> Store
    App --> UI
    Store --> UI
```

---

### 实际应用示例

#### Level-1 示例
```mermaid
flowchart TB
    subgraph 用户层
        User1[小学生]
        User2[家长]
        User3[教师]
    end

    subgraph 知识冒险岛
        WebApp[Web应用]
    end

    subgraph 外部
        AI[Claude]
    end

    User1 -->|学习| WebApp
    User2 -->|监督| WebApp
    User3 -->|管理| WebApp
    WebApp -->|生成题目| AI
```

#### Level-2 示例
```mermaid
flowchart TB
    subgraph 前端
        Browser[浏览器]
        React[React SPA]
        Client[MCP客户端]
    end

    subgraph 后端
        Server[MCP服务器]
        Parser[内容解析]
        Gen[题目生成]
        Eval[答案评估]
    end

    subgraph AI
        Claude[Claude API]
    end

    Browser --> React
    React --> Client
    Client --> Server
    Server --> Parser
    Server --> Gen
    Server --> Eval
    Gen --> Claude
    Eval --> Claude
```

#### Level-3 示例 (前端组件)
```mermaid
flowchart TB
    subgraph components
        Character[角色选择]
        Game[游戏界面]
        Question[题目卡片]
        Result[结果展示]
    end

    subgraph hooks
        Speech[语音Hook]
        Game[游戏Hook]
    end

    subgraph api
        Client[API客户端]
    end

    Game --> Character
    Game --> Question
    Game --> Result
    Question --> Speech
    Game --> Game
    Speech --> Client
    Game --> Client
```

## Input Questions

- What are the major subsystems/components?
- What is the responsibility of each component?
- How do components interact?
- Which components are architecturally significant?
- What interfaces exist between components?
- Are there shared/common components?

## Quality Checklist

- [ ] Level 1 is provided (mandatory)
- [ ] Each component has clear, single responsibility
- [ ] Components are at similar abstraction level
- [ ] Interfaces are documented
- [ ] Diagram is not too crowded (max 7±2 elements)
- [ ] Only architecturally significant details are shown
- [ ] Naming is consistent with domain language

## Common Mistakes

❌ **Too many components at Level 1** (more than 7-9)  
❌ **Mixed abstraction levels** (components and classes together)  
❌ **Missing responsibilities** (just boxes)  
❌ **No interfaces documented**  
❌ **Showing everything** (not just architecturally significant)  
❌ **Inconsistent naming**  
❌ **Level 3 when not needed**

## Example

```markdown
### 5.1 Building Block Level-1

```
+---------------------+     +---------------------+
|   Order Service     |-----|  Payment Service    |
|   (Spring Boot)     |     |  (Spring Boot)      |
+---------------------+     +---------------------+
           |                           |
           | Events                    | API Calls
           v                           v
+---------------------+     +---------------------+
|  Inventory Service  |     |  Notification Svc   |
|  (Spring Boot)      |     |  (Node.js)          |
+---------------------+     +---------------------+
           |                           
           | Query                     
           v                           
+---------------------+               
|  PostgreSQL         |               
|  (Primary DB)       |               
+---------------------+               
```

**Responsibilities:**
| Component | Responsibility |
|-----------|---------------|
| Order Service | Manages order lifecycle; validates orders; orchestrates checkout process |
| Payment Service | Processes payments; handles refunds; integrates with payment providers |
| Inventory Service | Tracks stock levels; reserves inventory; updates quantities |
| Notification Service | Sends emails, SMS, push notifications; manages templates |

**Interfaces:**
| Interface | Between | Description |
|-----------|---------|-------------|
| Order Events | Order -> Inventory | OrderCreated, OrderCancelled events |
| Payment API | Order -> Payment | REST API for payment processing |
| Inventory Query | Order -> Inventory | gRPC for real-time stock checks |

### 5.2 Building Block Level-2: Order Service

```
+------------------+     +------------------+     +------------------+
|   Order API      |-----|  Order Service   |-----|  Order Repository |
|   (Controller)   |     |  (Domain)        |     |  (Infrastructure) |
+------------------+     +------------------+     +------------------+
                                |
                                v
                         +------------------+
                         |  Event Publisher |
                         |  (Infrastructure)|
                         +------------------+
```

**Responsibilities:**
| Component | Responsibility |
|-----------|---------------|
| Order API | HTTP endpoints; request validation; DTO mapping |
| Order Service | Business logic; order state machine; validation rules |
| Order Repository | Database access; CRUD operations; query optimization |
| Event Publisher | Publishes domain events to message bus |
```
