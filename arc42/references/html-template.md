# Arc42 HTML 输出模板

> 用于生成高质量的 arc42 架构文档 HTML 页面

## 设计理念

采用 **建筑杂志风格 (Architectural Editorial)** 美学：
- 优雅、现代、富有质感
- 避免通用的"AI风格"
- 适合技术文档的专业感

## 字体

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;0,700;1,400&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,400&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

- **标题**: Cormorant Garamond (衬线)
- **正文**: DM Sans (无衬线)
- **代码**: JetBrains Mono

## CSS 变量

```css
:root {
    /* 主色调 */
    --bg-primary: #1a1a1a;
    --bg-secondary: #242424;
    --bg-elevated: #2d2d2d;
    --bg-content: #faf9f7;
    --bg-content-alt: #f5f4f1;

    /* 强调色 - 铜金色 */
    --accent: #c9a86c;
    --accent-light: #e4d4a8;
    --accent-dark: #8b7355;

    /* 文字 */
    --text-primary: #1a1a1a;
    --text-secondary: #5a5a5a;
    --text-muted: #8a8a8a;
    --text-inverse: #faf9f7;
    --text-inverse-muted: #a0a0a0;

    /* 边框 */
    --border: #e5e4e1;
    --border-light: #f0efed;
    --border-dark: #3d3d3d;

    /* 状态色 */
    --success: #6b8e6b;
    --warning: #c4a35a;
    --danger: #a65d5d;

    /* 间距 */
    --space-xs: 4px;
    --space-sm: 8px;
    --space-md: 16px;
    --space-lg: 24px;
    --space-xl: 32px;
    --space-2xl: 48px;
    --space-3xl: 64px;

    /* 字体 */
    --font-display: 'Cormorant Garamond', Georgia, serif;
    --font-body: 'DM Sans', -apple-system, sans-serif;
    --font-mono: 'JetBrains Mono', monospace;
}
```

## 页面结构

```html
<body>
    <!-- 侧边栏 -->
    <nav class="sidebar">
        <div class="sidebar-header">
            <div class="sidebar-logo">项目名称</div>
            <div class="sidebar-subtitle">Arc42 架构文档</div>
        </div>
        <nav class="sidebar-nav">
            <a href="#chapter1" class="nav-chapter">
                <span class="nav-chapter-number">01</span> 介绍和目标
            </a>
            <!-- 更多章节... -->
        </nav>
    </nav>

    <!-- 主内容区 -->
    <main class="main">
        <div class="content">
            <section id="chapter1">
                <span class="section-number">Chapter 01</span>
                <h1>介绍和目标</h1>
                <!-- 内容... -->
            </section>
            <!-- 更多章节... -->
        </div>
    </main>
</body>
```

## 侧边栏样式

```css
.sidebar {
    position: fixed;
    left: 0;
    top: 0;
    width: 320px;
    height: 100vh;
    background: var(--bg-primary);
    border-right: 1px solid var(--border-dark);
    z-index: 100;
    display: flex;
    flex-direction: column;
}

.sidebar-logo {
    font-family: var(--font-display);
    font-size: 24px;
    font-weight: 600;
    color: var(--text-inverse);
}

.sidebar-subtitle {
    font-size: 12px;
    color: var(--text-inverse-muted);
    text-transform: uppercase;
    letter-spacing: 0.15em;
}

.nav-chapter {
    display: block;
    padding: var(--space-sm) var(--space-xl);
    color: var(--text-inverse-muted);
    text-decoration: none;
    font-size: 13px;
    transition: all 0.2s ease;
    border-left: 2px solid transparent;
}

.nav-chapter:hover {
    color: var(--text-inverse);
    background: rgba(255,255,255,0.03);
}

.nav-chapter.active {
    color: var(--accent);
    border-left-color: var(--accent);
    background: rgba(201, 168, 108, 0.08);
}

.nav-chapter-number {
    display: inline-block;
    width: 24px;
    font-family: var(--font-display);
    font-weight: 500;
    opacity: 0.6;
}
```

## 内容区样式

```css
.main {
    margin-left: 320px;
    min-height: 100vh;
}

.content {
    max-width: 900px;
    margin: 0 auto;
    padding: var(--space-3xl) var(--space-2xl);
}

h1 {
    font-family: var(--font-display);
    font-size: 48px;
    font-weight: 500;
    letter-spacing: -0.02em;
    line-height: 1.2;
    margin-bottom: var(--space-xl);
}

h2 {
    font-family: var(--font-display);
    font-size: 32px;
    font-weight: 500;
    margin: var(--space-3xl) 0 var(--space-lg);
    padding-bottom: var(--space-md);
    border-bottom: 1px solid var(--border);
}

h3 {
    font-family: var(--font-display);
    font-size: 22px;
    font-weight: 500;
    margin: var(--space-xl) 0 var(--space-md);
}

h4 {
    font-family: var(--font-body);
    font-size: 14px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--text-muted);
    margin: var(--space-lg) 0 var(--space-sm);
}

.section-number {
    font-family: var(--font-display);
    font-size: 12px;
    color: var(--accent);
    text-transform: uppercase;
    letter-spacing: 0.2em;
    margin-bottom: var(--space-sm);
    display: block;
}
```

