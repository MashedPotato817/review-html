# 📖 Review HTML - 考前速记生成器

> 从文件提取到 GitHub Pages 的全流程保姆级指南

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/MashedPotato817/review-html.svg)](https://github.com/MashedPotato817/review-html/stargazers)

## ✨ 特性

- 📚 **适用任何科目** - 工科、理科、文科、专业课
- 🎨 **蓝白/深色主题** - 可切换的视觉风格
- 📱 **移动端优化** - 响应式设计，表格自动转置
- 🏷️ **标签系统** - 掌握/理解/了解 三级标注
- ⚡ **速记卡片** - 公式、地址、数据速查
- 📝 **代码模板** - 编程类科目常用代码
- 🔢 **数学公式** - MathJax/LaTeX 支持

## 🚀 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/MashedPotato817/review-html.git
cd review-html
```

### 2. 选择模板

| 模板 | 用途 |
|------|------|
| `templates/css-variables.md` | 颜色主题（蓝白/深色） |
| `templates/card-structure.md` | 卡片结构模板 |
| `templates/color-tags.md` | 色彩标签系统 |
| `examples/reference-card.md` | 速记卡片示例 |

### 3. 创建页面

按照 `skill.md` 中的 6 阶段流程：

1. **内容提取** - 从 PPT/DOC/PDF 或已有文档开始
2. **内容整理** - 结构化为知识模块
3. **HTML 生成** - 创建响应式页面
4. **移动端优化** - 表格转置、响应式断点
5. **交互功能** - 手风琴折叠、导航、返回顶部
6. **部署** - 推送到 GitHub Pages

### 4. 部署到 GitHub

```bash
git add index.html
git commit -m "feat: 添加考前速记页面"
git push origin main
```

## 📁 项目结构

```
review-html/
├── README.md              # 项目说明
├── LICENSE                # MIT 许可证
├── skill.md               # 主流程文档
├── templates/
│   ├── css-variables.md   # 颜色主题
│   ├── card-structure.md  # 卡片结构
│   └── color-tags.md      # 色彩标签
└── examples/
    └── reference-card.md  # 速记卡片示例
```

## 🎯 导航方案

根据模块数量选择：

| 方案 | 适用场景 | 说明 |
|------|----------|------|
| A. 快速导航标签 | ≤ 15 个模块 | 横向滚动，简单直接 |
| B. 全屏导航 | > 15 个模块 | 汉堡菜单，全屏显示 |
| C. 两者结合 | 任意数量 | 快速导航 + 全屏导航 |

## 📚 参考项目

- [概率论考前速记](https://github.com/MashedPotato817/gailvlun-notes) - 深色主题、MathJax
- [英语考前速记](https://github.com/MashedPotato817/English-Notes) - 蓝白主题、词汇卡片
- [单片机考前速记](https://github.com/MashedPotato817/AT89S52-Notes) - 色彩编码、速记卡片

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

本项目基于 [MIT 许可证](LICENSE) 开源。

---

*Composed by MashedPotato*
