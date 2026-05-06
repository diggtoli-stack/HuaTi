# HuaTI — Project Context for Claude

## 项目概述

**产品名：** HuaTI（花花TI）
**核心概念：** 12题人格测试，MBTI版，结果是各种"以不同方式面对世界的花"。
**目标感觉：** 向内探索、诗意、安静但有力、让用户发现自己面对世界的方式。
**系列关系：** DogTI/CatTI 系列第三作，但调性完全不同——不是搞笑梗图，而是一次向内探索的旅程。

---

## 设计原则（不要改动）

- **视觉风格：** 像素风花卉（pixel art flowers），保持与系列一致的像素美学
- **配色：** 黑字白底，极简 UI
- **禁止：** 深色主题、复杂配色、搞笑风格、严肃的 MBTI 风格
- **字体：** 标题用 `Press Start 2P`（base64 内嵌），正文用系统字体
- **按钮：** 黑色胶囊形（`border-radius: 100px`），白字，带播放圆圈图标
- **调性关键词：** 诗意、安静、向内、生命状态、面对世界的方式

---

## 文件结构

```
/Users/junli/Desktop/huati-designs/
├── index.html         ← 生产主文件（Cloudflare Pages 入口）
├── huati-main.html    ← 开发主文件（内容与 index.html 完全相同）
├── CLAUDE.md          ← 本文件
├── QUIZ-LOGIC.md      ← 题目与结果逻辑文档
└── assets/            ← 静态资源目录
    ├── HUATI标题.png
    ├── 花文案.png
    └── 16种花.png × 16
```

主文件是**单文件 HTML**，所有 CSS 和 JS 内联，无构建工具，无外部依赖。

---

## 页面结构（huati-main.html）

三个页面，通过 `.page` / `.page.active` 切换显示：

| 页面 | ID | 内容 |
|------|-----|------|
| 封面页 | `#page-home` | 像素大标题 HUATI + 三行滚动像素花 + 文案 + 开始按钮 |
| 题目页 | `#page-quiz` | 进度条 + 像素花提示气泡 + 问题文本 + 3个选项(A/B/C) |
| 结果页 | `#page-result` | 花格名称 + 副标题 + 生命状态描述 + 性格标签 + 内心独白 + 分享/再测按钮 |

### 首页关键实现
- 花卉滚动带：CSS `@keyframes`，第1、3行向左，第2行向右
- 像素花：`<img src="assets/花种.png">` PNG 文件，`image-rendering: pixelated`
- 标题：`assets/HUATI标题.png`，文案：`assets/花文案.png`

---

## 测试逻辑

- **12道题**，每个选项标记 MBTI 维度（E/I、S/N、T/F、J/P）
- 每题3个选项（A/B/C），选项覆盖不同维度
- 题目视角：**"我"是一朵花**，全程第一视角，经历从种子到凋谢的一生
- `calcResult()` 统计各维度计数，4个维度各取多数，组合成16种 MBTI 类型
- 详细题目、维度映射、结果数据见 → `QUIZ-LOGIC.md`

### 16种结果（格式：生命状态+花种）

| MBTI | 结果名 | 花种 | flower key |
|------|--------|------|------------|
| ENTJ | 先破土再说的剑兰 | 剑兰 | gladiolus |
| ENTP | 哪里都能扎根的蒲公英 | 蒲公英 | dandelion |
| ENFJ | 替所有人开花的绣球 | 绣球 | hydrangea |
| ENFP | 一朵花开了还想开满树的樱花 | 樱花 | cherryblossom |
| ESTJ | 按时开放绝不含糊的桂花 | 桂花 | osmanthus |
| ESTP | 突然就开了的昙花 | 昙花 | epiphyllum |
| ESFJ | 开满了整面墙的紫藤 | 紫藤 | wisteria |
| ESFP | 走到哪开到哪的向日葵 | 向日葵 | sunflower |
| INTJ | 开在悬崖上的雪莲 | 雪莲 | snowlotus |
| INTP | 慢慢开不知道在等什么的睡莲 | 睡莲 | waterlily |
| INFJ | 开在水里却向往天空的荷花 | 荷花 | lotus |
| INFP | 仔细看才发现很美的铃兰 | 铃兰 | lilyofthevalley |
| ISTJ | 每年同一天准时开的白玉兰 | 白玉兰 | magnolia |
| ISTP | 开完就走不回头的虞美人 | 虞美人 | poppy |
| ISFJ | 默默开满整片山坡的满天星 | 满天星 | babysbreath |
| ISFP | 慢慢开慢慢落不着急的木槿 | 木槿 | hibiscus |

---

## 结果页文案规范

- 标签文字：**「你的花格是」**
- 结果格式：生命状态+花种（共16种花）
- 生命状态描述：不是花语，而是"这朵花如何面对世界"

---

## 部署

- **平台：** Cloudflare Pages（主用）→ huati.pages.dev
- **GitHub 仓库：** diggtoli-stack/huati-designs
- **流程：** 用户确认OK → 推送 GitHub → Cloudflare 自动重新部署

---

## 用户偏好（重要）

- **只改文案时，不动设计和结构**
- 修改某一项时，只改被指定的那一项，其余保持原样
- 不要主动"顺手"优化代码、重构结构、添加功能