## 卡片样式

```css
.card {
    background: white;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: var(--space-lg);
    margin: var(--space-lg) 0;
    transition: all 0.3s ease;
}

.card:hover {
    border-color: var(--accent-light);
    box-shadow: 0 4px 20px rgba(0,0,0,0.05);
}

.card-header {
    font-family: var(--font-display);
    font-size: 18px;
    font-weight: 500;
    margin-bottom: var(--space-md);
    display: flex;
    align-items: center;
    gap: var(--space-sm);
}
```

## 质量目标卡片

```css
.quality-goal {
    display: flex;
    align-items: flex-start;
    gap: var(--space-lg);
    padding: var(--space-lg);
    background: white;
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent);
    margin: var(--space-md) 0;
    transition: all 0.3s ease;
}

.quality-goal:hover {
    border-color: var(--accent-light);
    transform: translateX(4px);
}

.quality-goal-icon {
    font-family: var(--font-mono);
    font-size: 14px;
    font-weight: 500;
    color: var(--accent);
    background: var(--bg-content-alt);
    padding: var(--space-xs) var(--space-sm);
    border-radius: 4px;
}
```

## ADR 卡片

```css
.adr {
    background: white;
    border: 1px solid var(--border);
    margin: var(--space-lg) 0;
    overflow: hidden;
}

.adr-header {
    background: var(--bg-content-alt);
    padding: var(--space-md) var(--space-lg);
    border-bottom: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.adr-title {
    font-family: var(--font-display);
    font-size: 18px;
    font-weight: 500;
}

.adr-status {
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    padding: var(--space-xs) var(--space-sm);
    border-radius: 4px;
}

.adr-status.accepted {
    background: rgba(107, 142, 107, 0.15);
    color: var(--success);
}

.adr-body {
    padding: var(--space-lg);
}

.adr-section {
    margin-bottom: var(--space-md);
}

.adr-section-title {
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--text-muted);
}
```

## 表格样式

```css
table {
    width: 100%;
    border-collapse: collapse;
    margin: var(--space-lg) 0;
    font-size: 14px;
}

th {
    font-family: var(--font-body);
    font-weight: 600;
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--text-muted);
    text-align: left;
    padding: var(--space-sm) var(--space-md);
    border-bottom: 2px solid var(--text-primary);
}

td {
    padding: var(--space-md);
    border-bottom: 1px solid var(--border-light);
    color: var(--text-secondary);
}

tr:hover td {
    background: var(--bg-content-alt);
}
```

## 代码样式

```css
code {
    font-family: var(--font-mono);
    font-size: 13px;
    background: var(--bg-content-alt);
    padding: 2px 6px;
    border-radius: 3px;
    color: var(--accent-dark);
}

pre {
    background: var(--bg-primary);
    color: var(--text-inverse);
    padding: var(--space-lg);
    border-radius: 8px;
    overflow-x: auto;
    margin: var(--space-lg) 0;
    font-family: var(--font-mono);
    font-size: 13px;
    line-height: 1.6;
}
```

## 图表容器

```css
.diagram {
    background: white;
    border: 1px solid var(--border);
    margin: var(--space-xl) 0;
    padding: var(--space-xl);
    text-align: center;
}

.diagram-caption {
    font-size: 13px;
    color: var(--text-muted);
    margin-top: var(--space-md);
    font-style: italic;
}
```

## 响应式

```css
@media (max-width: 1024px) {
    .sidebar {
        transform: translateX(-100%);
        transition: transform 0.3s ease;
    }

    .sidebar.open {
        transform: translateX(0);
    }

    .main {
        margin-left: 0;
    }
}
```

## JavaScript

```javascript
// 初始化 Mermaid
mermaid.initialize({
    startOnLoad: true,
    theme: 'default',
    flowchart: { useMaxWidth: true, htmlLabels: true, curve: 'basis' },
    sequence: { useMaxWidth: true, diagramMarginX: 50, actorMargin: 50 },
    classDiagram: { useMaxWidth: true }
});

// 导航点击
document.querySelectorAll('.nav-chapter').forEach(link => {
    link.addEventListener('click', (e) => {
        e.preventDefault();
        const targetId = link.getAttribute('href').substring(1);
        const target = document.getElementById(targetId);
        if (target) {
            target.scrollIntoView({ behavior: 'smooth' });
        }
    });
});

// 滚动高亮当前章节
const sections = document.querySelectorAll('section');
window.addEventListener('scroll', () => {
    let current = '';
    sections.forEach(section => {
        const sectionTop = section.offsetTop;
        if (scrollY >= sectionTop - 150) {
            current = section.getAttribute('id');
        }
    });

    document.querySelectorAll('.nav-chapter').forEach(link => {
        link.classList.remove('active');
        if (link.getAttribute('href') === '#' + current) {
            link.classList.add('active');
        }
    });
});
```

## Mermaid CDN

```html
<script src="https://cdn.jsdelivr.net/npm/mermaid@11.12.3/dist/mermaid.min.js"></script>
```
