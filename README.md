# Editorial Page Skill · Design System Collection

> AI 可读的设计系统合集 —— 一层通用排版原则 + 多种视觉风味。
> 给任何 AI 工具(Claude Code / Cursor / v0 / Copilot / Lovable)生成视觉一致的单页 HTML。

---

## 两层架构

```
PRINCIPLES.md           ← 通用排版原则(6 条,所有风格都要遵守)
│
├── warm-editorial/     ← 风味 1: 暖色编辑杂志风 (米色 + 砖红 + 衬线)
│   ├── DESIGN.md
│   ├── template.html
│   └── example.html
│
└── [更多风格陆续加入]
```

### 为什么分两层

AI 生成的页面之所以"有 AI 味儿",**真正原因不在视觉层,在排版语法层** —— 结构可预测、信息密度均一、没有作者痕迹。

`PRINCIPLES.md` 抽出了这 6 条**跨风格通用的底层原则**。
每种风格的 `DESIGN.md` 只讲该风格自己的**视觉选择**(颜色、字体、装饰偏好)。

**风味可以变化,原则不能。** 一个用青紫渐变的页面可以气质高级(如果排版节制),一个用米色衬线的页面也可以 AI 味儿满满(如果结构模板化)。

---

## 怎么用

### Claude Code 用户

```bash
# 解压 skill 包到 ~/.claude/skills/
tar -xzf editorial-page-skill.tar.gz -C ~/.claude/skills/

# 然后在 Claude Code 里自然语言触发:
"帮我做个项目介绍页"
"生成一份本周周报"
"做一页个人简历"
```

Skill 会自动加载 PRINCIPLES.md + 对应风格的 DESIGN.md。

### 任何 AI 工具

把下面两份 Markdown 一起贴给 Cursor / v0 / Copilot / ChatGPT:

1. `PRINCIPLES.md` —— 通用排版原则
2. 你选的风格文件,如 `warm-editorial/DESIGN.md`

然后说:
```
Build a single-page HTML following the two Markdown specs above.

Topic: [主题]
Audience: [受众]
Key messages: [3-7 点]
CTA: [结尾希望读者做什么]

Apply PRINCIPLES.md's 6 rules (structural variety, density jump, spacing
rhythm, accent restraint, author signature, break uniformity) first.
Then apply the style's visual choices.
```

### Fork template

```bash
cp warm-editorial/template.html my-page.html
# 替换 {{PLACEHOLDER}} 占位符,所有 CSS inline,双击即可预览
```

---

## 当前风格

| 风格 | 气质 | 场景 |
|---|---|---|
| [warm-editorial](./warm-editorial/) | 米色底 + 砖红 + 衬线 + 克制 | 项目名片、产品 landing、周报、简历、博客长文、分享封面 |
| [tech-dark](./tech-dark/) | 暖中性黑 + Lime + italic serif 字族反差 + hairline 列表式 | 开发者工具、API 平台、CLI 产品、技术文档、基础设施。支持 `fx-rich` 开关切换克制/丰富表现力 |
| [minimal-mono](./minimal-mono/) | 纯黑白 + Inter + 等宽元信息 + 虚线分隔 + 粗细断崖(300 vs 900) | 技术博客、开源 README 展示、工程师个人站、论文式长文 |
| [retro](./retro/) | 奶油底 + 糖果三色(奶粉/天空蓝/奶油黄) + chunky 边框硬阴影 + CRT 细扫描 + 现代骨架 | 活动邀请、创作者作品集、独立游戏站、有玩心的产品 |
| [swiss-grid](./swiss-grid/) | 红黑二色 + Inter 900 uppercase + 12 栏精确对齐 + 1.25 modular scale | 出版/期刊、设计品牌、文化机构、严肃年报、排版研究 |
| [brutalist](./brutalist/) | 鲜黄底 + 纯黑 + Archivo Black 超粗 + 歪斜印章 + 黑黄反色块 + screamer 超大声量段 | 活动海报、观点宣言、创始人声明、竞选倡议、反叛品牌、音乐节 landing |

**在浏览器中对比选风味**:打开 [`preview-index.html`](./preview-index.html),5 个风味缩略图 + 对号入座的选择指南。

---

## 灵感来源

- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) —— AI 可读设计规范的生态
- [designmd.me](https://designmd.me/) —— 推广 DESIGN.md 作为格式的工具

本 repo 的贡献是:**把"通用原则层" (PRINCIPLES.md) 和"风味层" (DESIGN.md) 分开**,让规范可以在不同风格间复用,也让每个具体风格的规范更精简。

---

## License

MIT — 自由使用、修改、分发。

## Credits

由 X 和小克(Claude)共同提炼。风格最初诞生于 Teamspace 项目名片页(2026-04)。
