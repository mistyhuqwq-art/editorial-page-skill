# Editorial Warm Design

> An AI-readable design system for warm, editorial-style single-page HTML.
> 一份 AI 可读的设计系统规范，生成编辑杂志风格的单页网页。

<img width="800" alt="Editorial Warm Design preview" src="./example-project-card.html">

## ✨ What is this?

A **design system spec** (`DESIGN.md`) + **HTML template** (`template.html`) you can feed to any AI coding assistant — **Claude Code, Cursor, v0, Lovable, Copilot** — to generate visually consistent pages in the "editorial warm" style.

**Style characteristics:**
- 🎨 Warm cream background (`#f5f0e8`) + terracotta accent (`#c0542e`)
- 📖 Serif headlines + sans-serif body (Source Serif 4 / Noto Serif SC + Noto Sans SC)
- 🎯 Radical restraint — no gradients, no shadows, no icons
- 📐 Narrow 960px container, magazine-style section rhythm
- 🧱 10 composable blocks: hero / def-list / cards / compare-table / stats / roles / flow / stack / code / CTA

**Great for:** project cards · product landing pages · technical proposals · blog articles · résumés · pitch one-pagers · presentation web versions · team digests.

---

## 🚀 Three Ways to Use

### Option A: One-shot with any AI

```
Build a single-page HTML following this DESIGN.md:

[paste DESIGN.md contents]

Topic: [your topic]
Audience: [your audience]
Key messages: [3-7 points]
CTA: [what should readers do at the end]
Use at least 4 different section types from the 10 components.
```

### Option B: Fork the template

```bash
cp template.html my-page.html
# then edit the {{PLACEHOLDER}} slots
```

All CSS is inline — single file, no build tools, no dependencies beyond Google Fonts.

### Option C: Install as Claude Code Skill

If you use [Claude Code](https://claude.com/claude-code):

```bash
# Download skill bundle (coming soon to this repo's Releases)
curl -L https://github.com/YOUR_NAME/editorial-warm-design/releases/latest/download/editorial-page-skill.tar.gz | tar -xz -C ~/.claude/skills/

# Then in Claude Code, just ask:
# "Make me an editorial-style project card for X"
```

---

## 📦 What's in this repo

| File | Purpose |
|------|---------|
| `DESIGN.md` | The design system spec — **the main deliverable**. Feed this to any AI. |
| `template.html` | A blank HTML template with `{{PLACEHOLDER}}` slots for all 10 block types. |
| `example-project-card.html` | A real-world example: the project card this style was born from. |

---

## 🎨 Design Philosophy

Inspired by print editorial design. The goal is to make tech/product content feel **calm, credible, and readable** — the opposite of dashboard-style UIs saturated with gradients and icons.

Three anchors hold the style together:
1. **Color restraint** — 70% cream + 25% greyscale + 5% terracotta. No other hues.
2. **Typography hierarchy** — serif 900 for H1 vs sans 400 for body. Strong contrast builds magazine rhythm.
3. **Structural variety** — every page must mix at least 4 different block types. No uniform card grids.

See [DESIGN.md §7 Design Taboos](./DESIGN.md#7-design-taboos设计禁忌必读) for the negative rules — the things you must NOT do.

---

## 🔗 Inspired by

- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) — the pattern of AI-readable design specs
- [designmd.me](https://designmd.me/) — the tool that popularized DESIGN.md as a format

This repo contributes a specific style (warm editorial) to that ecosystem.

---

## 📝 License

MIT — use freely, modify freely, attribute if you want.

## 🙋 Credits

Born from the [Teamspace](https://github.com/) project card, Apr 2026.
Extracted and systematized by X and Claude.
