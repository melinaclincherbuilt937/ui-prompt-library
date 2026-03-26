# SaaS Landing Page Prompts

All prompts build full pages — navbar, hero, sections, footer. Copy any `.md` file and paste directly into Claude or ChatGPT.

---

## Available Prompts

| Prompt | Theme | Difficulty | Key Features |
|---|---|---|---|
| [hero-dark-video-mindloop.md](./hero-dark-video-mindloop.md) | Dark monochrome | Advanced | HLS video, scroll word-reveal, liquid glass |
| [hero-light-dashboard-nexora.md](./hero-light-dashboard-nexora.md) | Light SaaS | Advanced | Coded dashboard preview, SVG chart, frosted glass |
| [hero-dark-grow.md](./hero-dark-grow.md) | Dark minimal | Intermediate | 230px gradient heading, video fade loop, logo marquee |

---

## Pattern: What Every SaaS Prompt Contains

```
1. Stack declaration
2. npm install commands
3. CSS design tokens (all HSL)
4. Special utility classes (liquid glass, etc.)
5. Animation helpers
6. Asset URLs (videos, images)
7. Section-by-section spec with exact Tailwind classes
8. Key design decisions (the "why")
9. Tags
```

---

## How to Add Your Own

1. Copy [`../templates/PROMPT_TEMPLATE.md`](../templates/PROMPT_TEMPLATE.md)
2. Fill in every section
3. Submit a PR — see [`../CONTRIBUTING.md`](../CONTRIBUTING.md)
