# 卡片结构模板

## 页面整体结构

### 方案 A：快速导航标签（推荐，适合模块 ≤ 15 个）

```html
<!-- 头部 -->
<header class="header">
    <div class="header-content">
        <h1>📖 科目名称</h1>
        <span class="exam-info">📅 考试时间</span>
    </div>
</header>

<!-- 快速导航标签（横向滚动） -->
<div class="quick-nav">
    <a href="#guide">指南</a>
    <a href="#module1">模块1</a>
    <a href="#module2">模块2</a>
    <!-- ... -->
</div>
```

```css
.quick-nav {
    display: flex;
    overflow-x: auto;
    gap: 0.5rem;
    padding: 0.75rem 1rem;
    background: var(--card-bg);
    border-bottom: 1px solid var(--border);
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none;
    position: sticky;
    top: 52px;
    z-index: 99;
}

.quick-nav::-webkit-scrollbar { display: none; }

.quick-nav a {
    flex-shrink: 0;
    padding: 0.4rem 0.85rem;
    background: var(--bg);
    color: var(--text-secondary);
    text-decoration: none;
    border: 1px solid var(--border);
    border-radius: 999px;
    font-size: 0.8rem;
    font-weight: 500;
    transition: all 0.2s;
}

.quick-nav a:hover,
.quick-nav a:active {
    background: var(--primary-light);
    color: var(--primary);
    border-color: var(--primary);
}
```

### 方案 B：全屏导航（适合模块 > 15 个）

```html
<!-- 汉堡菜单按钮 -->
<button class="menu-toggle" id="menuToggle">
    <span></span><span></span><span></span>
</button>

<!-- 全屏导航 -->
<nav class="fullscreen-nav" id="fullscreenNav">
    <a href="#guide" onclick="closeMenu()">📖 复习指南</a>
    <a href="#module1" onclick="closeMenu()">📖 模块1</a>
    <a href="#module2" onclick="closeMenu()">📖 模块2</a>
    <!-- ... -->
</nav>

<!-- 头部 -->
<header class="header">
    <div class="header-content">
        <h1>📖 科目名称</h1>
        <span class="exam-info">📅 考试时间</span>
    </div>
</header>
```

```css
/* 汉堡菜单按钮 */
.menu-toggle {
    display: none;
    position: fixed;
    top: 0.75rem;
    right: 0.75rem;
    width: 42px;
    height: 42px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    cursor: pointer;
    z-index: 200;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 5px;
}

.menu-toggle span {
    display: block;
    width: 18px;
    height: 2px;
    background: var(--primary);
    border-radius: 1px;
    transition: all 0.3s;
}

.menu-toggle.active span:nth-child(1) { transform: rotate(45deg) translateY(7px); }
.menu-toggle.active span:nth-child(2) { opacity: 0; }
.menu-toggle.active span:nth-child(3) { transform: rotate(-45deg) translateY(-7px); }

/* 全屏导航 */
.fullscreen-nav {
    display: none;
    position: fixed;
    inset: 0;
    background: var(--bg);
    z-index: 150;
    padding: 5rem 1.5rem 1.5rem;
    overflow-y: auto;
    animation: fadeIn 0.25s ease;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(-8px); }
    to { opacity: 1; transform: translateY(0); }
}

.fullscreen-nav.active { display: block; }

.fullscreen-nav a {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 1rem 1.25rem;
    color: var(--text);
    text-decoration: none;
    border-bottom: 1px solid var(--border);
    font-size: 1.1rem;
    transition: all 0.2s;
}

.fullscreen-nav a:hover,
.fullscreen-nav a:active {
    background: var(--primary-light);
    color: var(--primary);
}

/* 移动端显示汉堡菜单 */
@media (max-width: 768px) {
    .menu-toggle { display: flex; }
}
```

```javascript
// 汉堡菜单
const menuToggle = document.getElementById('menuToggle');
const fullscreenNav = document.getElementById('fullscreenNav');

menuToggle.addEventListener('click', () => {
    menuToggle.classList.toggle('active');
    fullscreenNav.classList.toggle('active');
    document.body.style.overflow = fullscreenNav.classList.contains('active') ? 'hidden' : '';
});

function closeMenu() {
    menuToggle.classList.remove('active');
    fullscreenNav.classList.remove('active');
    document.body.style.overflow = '';
}
```

### 方案 C：两者结合（推荐）

同时使用两种导航：
- **快速导航**：显示常用模块（5-8个）
- **全屏导航**：显示所有模块（通过汉堡菜单打开）

```html
<!-- 汉堡菜单（移动端显示） -->
<button class="menu-toggle" id="menuToggle">
    <span></span><span></span><span></span>
</button>

<!-- 全屏导航（所有模块） -->
<nav class="fullscreen-nav" id="fullscreenNav">
    <a href="#guide" onclick="closeMenu()">📖 复习指南</a>
    <a href="#module1" onclick="closeMenu()">📖 模块1</a>
    <!-- ... -->
</nav>

<!-- 头部 -->
<header class="header">
    <div class="header-content">
        <h1>📖 科目名称</h1>
        <span class="exam-info">📅 考试时间</span>
    </div>
</header>

<!-- 快速导航（常用模块） -->
<div class="quick-nav">
    <a href="#guide">指南</a>
    <a href="#module1">模块1</a>
    <a href="#module2">模块2</a>
    <!-- ... -->
</div>
```

