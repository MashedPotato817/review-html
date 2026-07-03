# CSS 变量模板

## 蓝白主题（推荐）

适用于大多数科目，阅读舒适，专业感强。

```css
:root {
    /* 主色调 */
    --primary: #2563eb;
    --primary-dark: #1d4ed8;
    --primary-light: #dbeafe;

    /* 功能色 */
    --success: #16a34a;
    --success-light: #dcfce7;
    --warning: #f59e0b;
    --warning-light: #fef3c7;
    --danger: #dc2626;
    --danger-light: #fee2e2;

    /* 中性色 */
    --bg: #f8fafc;
    --card-bg: #ffffff;
    --border: #e2e8f0;
    --text: #1e293b;
    --text-light: #64748b;
    --text-dim: #94a3b8;

    /* 布局 */
    --radius: 8px;
    --radius-lg: 12px;
    --shadow: 0 1px 3px rgba(0,0,0,0.1), 0 1px 2px rgba(0,0,0,0.06);
    --shadow-md: 0 4px 6px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.06);

    /* 字体 */
    --font-mono: 'JetBrains Mono', 'Cascadia Code', 'Fira Code', monospace;
    --font-body: 'Noto Sans SC', -apple-system, sans-serif;
}
```

## 深色主题（概率论风格）

适用于偏好深色模式的用户，护眼，科技感强。

```css
:root {
    --bg: #1a1a2e;
    --fg: #eaeaea;
    --accent: #00d4ff;
    --accent2: #ff6b6b;
    --card-bg: #16213e;
    --border: #0f3460;
    --highlight: #e94560;
    --success: #4ecca3;
    --warning: #ffd93d;
    --font-mono: 'JetBrains Mono', 'Fira Code', monospace;
    --font-sans: 'Noto Sans SC', -apple-system, sans-serif;
}
```

## 主题切换（可选）

支持用户手动切换主题：

```css
/* 深色模式自动检测 */
@media (prefers-color-scheme: dark) {
    :root {
        --bg: #0f172a;
        --card-bg: #1e293b;
        --border: #334155;
        --text: #e2e8f0;
        --text-light: #94a3b8;
    }
}
```

## 自定义滚动条

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

::-webkit-scrollbar-thumb:hover {
    background: var(--primary-dark);
}
```

## 使用建议

| 科目类型 | 推荐主题 | 理由 |
|----------|----------|------|
| 工科/理科 | 蓝白或深色 | 专业、清晰 |
| 文科/语言 | 蓝白 | 阅读舒适 |
| 数学/物理 | 深色 | 护眼，公式清晰 |
| 艺术设计 | 可自定义 | 按需调整 |

## 常见问题

### 颜色对比度不足
**问题**：文字看不清
**解决**：确保文字与背景对比度 ≥ 4.5:1

### 主题切换闪烁
**问题**：深色模式切换时闪烁
**解决**：使用 CSS 变量，不使用 JavaScript 切换

### 滚动条样式失效
**问题**：Firefox 不支持 webkit 滚动条
**解决**：添加标准属性

```css
scrollbar-width: thin;
scrollbar-color: var(--primary) var(--bg);
```
