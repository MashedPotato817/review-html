---
name: review-html
description: 创建考前速记HTML页面的完整工作流程。支持从PPT/DOC/PDF提取内容或从已有Markdown文档开始，整理成结构化内容，生成响应式HTML，优化移动端体验，最后推送到GitHub。适用于任何科目的考前速记整理。
license: Proprietary
---

# 考前速记 HTML 创建流程

## 概述

本技能描述从零开始创建考前速记HTML页面的完整工作流程，包括内容提取、整理、HTML生成、优化和部署。

**适用范围**：任何科目的考前速记整理，包括但不限于：
- 工科（单片机、电路、编程）
- 理科（数学、物理、概率论）
- 文科（英语、政治）
- 专业课（数据结构、操作系统）

## 工作流程

### 阶段 1：内容提取

**目标**：从PPT/DOC/PDF文件中提取文本内容，或从已有Markdown文档开始

**方案 A：从课件/教材提取**

| 格式 | 工具 | 说明 |
|------|------|------|
| .ppt/.pptx | `python-pptx` 或 `win32com` | 提取幻灯片文本 |
| .doc/.docx | `python-docx` 或 `win32com` | 提取文档文本 |
| .pdf（文字版） | `pdfplumber` 或 `PyPDF2` | 提取PDF文本 |
| .pdf（扫描版） | OCR 工具 | 图像识别文字 |

**方案 B：从已有文档开始（推荐）**

如果已有结构化的复习指南（如老师发放的复习要点），直接使用：

```
5_review/
├── demand.md          # 复习指南（老师发放）
├── menu.md            # 教材目录（可选）
└── index.html         # 最终输出
```

**判断标准**：
- 如果有现成的复习指南 → 直接进入阶段 2
- 如果只有课件/教材 → 先提取内容

### 阶段 2：内容整理

**目标**：将内容整理成结构化的知识模块

**模块结构**（通用模板）：

```
考前速记/
├── 📘 复习指南        # 考试范围、题型、分值
├── 模块1 ~ 模块N      # 按章节/主题组织
├── 📝 代码模板        # 编程类科目（可选）
└── ⚡ 速记卡片        # 关键数据速查
```

**内容标注系统**：

为每个知识点添加要求程度标签：

| 标签 | 含义 | 颜色 | 使用场景 |
|------|------|------|----------|
| 掌握/熟练掌握 | 最重要，必须背熟 | 🔴 红色 | 必考内容 |
| 理解/熟悉/会 | 重要，需理解原理 | 🔵 蓝色 | 重点内容 |
| 了解 | 次要，知道即可 | ⚪ 灰色 | 一般内容 |

**出题角度标注**：

为关键知识点添加考试方向提示：

```html
<div class="tip-box">
    <strong>出题角度：</strong>填空题考xxx，选择题考xxx
</div>
```

### 阶段 3：HTML 生成

**目标**：创建响应式HTML页面

**设计规范**：

#### 颜色主题（蓝白风格）

```css
:root {
    /* 主色调 */
    --primary: #2563eb;
    --primary-dark: #1d4ed8;
    --primary-light: #dbeafe;

    /* 功能色 */
    --success: #16a34a;
    --warning: #f59e0b;
    --danger: #dc2626;

    /* 中性色 */
    --bg: #f8fafc;
    --card-bg: #ffffff;
    --border: #e2e8f0;
    --text: #1e293b;
    --text-light: #64748b;
}
```

#### 标签色彩编码

```css
/* 要求程度标签 */
.level-tag-master { background: #fef2f2; color: #dc2626; }  /* 掌握 */
.level-tag-understand { background: #eff6ff; color: #2563eb; }  /* 理解 */
.level-tag-know { background: #f8fafc; color: #64748b; }  /* 了解 */

/* 内容分类标签（按科目自定义） */
.sfr-io { background: #dbeafe; color: #1d4ed8; }  /* 示例：IO口 */
.sfr-bit { background: #fef3c7; color: #92400e; }  /* 示例：可位寻址 */
.sfr-int { background: #fee2e2; color: #991b1b; }  /* 示例：中断 */
```

#### 卡片结构

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

#### 知识点卡片

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

### 阶段 4：移动端优化

**关键规则**：

#### 表格优化

| 规则 | 说明 |
|------|------|
| 宽表格转置 | 超过 5 列的表格转置为纵向 |
| 固定表头 | `position: sticky; top: 0` |
| 响应式布局 | `table-layout: fixed; word-break: break-all` |

**转置示例**：

