# 色彩标签系统

## 要求程度标签

用于标注知识点的重要程度。

### CSS 样式

```css
.level-tag {
    display: inline-block;
    font-size: 0.7rem;
    padding: 0.1rem 0.4rem;
    border-radius: 3px;
    margin-right: 0.3rem;
    font-weight: 600;
}

.level-tag-master {
    background: #fef2f2;
    color: #dc2626;
    border: 1px solid #fecaca;
}

.level-tag-understand {
    background: #eff6ff;
    color: #2563eb;
    border: 1px solid #bfdbfe;
}

.level-tag-know {
    background: #f8fafc;
    color: #64748b;
    border: 1px solid #e2e8f0;
}
```

### 使用示例

```html
<li><span class="level-tag level-tag-master">掌握</span> 51单片机的片内硬件组成</li>
<li><span class="level-tag level-tag-understand">理解</span> 存储器结构</li>
<li><span class="level-tag level-tag-know">了解</span> 发展历史</li>
```

### 标签含义

| 标签 | 颜色 | 含义 | 复习策略 |
|------|------|------|----------|
| 掌握/熟练掌握 | 🔴 红色 | 最重要，必须背熟 | 反复记忆，会写会画 |
| 理解/熟悉/会 | 🔵 蓝色 | 重要，需理解原理 | 理解原理，能解释 |
| 了解 | ⚪ 灰色 | 次要，知道即可 | 看一遍，有印象 |

## 内容分类标签

用于按类型/功能分类内容。

### 通用标签（适用于任何科目）

```css
.tag {
    display: inline-block;
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 700;
    padding: 0.1rem 0.4rem;
    border-radius: 3px;
    margin-right: 0.25rem;
}

/* 按类型分类 */
.tag-theory { background: #dbeafe; color: #1d4ed8; }  /* 理论 */
.tag-formula { background: #fef3c7; color: #92400e; }  /* 公式 */
.tag-example { background: #d1fae5; color: #065f46; }  /* 例题 */
.tag-key { background: #fee2e2; color: #991b1b; }  /* 重点 */
```

### 单片机专用标签

```css
/* 按功能分类 */
.sfr-io { background: #dbeafe; color: #1d4ed8; }  /* IO口 */
.sfr-bit { background: #fef3c7; color: #92400e; }  /* 可位寻址 */
.sfr-int { background: #fee2e2; color: #991b1b; }  /* 中断 */
.sfr-timer { background: #e0e7ff; color: #3730a3; }  /* 定时器 */
.sfr-uart { background: #d1fae5; color: #065f46; }  /* 串口 */
```

### 英语专用标签

```css
/* 按词性分类 */
.tag-noun { background: #dbeafe; color: #1d4ed8; }  /* 名词 */
.tag-verb { background: #d1fae5; color: #065f46; }  /* 动词 */
.tag-adj { background: #fef3c7; color: #92400e; }  /* 形容词 */
.tag-adv { background: #e0e7ff; color: #3730a3; }  /* 副词 */
```

### 使用示例

```html
<!-- 单片机 -->
<td><span class="sfr-tag sfr-io">P0</span></td>
<td><span class="sfr-tag sfr-bit">TCON</span></td>
<td><span class="sfr-tag sfr-int">INT0</span></td>

<!-- 英语 -->
<span class="tag tag-noun">n.</span>
<span class="tag tag-verb">v.</span>
<span class="tag tag-adj">adj.</span>
```

## 图例说明

在速记卡片末尾添加图例：

```html
<p class="tag-legend">
    <span class="sfr-tag sfr-io">IO口</span>
    <span class="sfr-tag sfr-bit">可位寻址</span>
    <span class="sfr-tag sfr-int">中断</span>
    <span class="sfr-tag sfr-timer">定时器</span>
    <span class="sfr-tag sfr-uart">串口</span>
</p>
```

```css
.tag-legend {
    margin-top: 0.5rem;
    font-size: 0.8rem;
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
}
```

## 配色原则

### 对比度
- 文字与背景对比度 ≥ 4.5:1
- 使用工具检查：https://webaim.org/resources/contrastchecker/

### 色盲友好
- 不要仅靠颜色区分信息
- 同时使用形状、图标、文字

### 一致性
- 同一类型内容使用相同颜色
- 全站保持统一的色彩语义

## 常见问题

### 标签颜色太多
**问题**：页面花哨，难以阅读
**解决**：限制在 5-6 种颜色以内

### 标签与背景融合
**问题**：标签看不清
**解决**：添加边框

```css
.tag {
    border: 1px solid rgba(0,0,0,0.1);
}
```

### 深色模式失效
**问题**：深色模式下标签颜色异常
**解决**：使用 CSS 变量

```css
@media (prefers-color-scheme: dark) {
    .tag {
        opacity: 0.9;
    }
}
```
