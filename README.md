# 🎨 UI Prompt Library

[![License: MIT](https://img.shields.io/badge/License-MIT-white.svg)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![Prompts](https://img.shields.io/badge/Prompts-5-blue.svg)](#)
[![Validate Prompts](https://github.com/P-r-e-m-i-u-m/ui-prompt-library/actions/workflows/validate.yml/badge.svg)](https://github.com/P-r-e-m-i-u-m/ui-prompt-library/actions/workflows/validate.yml)

> A curated, open-source collection of production-grade UI prompts for building landing pages, SaaS dashboards, and components — using React, Tailwind CSS, shadcn/ui, and Framer Motion.

**Copy a prompt → paste into Claude or GPT → get a fully working page.**

---

## 📦 What's Inside

| Category | Prompts | Stack |
|---|---|---|
| [SaaS Landing Pages](./saas/) | 3 prompts — hero sections, full pages | React + Vite + Tailwind + shadcn/ui |
| [Components](./components/) | 2 prompts — navbar, cards | Tailwind + Framer Motion |
| [Templates](./templates/) | Blank prompt skeleton | Any stack |

---

## 🚀 How to Use

### Option A — Use with Claude (recommended)
1. Open [claude.ai](https://claude.ai)
2. Copy any `.md` prompt file from this repo
3. Paste it and say: **"Build this exactly as specified"**
4. Claude generates the full code

### Option B — Use with ChatGPT
1. Copy the prompt
2. Start with: **"You are an expert React developer. Build the following UI exactly:"**
3. Paste the prompt

### Option C — Use with Cursor / Windsurf
1. Open your project
2. Press `Ctrl+K` or open AI chat
3. Paste the prompt directly

---

## 🧠 How to Write Your Own Prompt (The System)

The secret: **every design decision becomes a prompt line.**

### Step 1 — Find a UI you like
Screenshot any landing page, SaaS app, or component.

### Step 2 — Break it into layers
```
Stack → Design Tokens → Assets → Sections → Animations
```

### Step 3 — Use the template
Copy [`templates/PROMPT_TEMPLATE.md`](./templates/PROMPT_TEMPLATE.md) and fill it in.

### Step 4 — Be exact, not vague
❌ "Make a big heading"  
✅ `text-[80px] font-medium tracking-[-0.04em]`

❌ "Add a smooth animation"  
✅ `initial: { opacity: 0, y: 20 }, animate: { opacity: 1, y: 0 }, transition: { duration: 0.6, delay: 0.1 }`

### Step 5 — Screenshot → Prompt shortcut
Ask Claude:
> "Convert this screenshot into a detailed React + Tailwind prompt spec. List every component, exact Tailwind classes, colors in HSL, and animation details."

Then clean it up and add your asset URLs. Done in ~10 minutes.

---

## 📁 Repo Structure

```
ui-prompt-library/
├── README.md                          ← You are here
├── CONTRIBUTING.md                    ← How to add your prompt
│
├── saas/
│   ├── README.md                      ← Index of all SaaS prompts
│   ├── hero-dark-video-mindloop.md    ← Dark newsletter landing page
│   ├── hero-light-dashboard-nexora.md ← Light SaaS with dashboard preview
│   └── hero-dark-grow.md              ← Minimal dark hero with marquee
│
├── components/
│   └── README.md
│
└── templates/
    └── PROMPT_TEMPLATE.md             ← Blank skeleton for new prompts
```

---

## 🤝 Contributing

Want to add your own prompt? Read [`CONTRIBUTING.md`](./CONTRIBUTING.md).

Every merged prompt gets credited in the README.

---

## 📄 License

MIT — free to use, modify, and share.

---

## ✨ Contributors

| Avatar | Name | Contribution |
|---|---|---|
| [@P-r-e-m-i-u-m](https://github.com/P-r-e-m-i-u-m) | Syed Abdul Aman | Creator, all initial prompts |

Want your name here? Read [CONTRIBUTING.md](./CONTRIBUTING.md) and open a PR.

---

## 📊 Stats

- **5** prompts and counting
- **3** SaaS full-page prompts
- **2** component prompts
- Tested with **Claude** and **ChatGPT**

See [ROADMAP.md](./ROADMAP.md) for what's coming next.
