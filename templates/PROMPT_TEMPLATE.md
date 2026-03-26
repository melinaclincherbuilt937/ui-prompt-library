# [Prompt Name] — [Brief Description]

> **Stack:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui + Framer Motion  
> **Category:** `saas` / `component` / `marketing`  
> **Difficulty:** Beginner / Intermediate / Advanced  
> **Preview:** _(add screenshot URL here)_

---

## 📦 Dependencies

```bash
npm install framer-motion lucide-react
npx shadcn@latest init
npx shadcn@latest add button
# add more as needed
```

---

## 🎨 Design Tokens (`src/index.css`)

```css
@import url('https://fonts.googleapis.com/css2?family=FONT_NAME&display=swap');

:root {
  --background:          ;   /* e.g. 0 0% 0% */
  --foreground:          ;   /* e.g. 0 0% 100% */
  --card:                ;
  --card-foreground:     ;
  --primary:             ;
  --primary-foreground:  ;
  --secondary:           ;
  --secondary-foreground:;
  --muted:               ;
  --muted-foreground:    ;
  --accent:              ;
  --accent-foreground:   ;
  --border:              ;
  --input:               ;
  --ring:                ;
  --radius:              ;
  /* custom tokens */
}
```

> ⚠️ All values are HSL **without** the `hsl()` wrapper. Components use `hsl(var(--token))`.

---

## 🌀 Reusable Animation Helper

```ts
// Paste this at the top of any component file
const fadeUp = (delay: number) => ({
  initial: { opacity: 0, y: 20 },
  whileInView: { opacity: 1, y: 0 },
  viewport: { once: true, margin: "-100px" },
  transition: { duration: 0.6, delay, ease: "easeOut" },
});
```

---

## 🖼️ Assets

| Asset | URL / Path |
|---|---|
| Background video | `https://...` |
| Logo | `src/assets/logo.png` |
| Avatar 1 | `src/assets/avatar-1.png` |
| _(add more)_ | |

---

## 🏗️ Page Structure

### 1. Navbar
- **Position:** fixed, top-0, z-50, fully transparent
- **Left:** [Logo description]
- **Center:** [Nav links]
- **Right:** [CTA / icons]
- **Classes:** `px-8 md:px-28 py-4 flex items-center justify-between`

---

### 2. Hero Section
- **Height:** `min-h-screen` / `h-screen`
- **Background:** [video / gradient / solid]

#### Heading
```
Text: "Your Headline Here"
Sizes: text-5xl md:text-7xl lg:text-8xl
Weight: font-medium
Tracking: tracking-[-2px]
Serif word: wrap "ItalicWord" in <span className="font-serif italic font-normal">
```

#### Subheading
```
Text: "Your subtitle text here."
Size: text-lg
Color: text-muted-foreground
Max width: max-w-2xl mx-auto
```

#### CTA / Form
```
[Describe the button or email form here]
Animation: whileHover={{ scale: 1.03 }} whileTap={{ scale: 0.98 }}
```

---

### 3. [Section Name]
- **Padding:** `py-32 md:py-44`
- **Border:** `border-t border-border/30`

#### Content
```
[Describe this section's content]
```

---

### 4. Footer
```
Left: "© 2026 [Brand]. All rights reserved."
Right: Privacy · Terms · Contact
Classes: py-12 px-8 md:px-28 flex justify-between
Color: text-muted-foreground text-sm
```

---

## 💡 Key Design Decisions

- [Why you made specific choices]
- [Any gotchas or things AI needs to know]
- [e.g. "The dashboard overflows intentionally and is clipped by overflow-hidden"]

---

## 🏷️ Tags

`dark-theme` `video-background` `newsletter` `saas` `hero` _(edit as needed)_
