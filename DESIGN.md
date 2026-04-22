# DESIGN.md — Editorial Warm（编辑杂志风·赤陶米色）

> 一份可独立分享给任何 AI coding agent 的设计系统规范。
> 让 Cursor / Claude / Copilot / v0 / Lovable 等工具生成视觉一致的 UI。
>
> **使用方法**：把本文件完整贴给 AI，说 "Build UI following this DESIGN.md"。

---

## 1. Visual Theme & Mood（视觉主题与氛围）

**风格关键词**：编辑杂志风 / Editorial / Warm Minimalism / Print-inspired

**灵感来源**：高端印刷杂志的内页排版、独立出版物、书籍装帧设计

**情感基调**：
- 温暖（米色底色替代冷白，避免屏幕疲劳）
- 克制（装饰极简，靠排版撑场）
- 可信（衬线字体带来权威感）
- 有呼吸感（大量留白 + 窄容器）

**适用场景**：项目介绍页、产品 landing、技术方案、个人简历、博客长文、演讲稿在线版、团队周报、分享封面

**不适用**：B2C 电商（太冷静）、游戏站（太平静）、金融仪表盘（数据密度不够）

---

## 2. Color Palette（色彩系统）

### 核心三色（禁止扩充）

```css
--bg:       #f5f0e8;  /* 米色底（主背景，替代 #fff） */
--text:     #1a1a1a;  /* 近黑文字（不用纯黑 #000） */
--accent:   #c0542e;  /* 赤陶红/砖红（强调色，用量 <5%） */
```

### 辅助色（仅为灰度和 accent 透明度变体）

```css
--bg-card:         #fff;                    /* 卡片背景（唯一的纯白用处） */
--bg-code:         #1a1a2e;                 /* 深色代码块背景 */
--border:          rgba(0,0,0,0.08);        /* 统一边框色 */
--text-secondary:  #6b6560;                 /* 正文辅助色（段落描述） */
--text-light:      #999080;                 /* 最浅文字（标签、元信息） */
--accent-light:    rgba(192,84,46,0.08);    /* accent 极淡变体（hover/强调区域） */
```

### 配色禁忌

- ❌ **禁用**：绿色、蓝色、紫色等其他色相（除非作为角色标识的小圆点 8×8px）
- ❌ **禁用**：渐变（唯一例外：roadmap 高亮卡片可用 `linear-gradient(135deg, #fff, rgba(192,84,46,0.02))`）
- ❌ **禁用**：纯黑 `#000`、纯白 `#fff`（除卡片背景）
- ✅ **唯一允许的彩色点**：角色/标签的 8px 圆点（`#6366f1` / `#ec4899` / `#14b8a6` / `#f59e0b` / `#ef4444`），仅作为身份标识，不作为视觉主角

### 颜色使用比例

大致遵循 `70-25-5` 规则：
- **70%** 米色底 + 近黑文字
- **25%** 灰度（辅助文字、边框、卡片白底）
- **5%** 赤陶 accent（小红条、强调词、CTA、highlight 单元格）

---

## 3. Typography（排版系统）

### 字体栈

```css
--serif: 'Source Serif 4', 'Noto Serif SC', 'Georgia', serif;
--sans:  'Noto Sans SC', -apple-system, BlinkMacSystemFont, sans-serif;
```

**从 Google Fonts 加载**：
```
https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;600;700;900&family=Noto+Sans+SC:wght@300;400;500;600&family=Source+Serif+4:ital,opsz,wght@0,8..60,400;0,8..60,600;0,8..60,700;0,8..60,900;1,8..60,400&display=swap
```

### 字体分工（严格遵守）

| 元素 | 字体 | 原因 |
|------|------|------|
| h1 / h2 / h3 | **衬线** (serif) | 建立权威感和杂志感 |
| 正文 / 段落 / 标签 | **无衬线** (sans) | 屏幕可读性优先 |
| 数字墙大数字 | **衬线** | 视觉锚点 |
| 代码 / URL | `'SF Mono', 'Fira Code', monospace` | 技术感 |
| 章节小标签 "THE CORE IDEA" | sans + `letter-spacing: 0.15em` + uppercase | 杂志章节感 |

### 字号系统（clamp 响应式）

