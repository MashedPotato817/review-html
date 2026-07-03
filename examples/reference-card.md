# 速记卡片示例

## 用途

速记卡片用于存放需要快速查阅的公式、数据、地址等信息，适合考前突击记忆。

## 通用结构

```html
<section class="card" id="quick-ref">
    <div class="card-header">
        <h2><span class="icon">⚡</span> 速记卡片</h2>
        <span class="arrow">▼</span>
    </div>
    <div class="card-content">
        <div class="card-body">
            <!-- 按类别组织 -->
            <h3>// 公式速记</h3>
            <!-- 公式卡片 -->

            <h3>// 数据速记</h3>
            <!-- 数据卡片 -->

            <h3>// 地址速记</h3>
            <!-- 地址卡片 -->
        </div>
    </div>
</section>
```

## 示例：单片机速记卡片

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
                <h4>周期计算</h4>
                <table>
                    <tr><th>周期</th><th>公式</th><th>12MHz</th></tr>
                    <tr><td>机器周期</td><td>12/fosc</td><td>1μs</td></tr>
                </table>
            </div>

            <div class="knowledge-card">
                <h4>定时器初值</h4>
                <p class="formula">TH0 = (65536 - T×fosc/12) / 256</p>
                <p class="formula">TL0 = (65536 - T×fosc/12) % 256</p>
            </div>

            <h3>// 地址速记</h3>

            <div class="knowledge-card">
                <h4>中断入口地址</h4>
                <table>
                    <tr><th>中断源</th><th>入口地址</th></tr>
                    <tr><td>INT0</td><td class="addr">0003H</td></tr>
                    <tr><td>T0</td><td class="addr">000BH</td></tr>
                </table>
            </div>

            <h3>// 寄存器速记</h3>

            <div class="knowledge-card">
                <h4><span class="sfr-tag sfr-bit">PSW</span> 程序状态字</h4>
                <table>
                    <tr><th>位</th><th>名称</th><th>功能</th></tr>
                    <tr><td>7</td><td>CY</td><td>进位标志</td></tr>
                    <tr><td>6</td><td>AC</td><td>辅助进位</td></tr>
                </table>
            </div>

        </div>
    </div>
</section>
```

## 示例：英语速记卡片

```html
<section class="card" id="quick-ref">
    <div class="card-header">
        <h2><span class="icon">⚡</span> 速记卡片</h2>
        <span class="arrow">▼</span>
    </div>
    <div class="card-content">
        <div class="card-body">

            <h3>// 高频词汇</h3>

            <div class="knowledge-card">
                <h4>核心动词</h4>
                <table>
                    <tr><th>单词</th><th>释义</th><th>例句</th></tr>
                    <tr><td>achieve</td><td>实现</td><td>achieve success</td></tr>
                </table>
            </div>

            <h3>// 写作模板</h3>

            <div class="knowledge-card">
                <h4>开头句式</h4>
                <ul>
                    <li>Nothing is more important than...</li>
                    <li>It is universally acknowledged that...</li>
                </ul>
            </div>

        </div>
    </div>
</section>
```

## CSS 样式

```css
/* 公式样式 */
.formula {
    font-family: var(--font-mono);
    color: var(--blue-600);
    font-weight: 700;
    padding: 0.25rem 0;
}

/* 地址样式 */
.addr {
    font-family: var(--font-mono);
    font-weight: 600;
    color: var(--blue-600);
}

/* 分类标题 */
h3 {
    font-size: 0.95rem;
    font-weight: 700;
    color: var(--blue-600);
    margin: 1.25rem 0 0.75rem;
    padding-bottom: 0.5rem;
    border-bottom: 2px solid var(--blue-100);
}

h3:first-child { margin-top: 0; }
```

## 设计原则

### 信息密度
- 速记卡片信息密度可以比普通模块高
- 但仍需保持可读性
- 使用表格对齐数据

### 快速查阅
- 使用等宽字体显示代码/地址
- 使用色彩标签分类
- 表格转置为纵向（适合手机）

### 分类清晰
- 使用 h3 标题分隔不同类别
- 每个类别使用独立的 knowledge-card
- 相关内容放在一起

## 常见问题

### 速记卡片太长
**问题**：内容太多，难以查找
**解决**：添加快速导航锚点

```html
<div class="quick-nav">
    <a href="#formula">公式</a>
    <a href="#address">地址</a>
    <a href="#register">寄存器</a>
</div>
```

### 公式显示不清晰
**问题**：公式与普通文字混在一起
**解决**：使用 formula 类高亮

```css
.formula {
    font-family: var(--font-mono);
    color: var(--blue-600);
    font-weight: 700;
    background: var(--blue-50);
    padding: 0.5rem;
    border-radius: var(--radius);
    margin: 0.25rem 0;
}
```

### 地址容易看错
**问题**：0 和 O 混淆
**解决**：使用等宽字体

```css
.addr {
    font-family: var(--font-mono);
    font-weight: 600;
}
```
