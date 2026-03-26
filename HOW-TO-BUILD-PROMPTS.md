# How to Build Prompts Fast

The people writing great UI prompts aren't starting from scratch each time. They use a repeatable system. Here's the exact system.

---

## The Core Insight

**Every design decision becomes a prompt line.**

When you build a UI, you're making hundreds of micro-decisions — font size, spacing, color, animation duration. A great prompt captures all of them. A vague prompt captures none.

---

## Method 1: Screenshot → Prompt (fastest, ~10 min)

1. Find a landing page you want to replicate (Dribbble, Mobbin, Awwwards)
2. Take a screenshot
3. Open Claude and say:

```
Convert this screenshot into a detailed React + Tailwind CSS prompt spec.
Include:
- Exact Tailwind classes for layout, spacing, typography
- All colors as HSL CSS variables
- Font names and weights
- Animation specs (duration, delay, easing)
- Component breakdown (navbar, hero, sections, footer)
- Any special effects (glass, blur, gradients)
```

4. Claude gives you a rough spec. Clean it up, add real asset URLs, fill in missing values.
5. Done.

---

## Method 2: Build → Document (most accurate)

1. Build the UI normally in React + Tailwind
2. When it looks right, open your code
3. For each component, write down:
   - The exact className strings
   - The Framer Motion values
   - The CSS variable values
4. Paste into the prompt template

This gives you 100% accurate prompts because you're reverse-engineering working code.

---

## Method 3: Variation Chain (build a library fast)

Start with one working prompt. Vary one thing at a time:

```
Base: dark-hero-video.md
  ↓ change theme
light-hero-video.md
  ↓ swap video for image
light-hero-image.md
  ↓ add dashboard preview
light-hero-image-dashboard.md
  ↓ change stack
light-hero-image-dashboard-nextjs.md
```

Each variation is a new prompt. 5 variations = 5 prompts in an hour.

---

## The Anatomy of a Prompt

Every good prompt has 5 layers:

### Layer 1 — Stack declaration
```
React + Vite + TypeScript + Tailwind CSS + shadcn/ui + Framer Motion
```
AI needs to know exactly which tools to use upfront.

### Layer 2 — Design tokens
```css
:root {
  --background: 0 0% 0%;
  --foreground: 0 0% 100%;
  /* ... all tokens */
}
```
This is the design system. Everything references these. Never use raw hex in prompts.

### Layer 3 — Assets
```
Video: https://...
Logo: src/assets/logo.png
```
Real URLs baked in. AI can't guess asset paths.

### Layer 4 — Section specs
```
Heading:
  text-5xl md:text-7xl lg:text-8xl
  font-medium tracking-[-2px]
  Text: "Get Inspired with Us"
  "Inspired" → font-serif italic
```
Exact. Not "big heading in serif".

### Layer 5 — Key design decisions
```
- Dashboard intentionally overflows — clipped by overflow-hidden
- HLS video requires hls.js for Chrome, native for Safari
```
The "why" that prevents AI from second-guessing your decisions.

---

## Common Mistakes

| ❌ Vague | ✅ Exact |
|---|---|
| "large heading" | `text-[80px] tracking-[-0.04em]` |
| "smooth animation" | `duration: 0.6, delay: 0.1, ease: "easeOut"` |
| "dark background" | `--background: 260 87% 3%` |
| "glass effect" | Full `.liquid-glass` CSS block |
| "add a video" | Full video URL + `autoPlay muted loop playsInline` + fade logic |
| "nice card" | `rounded-2xl border border-border/30 bg-card p-6` |

---

## Prompt Length Guide

| Type | Target Length |
|---|---|
| Single component | 200–400 words |
| Hero section | 400–800 words |
| Full landing page | 800–1500 words |
| Complex page (dashboard) | 1500–2500 words |

Longer is almost always better. AI hallucinates when it has to guess.

---

## Testing Your Prompt

Before adding to the library, test it:

1. Paste into Claude: *"Build this exactly as specified"*
2. Check:
   - Does it install the right dependencies?
   - Are all sections present?
   - Are fonts/colors correct?
   - Do animations work?
3. If something is wrong, find the ambiguous line in your prompt and make it more specific
4. Re-test until the output is close to your intention

---

## The 80/20 Rule

80% of the visual quality comes from:
1. Getting the **color tokens** right (spend time here)
2. Getting the **heading sizes and tracking** right
3. Getting the **animation easing and duration** right
4. Using the right **font pairing**

Everything else is secondary.