```html
<!-- 优化前（8列横向） -->
<table>
    <tr><td>P0</td><td>P1</td><td>P2</td><td>P3</td><td>SP</td><td>PSW</td><td>ACC</td><td>B</td></tr>
    <tr><td>80H</td><td>90H</td><td>A0H</td><td>B0H</td><td>81H</td><td>D0H</td><td>E0H</td><td>F0H</td></tr>
</table>

<!-- 优化后（3列纵向） -->
<table>
    <tr><th>寄存器</th><th>地址</th><th>功能</th></tr>
    <tr><td>P0</td><td class="addr">80H</td><td>IO口</td></tr>
    <!-- ... -->
</table>
```

#### 响应式断点

```css
@media (max-width: 768px) {
    html { font-size: 15px; }
    .card { padding: 1.25rem; }
}

@media (max-width: 480px) {
    html { font-size: 14px; }
    .card { padding: 1rem; }
}
```

### 阶段 5：交互功能

**必需功能**：

1. **手风琴折叠**（模块展开/收起）

```javascript
document.querySelectorAll('.card-header').forEach(header => {
    header.addEventListener('click', () => {
        header.parentElement.classList.toggle('active');
    });
});
```

2. **折叠所有按钮**

```javascript
const collapseBtn = document.getElementById('collapseAll');
let allCollapsed = false;

collapseBtn.addEventListener('click', () => {
    const cards = document.querySelectorAll('.card');
    allCollapsed = !allCollapsed;
    cards.forEach(card => {
        card.classList.toggle('active', !allCollapsed);
    });
});
```

3. **返回顶部按钮**

```javascript
window.addEventListener('scroll', () => {
    backToTop.style.display = window.scrollY > 300 ? 'flex' : 'none';
});
```

4. **导航方式选择**

根据模块数量选择合适的导航方式：

| 模块数量 | 推荐方案 | 说明 |
|----------|----------|------|
| ≤ 15 个 | 方案 A：快速导航标签 | 横向滚动，简单直接 |
| > 15 个 | 方案 B：全屏导航 | 汉堡菜单，全屏显示 |
| 任意 | 方案 C：两者结合 | 快速导航 + 全屏导航 |

**方案 A：快速导航标签**

```html
<div class="quick-nav">
    <a href="#module1">模块1</a>
    <a href="#module2">模块2</a>
    <!-- ... -->
</div>
```

**方案 B：全屏导航**

```html
<button class="menu-toggle" id="menuToggle">
    <span></span><span></span><span></span>
</button>

<nav class="fullscreen-nav" id="fullscreenNav">
    <a href="#module1" onclick="closeMenu()">📖 模块1</a>
    <!-- ... -->
</nav>
```

**方案 C：两者结合**

同时使用快速导航和全屏导航，详见 `templates/card-structure.md`。

### 阶段 6：部署

**推送到GitHub**：

```bash
git add index.html
git commit -m "feat: 添加考前速记页面"
git push origin main
```

**.gitignore**（排除大文件）：

```
*.pdf
*.ppt
*.doc
.claude/
```

### 尾注要求

**必须在 footer 中添加以下尾注**：

```html
<footer class="footer">
    <!-- 其他内容 -->
    <p class="footer-note">Composed by MashedPotato</p>
    <p class="footer-note">最后更新：<span id="lastModified"></span></p>
</footer>
```

**JavaScript 自动填充时间**：

```javascript
document.getElementById('lastModified').textContent = new Date(document.lastModified).toLocaleString('zh-CN', {
    year: 'numeric', month: '2-digit', day: '2-digit',
    hour: '2-digit', minute: '2-digit'
});
```

**说明**：
- 尾注标识项目来源
- 最后更新时间自动从文件修改时间获取
- 格式统一，便于版本追踪

## 模块清单

根据科目类型，选择合适的模块：

| 模块类型 | 适用科目 | 示例 |
|----------|----------|------|
| 📘 复习指南 | 所有科目 | 考试范围、题型、分值 |
| 知识点模块 | 所有科目 | 按章节/主题组织 |
| 📝 代码模板 | 编程类 | 初始化模板、常用算法 |
| ⚡ 速记卡片 | 公式/数据类 | 寄存器、公式、地址 |
| 📚 词汇卡片 | 语言类 | 单词、短语、句型 |
| ✍️ 写作模板 | 语言类 | 评分标准、句式、话题 |

## 速记卡片模板

适用于需要快速查阅公式/数据的科目：