```css
h1: clamp(40px, 6vw, 64px)  font-weight: 900  line-height: 1.15
h2: clamp(28px, 4vw, 40px)  font-weight: 700  line-height: 1.2
h3: 18-20px                  font-weight: 600-700
正文: 14-15px                font-weight: 400  line-height: 1.7
辅助: 12-13px                font-weight: 300-400
标签: 11px                   font-weight: 600  uppercase  letter-spacing: 0.15em
大数字: 36px                 font-weight: 700  serif
```

### 字重对比

- 标题 900 / 正文 400 / 引语 300 — **强对比建立层级**
- 禁止全页都用 500-600（扁平化会失去杂志感）

### 中文排版细节

- 中英混排时，中文用 `Noto Serif/Sans SC`，英文自动 fallback 到 `Source Serif 4`
- 标点使用中文全角（，。；：""）
- `line-height: 1.7` 比常规网页（1.5）略高，为中文留呼吸

---

## 4. Component Styles（组件样式）

### 通用原则

- **边框**：仅 `1px solid rgba(0,0,0,0.08)`，不用其他粗细
- **圆角**：仅 `4px`，不用其他值（圆形元素除外）
- **阴影**：**完全不用 box-shadow**（这是本风格的关键禁忌）
- **过渡**：`transition: all 0.2s` 仅用于 CTA 按钮 hover

### 10 个核心区块

#### `.hero`（页首）
```
min-height: 92vh
padding: 120px 0 80px
```
必须包含：40×4px 红色小条（视觉锚点）+ h1 + hero-sub + hero-meta 元信息行

#### `.section-tag`（小标签）
```
font-size: 11px
letter-spacing: 0.15em
text-transform: uppercase
color: var(--text-light)
margin-bottom: 16px
```
每个 section 开头必备，用英文（"The Core Idea" / "Highlights" / "How It Works"）

#### `.hero-bar`（小红条）
```
width: 40px  height: 4px
background: var(--accent)
```
**标志性元素**。出现在 hero 和 ending 开头，作为视觉锚点。

#### `.def-list`（定义列表）
左侧 accent 色标签（"定义" / "动因" / "路径"）+ 右侧 h3 + 描述。用于讲 what/why/how 三段式。

#### `.card`（卡片）
```
background: #fff
border: 1px solid rgba(0,0,0,0.08)
border-radius: 4px
padding: 32px 28px
```
内部必须有 `.card-tag`（accent 色小标签）+ `h3`（衬线）+ `p`（正文）

#### `.card-grid`（卡片网格）
默认 3 列。复杂内容用 `grid-template-columns: 1fr 1fr` 改 2 列。`gap: 20px`

#### `.compare-table`（对比表）
```
border-collapse: collapse
无竖线，仅 border-bottom 分隔
第一列: width: 100px, font-weight: 500
.highlight 列: color: var(--accent)
```

#### `.stats-row`（数字墙）
```
display: flex  gap: 48px
padding: 40px 0
border-top + border-bottom: 1px（只这一处用上下双边框）
.num: serif 36px bold accent 色
.label: 13px 灰色
```

#### `.flow-steps`（流程步骤）
```
display: flex（横向）
counter-reset: step（自动编号）
::before 显示序号：serif 28px accent 色 opacity: 0.3
.flow-arrow: 绝对定位的 → 符号
```

#### `.ending`（CTA 收尾）
```
min-height: 60vh
text-align: center
CTA 按钮: 2px 边框，hover 时反色填充
等宽字体显示 URL
```

---

## 5. Layout Principles（布局原则）

### 容器

```css
.container {
  max-width: 960px;
  margin: 0 auto;
  padding: 0 48px;  /* 移动端 24px */
}
```

**为什么 960px**：比主流 1280px 窄很多，模拟杂志内页的视线聚焦。读者视线移动距离短，阅读节奏好。

### 垂直节奏

```
section padding: 80px 0        /* 章节之间 */
hero padding:    120px 0 80px  /* 首屏更大留白 */
段落间距:         56-64px       /* section-lead 到内容 */
紧凑间距:         16-24px       /* 标签到标题到副标题 */
```

### 章节三件套（每个 section 必备）

```html
<section>
  <div class="section-tag">THE CORE IDEA</div>    <!-- 英文小标签 -->
  <h2>中文标题<span class="accent">强调词</span></h2>  <!-- 衬线 + accent 色关键词 -->
  <p class="section-lead">补充引语，≤560px 宽</p>   <!-- 浅灰 300 字重 -->
  <!-- ... 内容区块 ... -->
</section>
```

### 结构多样性原则（最重要的布局规则）

**同一页面必须使用至少 4 种不同的区块类型**。禁止通篇都是 card-grid。

