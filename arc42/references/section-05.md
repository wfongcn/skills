# Section 5: 构建块视图 (Building Block View)

## 目的

展示系统的静态分解为构建块，使用 C4 Model。

## C4 语法

### Level 1: C4Context

系统上下文图，展示系统与外部的关系：

```mermaid
C4Context
    title Context Diagram for [System]

    Person(user, "用户", "使用系统的人")
    Person_Ext(ext_user, "外部用户", "外部系统用户")

    System_Boundary(system, "[系统名称]") {
        System(main, "主系统", "核心业务")
    }

    System_Ext(ext, "外部系统", "第三方服务")

    Rel(user, main, "使用")
    Rel(main, ext, "调用")
```

### Level 2: C4Container

容器图，展示技术构建块：

```mermaid
C4Container
    title Container Diagram for [System]

    Person(user, "用户", "使用系统")

    System_Boundary(system, "[系统]") {
        Container(app, "应用", "TypeScript", "用户界面")
        Container(api, "API", "Node.js", "业务逻辑")
        ContainerDb(db, "数据库", "PostgreSQL", "数据存储")
    }

    System_Ext(ext, "外部服务", "API")

    Rel(user, app, "使用")
    Rel(app, api, "HTTP")
    Rel(api, db, "JDBC")
    Rel(api, ext, "REST")
```

### Level 3: C4Component

组件图，展示容器内部结构：

```mermaid
C4Component
    title Component Diagram for [Container]

    ContainerDb(db, "数据库", "PostgreSQL", "存储")

    Container_Boundary(container, "[容器]") {
        Component(controller, "控制器", "处理请求")
        Component(service, "服务层", "业务逻辑")
        Component(repo, "仓库", "数据访问")
    }

    Rel(controller, service, "调用")
    Rel(service, repo, "使用")
    Rel(repo, db, "JDBC")
```

---

## 图表拆分原则

### 按场景拆分

每个图表应该聚焦一个场景：

**第 3 章**：按用户角色
- 场景 A: 开发者使用 CLI
- 场景 B: Web 用户
- 场景 C: 运维管理

**第 5 章**：按组件/子系统
- 5.1 系统全景 (Level 1)
- 5.2 场景 A 架构 (Level 2)
- 5.3 场景 B 架构 (Level 2)
- 5.4 组件 X (Level 3)
- 5.5 组件 Y (Level 3)

---

## Pi Mono 示例

### 5.1 系统全景 (Level 1)

```mermaid
C4Context
    title System Context for Pi Mono

    Person(dev, "开发者", "使用 CLI")
    Person(slack, "Slack 用户", "消息交互")
    Person(ops, "运维", "管理集群")

    System_Boundary(pi, "Pi Mono") {
        System(pi_system, "Pi Mono", "AI Agent")
    }

    System_Ext(openai, "OpenAI", "LLM")
    System_Ext(slack, "Slack", "消息")

    Rel(dev, pi_system, "使用")
    Rel(slack, slack, "消息")
    Rel(slack, pi_system, "Webhook")
    Rel(pi_system, openai, "API")
```

### 5.2 开发者场景 (Level 2)

```mermaid
C4Container
    title Container for Developer Scenario

    Person(dev, "开发者", "使用 CLI")

    System_Boundary(pi, "Pi Mono") {
        Container(cli, "pi-coding-agent", "CLI", "编程工具")
        Container(tui, "pi-tui", "UI", "终端渲染")
        Container(agent, "pi-agent-core", "Runtime", "运行时")
        Container(ai, "pi-ai", "API", "LLM 抽象")
    }

    System_Ext(openai, "OpenAI", "LLM")

    Rel(dev, cli, "使用")
    Rel(dev, tui, "使用")
    Rel(cli, agent, "调用")
    Rel(tui, agent, "调用")
    Rel(agent, ai, "调用")
    Rel(ai, openai, "API")
```

### 5.3 pi-ai 组件 (Level 3)

```mermaid
C4Component
    title Component for pi-ai

    System_Ext(openai, "OpenAI API", "GPT")
    System_Ext(anthropic, "Anthropic API", "Claude")

    Container_Boundary(ai, "pi-ai") {
        Component(client, "LLMClient", "统一入口")
        Component(registry, "ProviderRegistry", "注册表")
    }

    Component_Boundary(providers, "Providers") {
        Component(openai_p, "OpenAIProvider", "适配器")
        Component(anthropic_p, "AnthropicProvider", "适配器")
    }

    Rel(client, registry, "获取")
    Rel(registry, openai_p, "注册")
    Rel(registry, anthropic_p, "注册")
    Rel(openai_p, openai, "HTTP")
    Rel(anthropic_p, anthropic, "HTTP")
```

---

## 组件说明格式

每个图表后添加说明：

```markdown
**组件说明：**

| 组件 | 职责 | 设计要点 |
|------|------|----------|
| **组件名** | 职责描述 | 设计要点 |

**流程：**
1. 步骤1
2. 步骤2
```

---

## 检查清单

- [ ] 使用 C4 语法 (C4Context/C4Container/C4Component)
- [ ] 按场景拆分图表
- [ ] 包含 Level 1/2/3 三层
- [ ] 图表后有说明