## 模块卡片结构

### 基础卡片

```html
<section class="card" id="module1">
    <div class="card-header">
        <h2><span class="icon">📖</span> 模块标题</h2>
        <span class="arrow">▼</span>
    </div>
    <div class="card-content">
        <div class="card-body">
            <!-- 内容 -->
        </div>
    </div>
</section>
```

### 卡片 hover 效果（概率论风格）

```css
.card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    padding: 1.5rem;
    margin-bottom: 1rem;
    transition: transform 0.3s, box-shadow 0.3s;
}

.card:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(37, 99, 235, 0.15);
}
```

### 知识点卡片

```html
<div class="knowledge-card">
    <h4><span class="level-tag level-tag-master">掌握</span> 知识点标题</h4>
    <ul>
        <li>内容1</li>
        <li>内容2</li>
    </ul>
    <div class="tip-box">
        <strong>出题角度：</strong>考试方向提示
    </div>
</div>
```

### 公式框（概率论风格）

```html
<div class="formula-box">
    <div class="formula"><strong>公式名称</strong></div>
    <p>$$P(A \cup B) = P(A) + P(B) - P(AB)$$</p>
</div>
```

```css
.formula-box {
    background: #0d1b2a;
    border: 1px solid var(--accent);
    border-radius: 8px;
    padding: 1rem;
    margin: 1rem 0;
    overflow-x: auto;
}

.formula-box .formula {
    font-size: 1.1rem;
    color: var(--success);
    text-align: center;
    padding: 0.5rem;
}
```

### 提示框类型

```html
<!-- 警告框（排除内容） -->
<div class="warning-box">
    不考：xxx
</div>

<!-- 提示框（重点内容） -->
<div class="tip-box">
    重点例题：xxx
</div>

<!-- 信息框（一般提示） -->
<div class="info-box">
    书后习题：xxx
</div>
```

### Grid 布局

```html
<div class="grid-2">
    <div class="card">内容1</div>
    <div class="card">内容2</div>
</div>
```

```css
.grid-2 {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
}

.grid-3 {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
}

@media (max-width: 768px) {
    .grid-2, .grid-3 {
        grid-template-columns: 1fr;
    }
}
```

## 速记卡片结构

```html
<section class="card" id="quick-ref">
    <div class="card-header">
        <h2><span class="icon">⚡</span> 速记卡片</h2>
        <span class="arrow">▼</span>
    </div>
    <div class="card-content">
        <div class="card-body">
            <h3>// 公式速记</h3>
            <div class="knowledge-card">
                <h4>公式名称</h4>
                <p class="formula">公式内容</p>
            </div>

            <h3>// 数据速记</h3>
            <div class="knowledge-card">
                <h4>数据名称</h4>
                <table>
                    <tr><th>项目</th><th>数值</th></tr>
                    <tr><td>xxx</td><td class="addr">xxx</td></tr>
                </table>
            </div>
        </div>
    </div>
</section>
```

## 表格结构

### 标准表格（3列以内）

```html
<table>
    <tr><th>列1</th><th>列2</th><th>列3</th></tr>
    <tr><td>数据1</td><td>数据2</td><td>数据3</td></tr>
</table>
```

### 转置表格（原表格超过5列）

```html
<!-- 转置后：3列纵向 -->
<table>
    <tr><th>寄存器</th><th>地址</th><th>功能</th></tr>
    <tr><td>P0</td><td class="addr">80H</td><td>IO口</td></tr>
</table>
```

## 步骤组件

```html
<div class="steps">
    <div class="step">
        <strong>步骤1：</strong>内容
    </div>
    <div class="step">
        <strong>步骤2：</strong>内容
    </div>
</div>
```

```css
.steps {
    counter-reset: step;
}

.step {
    counter-increment: step;
    margin: 0.75rem 0;
    padding: 1rem 1.25rem 1rem 3rem;
    background: rgba(37, 99, 235, 0.05);
    border-radius: var(--radius);
    position: relative;
    border: 1px solid var(--border);
}

.step::before {
    content: counter(step);
    position: absolute;
    left: 0.75rem;
    top: 1rem;
    width: 1.75rem;
    height: 1.75rem;
    background: var(--primary);
    color: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 0.85rem;
}
```

## CSS 关键样式

```css
/* 卡片 */
.card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    margin-bottom: 1rem;
    overflow: hidden;
    box-shadow: var(--shadow-sm);
}

/* 卡片头部 */
.card-header {
    padding: 1rem 1.25rem;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

/* 知识点卡片 */
.knowledge-card {
    background: var(--bg);
    border: 1px solid var(--border);
    border-left: 4px solid var(--blue-400);
    border-radius: 0 var(--radius) var(--radius) 0;
    padding: 0.875rem 1rem;
    margin: 0.5rem 0;
}

/* 公式样式 */
.formula {
    font-family: var(--font-mono);
    color: var(--blue-600);
    font-weight: 700;
}

/* 地址样式 */
.addr {
    font-family: var(--font-mono);
    font-weight: 600;
    color: var(--blue-600);
}
```

## 常见问题

### 卡片展开动画不流畅
**问题**：max-height 动画卡顿
**解决**：使用足够大的 max-height 值

### 表格撑破容器
**问题**：表格太宽超出屏幕
**解决**：使用 table-layout: fixed

### 数学公式不渲染
**问题**：MathJax 未加载
**解决**：检查 CDN 链接，确保网络通畅