推荐组合顺序：
1. hero（必备）
2. def-list 或长段落（讲核心思想）
3. compare-table（建立差异化）
4. roles-row 或 card-grid（功能矩阵）
5. stats-row（建立可信度）
6. flow-steps（讲清机制）
7. stack-grid 或 code block（技术内容）
8. ending（必备）

---

## 6. Depth & Shadow（深度系统）

**核心原则：基本不用阴影**

唯一建立深度感的方式：
- **边框** `1px solid rgba(0,0,0,0.08)`
- **背景对比** 米色底 vs 白色卡片
- **字重对比** 900 vs 400

**禁忌**：
- ❌ `box-shadow: 0 4px 12px rgba(0,0,0,0.1)` 一律禁用
- ❌ `backdrop-filter: blur()` 一律禁用
- ❌ 3D transform、parallax 等特效一律禁用

**深色反差区域**（唯一例外）：
技术文档的代码块可以用深色背景 `#1a1a2e`，作为视觉变化点。但整块区域仍保持 `border-radius: 4px`，不加阴影。

---

## 7. Design Taboos（设计禁忌·必读）

这些是这个风格的**负面清单**，违反任何一条都会让风格崩坏：

1. ❌ **禁止加图标库**：Font Awesome、Lucide、Heroicons、emoji 全部不用。靠排版和文字说话。
2. ❌ **禁止渐变**：除了 roadmap 高亮卡片的极淡 2% accent 渐变外，一律不用。
3. ❌ **禁止阴影**：box-shadow 全页不出现。
4. ❌ **禁止霓虹色/高饱和**：任何 `#xxxxff` / `#ff00ff` / 荧光绿粉都不允许。
5. ❌ **禁止圆形/椭圆大按钮**：CTA 用 `border-radius: 4px` 方形按钮。圆形仅用于 8px 角色标识小点。
6. ❌ **禁止全宽满屏布局**：最大 960px，不要占满 1920px。
7. ❌ **禁止通篇一种区块**：必须混合使用 4 种以上。
8. ❌ **禁止动画/过渡**：除 CTA hover 外，不用 transition/animation。
9. ❌ **禁止无 section-tag**：每个章节开头必须有英文小标签。
10. ❌ **禁止整句 accent**：h2 的 accent 色只能包一个关键词，不能整句染色。

---

## 8. Accessibility & Print（可访问性与打印）

这个风格天然适合长阅读和纸面输出，a11y 和打印都必须默认到位,不能事后补。

### 必备的 `<head>` 字段

每一份产出的 HTML 都必须填齐这四个字段,AI 不许占位符遗留:

```html
<meta name="description" content="一句话概括本页">
<meta name="color-scheme" content="light only">    <!-- 本风格明确不做暗色模式 -->
<meta property="og:title" content="...">
<meta property="og:description" content="...">
```

**为什么 `color-scheme: light only`**:杂志风的温暖氛围依赖米色底色,如果浏览器自动反色(Safari 的 Reader Mode、系统深色模式污染),整个温度感会崩坏。明确声明只做亮色。

### 键盘聚焦(`:focus-visible`)

CTA 按钮、所有 `<a>` 都必须有可见聚焦样式。用 accent 色做 2px outline + 3px 外偏移:

```css
a:focus-visible, button:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 3px;
  border-radius: 2px;
}
```

**为什么 `:focus-visible` 而不是 `:focus`**:避免鼠标点击后还残留聚焦框,只在键盘导航时显示。

### 动效偏好(`prefers-reduced-motion`)

本风格本来就几乎没动效,但唯一的 CTA hover transition 也要对有前庭障碍的用户关闭:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    transition-duration: 0.01ms !important;
    animation-duration: 0.01ms !important;
  }
}
```

### 打印样式(`@media print`)

**杂志风的核心优势之一就是纸面输出**。这个风格的项目名片、周报、简历、方案文档,大概率会被打印或另存为 PDF。print 样式不是可选项:

必须处理的 5 件事:
1. **保留背景色**:`-webkit-print-color-adjust: exact` + `print-color-adjust: exact`,否则 `#f5f0e8` 被浏览器丢弃变纯白
2. **展开超链接**:`a[href^="http"]::after { content: " (" attr(href) ")" }`,让纸面读者看得到 URL
3. **防止分页切断**:`.card`、`.insight`、`.flow-steps`、`.stats-row` 加 `page-break-inside: avoid`
4. **标题不孤立**:`h1/h2/h3` 加 `page-break-after: avoid`,避免末尾只剩一个标题跟着空白
5. **页边距用物理单位**:`@page { margin: 16mm 14mm; }`