```html
<section class="card" id="quick-ref">
    <div class="card-header">
        <h2><span class="icon">⚡</span> 速记卡片</h2>
        <span class="arrow">▼</span>
    </div>
    <div class="card-content">
        <div class="card-body">
            <!-- 公式速记 -->
            <div class="knowledge-card">
                <h4>公式名称</h4>
                <p class="formula">公式内容</p>
            </div>

            <!-- 数据速记 -->
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

## 设计原则

### 可读性优先
- 字体大小：正文 16px，移动端 14-15px
- 行高：1.7-1.8
- 内边距：卡片 1.5rem，移动端 1-1.25rem

### 快速扫描
- 使用图标区分不同类型内容
- 警告框（红色边框）突出排除内容
- 提示框（绿色边框）显示重点例题
- 信息框（蓝色边框）显示一般提示

### 响应式设计
- 768px 断点：平板设备
- 480px 断点：手机设备
- 表格横向滚动或转置

### 数学公式支持（可选）

对于数学/物理/概率论等科目，添加 MathJax 或 KaTeX 支持：

```html
<!-- MathJax -->
<script>
    window.MathJax = {
        tex: {
            inlineMath: [['$', '$'], ['\\(', '\\)']],
            displayMath: [['$$', '$$'], ['\\[', '\\]']]
        }
    };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js" async></script>
```

使用示例：
```html
<div class="formula-box">
    <div class="formula"><strong>贝叶斯公式</strong></div>
    <p>$$P(B_i|A) = \frac{P(B_i)P(A|B_i)}{\sum_j P(B_j)P(A|B_j)}$$</p>
</div>
```

### 卡片 hover 效果

```css
.card {
    transition: transform 0.3s, box-shadow 0.3s;
}

.card:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(37, 99, 235, 0.15);
}
```

### 自定义滚动条

```css
::-webkit-scrollbar {
    width: 8px;
    height: 8px;
}

::-webkit-scrollbar-track {
    background: var(--bg);
}

::-webkit-scrollbar-thumb {
    background: var(--primary);
    border-radius: 4px;
}
```

### Grid 多列布局

```css
.grid-2 {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
}

@media (max-width: 768px) {
    .grid-2 {
        grid-template-columns: 1fr;
    }
}
```

## 常见问题

### 表格溢出
**问题**：表格超出屏幕宽度
**解决**：
```css
.table-wrapper { overflow-x: auto; width: 100%; }
table { table-layout: fixed; }
th, td { word-break: break-all; }
```

### 背景色块未对齐
**问题**：背景色超出容器
**解决**：
```css
body { overflow-x: hidden; }
.card { overflow: hidden; }
```

### 文字排版过密
**问题**：阅读体验差
**解决**：
```css
line-height: 1.7;
padding: 1.5rem;
```

### 宽表格难以阅读
**问题**：手机端需要横向滚动
**解决**：转置为纵向排列（3列：项目/数值/说明）

## 模板文件

本 skill 包含以下模板文件，可直接复制使用：

| 文件 | 用途 |
|------|------|
| `templates/css-variables.md` | 颜色主题变量（蓝白/深色） |
| `templates/card-structure.md` | 卡片结构模板（页面/模块/知识点） |
| `templates/color-tags.md` | 色彩标签系统（要求程度/内容分类） |
| `examples/reference-card.md` | 速记卡片示例（单片机/英语） |

## 痛点解决方案

### 内容提取失败
**问题**：PDF扫描版无法提取文本
**解决**：使用方案B，从已有文档（demand.md）开始

### 章节编号错误
**问题**：模块标题与内容不匹配
**解决**：对照教材目录（menu.md）逐一核对

### 表格横向溢出
**问题**：手机端表格需要横向滚动
**解决**：超过5列的表格转置为纵向

### 标签遗漏
**问题**：部分知识点没有标注要求程度
**解决**：逐章检查，确保每个知识点都有标签

### 锚点跳转偏移
**问题**：点击导航链接后内容被头部遮挡
**解决**：添加 `scroll-padding-top: 100px`

### CSS 兼容性问题
**问题**：某些CSS属性不被支持
**解决**：避免使用 `-webkit-overflow-scrolling`，使用标准属性

### 内联样式警告
**问题**：VS Code 报告内联样式警告
**解决**：将内联样式提取为CSS类

## 参考项目

### 概率论考前速记
- **主题**：深色主题（#1a1a2e 背景 + #00d4ff 霓虹色）
- **公式**：MathJax/LaTeX 渲染
- **卡片**：hover 浮动效果
- **布局**：grid 多列布局
- **滚动条**：自定义品牌色
- **GitHub**：https://github.com/MashedPotato817/gailvlun-notes

### 英语考前速记
- **主题**：蓝白主题
- **导航**：快速导航标签
- **内容**：词汇卡片、句子卡片
- **GitHub**：https://github.com/MashedPotato817/English-Notes

### 单片机考前速记
- **主题**：蓝白主题
- **特色**：色彩编码、速记卡片、代码模板
- **标签**：掌握/理解/了解系统
- **GitHub**：https://github.com/MashedPotato817/AT89S52-Notes