### a11y 最小检查清单

- [ ] 所有图片(如有)有 `alt` 属性
- [ ] 所有 `<a>` 有可见聚焦样式
- [ ] 色彩对比:正文 `#1a1a1a` on `#f5f0e8` ≈ 14:1 ✓,辅助 `#6b6560` on `#f5f0e8` ≈ 4.8:1 ✓
- [ ] 不靠纯颜色传递信息(.highlight 列除了颜色还有字重区分)
- [ ] 无自动播放动画

---

## 9. Responsive Behavior（响应式）

### 断点：仅用一个 `@media (max-width: 768px)`

不用多断点，保持简单。

### 移动端调整

```css
@media (max-width: 768px) {
  .container { padding: 0 24px; }              /* 内边距减半 */
  .card-grid { grid-template-columns: 1fr; }   /* 卡片堆叠 */
  .roles-row { flex-direction: column; }       /* 角色列堆叠 */
  .flow-steps { flex-direction: column; }      /* 流程步骤堆叠 */
  .flow-arrow { display: none; }               /* 箭头在竖向时隐藏 */
  .stack-grid { grid-template-columns: repeat(2, 1fr); }  /* 4 列变 2 列 */
  .stats-row { flex-wrap: wrap; gap: 32px; }
  .hero-meta { flex-wrap: wrap; gap: 32px; }
}
```

**字号保持 clamp()**：h1/h2 已用 `clamp()` 函数自动适配，移动端不需要额外缩放。

---

## 10. Agent Prompt Guidelines（AI 生成指南）

当让 AI 基于本规范生成页面时，提供以下引导：

### 生成前的思考步骤

1. **确定主题**：这页讲什么？用一句话概括。
2. **选择 6-10 个区块**：从第 4 节的 10 个组件里选，确保至少 4 种不同类型。
3. **规划章节顺序**：按"what → why → how → proof → CTA"的叙事逻辑。
4. **准备强调词**：每个 h2 选一个关键词做 accent 染色。

### 内容密度建议

- **hero 标题**：≤12 字中文，断成两行，accent 包 2-4 字关键词
- **section-lead**：≤60 字，≤560px 宽
- **卡片正文**：≤50 字，保证 3 行以内
- **对比表**：≤4 行 ≤3 列，highlight 列用 accent 色

### 自检清单（生成后必须验证）

- [ ] 使用了至少 4 种不同区块？
- [ ] 每个 section 有 `section-tag + h2 + section-lead`？
- [ ] 完全没有图标、emoji、阴影？
- [ ] 只有米色 + 砖红 + 灰度三种色相？
- [ ] h2 的 accent 只染了关键词而非整句？
- [ ] 有 hero（开头）和 ending CTA（结尾）？
- [ ] container 是 960px 不是 1280px？
- [ ] 移动端媒体查询完整？
- [ ] `<head>` 里的 meta description / og:title / og:description / color-scheme 都填了(非占位符)？
- [ ] 有 `@media print` 打印样式(保留背景色 + 防分页切断 + 展开 URL)？
- [ ] 有 `:focus-visible` 键盘聚焦样式？
- [ ] 有 `prefers-reduced-motion` 支持？

### 风格复刻的 One-shot 启动语

```
Build a single-page HTML following the DESIGN.md above.
Topic: [用户主题]
Audience: [受众]
Key messages: [3-7 条重点]
CTA: [结尾希望读者做什么]
Use at least 4 different section types from the 10 components.
```

---

## Appendix: Token Quick Reference

```css
/* 直接复制可用的完整 :root 变量 */
:root {
  --bg: #f5f0e8;
  --bg-card: #fff;
  --bg-code: #1a1a2e;
  --border: rgba(0,0,0,0.08);
  --text: #1a1a1a;
  --text-secondary: #6b6560;
  --text-light: #999080;
  --accent: #c0542e;
  --accent-light: rgba(192,84,46,0.08);
  --serif: 'Source Serif 4', 'Noto Serif SC', 'Georgia', serif;
  --sans: 'Noto Sans SC', -apple-system, BlinkMacSystemFont, sans-serif;
}
```

---

**Credits**：风格最初诞生于 Teamspace 项目名片页（2026-04），由 X 和小克提炼沉淀。
**License**：MIT — 自由使用、修改、分发。
