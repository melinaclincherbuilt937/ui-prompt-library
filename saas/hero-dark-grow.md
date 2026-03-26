# Grow — Dark Minimal Hero with Video + Logo Marquee

> **Stack:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui  
> **Category:** `saas` `talent` `hero`  
> **Difficulty:** Intermediate  
> **Theme:** Deep dark purple background, subtle video section, animated logo marquee

---

## 📦 Dependencies

```bash
npm install framer-motion lucide-react
npm install @fontsource/geist-sans
npx shadcn@latest init
npx shadcn@latest add button
```

---

## 🎨 Design Tokens (`src/index.css`)

```css
@import "@fontsource/geist-sans/400.css";
@import "@fontsource/geist-sans/500.css";
@import "@fontsource/geist-sans/600.css";
@import "@fontsource/geist-sans/700.css";

:root {
  --background:           260 87% 3%;
  --foreground:           40 6% 95%;
  --card:                 240 6% 9%;
  --card-foreground:      40 6% 95%;
  --primary:              262 83% 58%;
  --primary-foreground:   0 0% 100%;
  --secondary:            240 4% 16%;
  --secondary-foreground: 40 6% 95%;
  --muted:                240 4% 16%;
  --muted-foreground:     240 5% 65%;
  --accent:               262 83% 58%;
  --accent-foreground:    0 0% 100%;
  --border:               240 4% 20%;
  --input:                240 4% 20%;
  --ring:                 262 83% 58%;
  --radius:               0.75rem;
  --hero-heading:         40 10% 96%;
  --hero-sub:             40 6% 82%;
}

body {
  font-family: 'Geist Sans', 'Inter', system-ui, sans-serif;
  background-color: hsl(var(--background));
  color: hsl(var(--foreground));
}
```

---

## 🌀 Liquid Glass Utility

```css
.liquid-glass {
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  border: none;
  box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1);
  position: relative;
  overflow: hidden;
}
.liquid-glass::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.4px;
  background: linear-gradient(180deg,
    rgba(255,255,255,0.45) 0%, rgba(255,255,255,0.15) 20%,
    rgba(255,255,255,0) 40%, rgba(255,255,255,0) 60%,
    rgba(255,255,255,0.15) 80%, rgba(255,255,255,0.45) 100%);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

---

## 🎞️ Marquee Animation (tailwind.config.ts)

```ts
theme: {
  extend: {
    keyframes: {
      marquee: {
        '0%': { transform: 'translateX(0%)' },
        '100%': { transform: 'translateX(-50%)' },
      },
    },
    animation: {
      marquee: 'marquee 20s linear infinite',
    },
  },
}
```

---

## 🖼️ Assets

| Asset | URL |
|---|---|
| Social proof background video | `https://d8j0ntlcm91z4.cloudfront.net/user_38xzZboKViGWJOttwIXH07lWA1P/hf_20260308_114720_3dabeb9e-2c39-4907-b747-bc3544e2d5b7.mp4` |
| Logo | `src/assets/logo.png` (32px height) |

---

## 🏗️ Page Structure

> The Index page renders `<HeroSection />` then `<SocialProofSection />` sequentially with no wrapper styling.

---

### 1. Navbar

```
Layout: flex items-center justify-between
Padding: py-5 px-8
Font: Geist Sans
```

**Left — Logo:**
```tsx
<img src="/src/assets/logo.png" alt="Logo" style={{ height: 32 }} />
```

**Center — Nav links:**
```
Items: ["Features" (+ ChevronDown), "Solutions", "Plans", "Learning" (+ ChevronDown)]
Style: text-foreground/90 text-base gap-1 between icon and text
Each item: flex items-center gap-1 cursor-pointer hover:text-foreground transition-colors
```

**Right — Sign Up:**
```
Variant: heroSecondary (liquid-glass rounded-full)
Size: sm
Text: "Sign Up"
Padding: px-4 py-2
```

**Divider below navbar:**
```
<div className="mt-[3px] w-full h-px bg-gradient-to-r from-transparent via-foreground/20 to-transparent" />
```

---

### 2. Hero Section

```
Tag: <section>
Classes: bg-background relative overflow-hidden
Layout: contains Navbar + hero content stacked
```

**Content block (below navbar + divider):**
```
Padding: pt-20 px-4
Layout: flex flex-col items-center
```

**Main heading "Grow":**
```
Size: text-[230px]
Weight: font-normal
Line height: leading-[1.02]
Tracking: tracking-[-0.024em]
Font: 'General Sans', sans-serif  ← note: different from body font

Gradient text:
  className="bg-clip-text text-transparent"
  style={{
    backgroundImage: "linear-gradient(223deg, #E8E8E9 0%, #3A7BBF 104.15%)"
  }}

Text: Grow
```

**Subtext:**
```
Style: text-hero-sub text-center text-lg leading-8 max-w-md mt-4 opacity-80
Text line 1: "The most powerful AI ever deployed"
Text line 2: "in talent acquisition"
Use <br/> between lines
```

**CTA Button:**
```
Motion: { initial: { opacity:0, y:10 }, animate: { opacity:1, y:0 }, transition: { delay:0.3 } }
Wrapper: mt-8 mb-[66px]
Variant: heroSecondary (liquid-glass rounded-full)
Text: "Schedule a Consult"
Padding: px-[29px] py-[24px]
```

---

### 3. Social Proof / Video Section

```
Tag: <section>
Classes: relative w-full overflow-hidden
```

**Background video with manual fade loop:**
```tsx
const videoRef = useRef<HTMLVideoElement>(null)
const animFrameRef = useRef<number>()

useEffect(() => {
  const video = videoRef.current
  if (!video) return

  const FADE_DURATION = 0.5

  const tick = () => {
    if (!video.duration) { animFrameRef.current = requestAnimationFrame(tick); return }

    const t = video.currentTime
    const d = video.duration
    let opacity = 1

    if (t < FADE_DURATION) {
      opacity = t / FADE_DURATION
    } else if (t > d - FADE_DURATION) {
      opacity = (d - t) / FADE_DURATION
    }

    video.style.opacity = String(Math.max(0, Math.min(1, opacity)))
    animFrameRef.current = requestAnimationFrame(tick)
  }

  const handleEnded = () => {
    video.style.opacity = '0'
    setTimeout(() => {
      video.currentTime = 0
      video.play()
    }, 100)
  }

  video.addEventListener('ended', handleEnded)
  video.play()
  animFrameRef.current = requestAnimationFrame(tick)

  return () => {
    cancelAnimationFrame(animFrameRef.current!)
    video.removeEventListener('ended', handleEnded)
  }
}, [])

// Video element:
<video
  ref={videoRef}
  muted playsInline
  className="absolute inset-0 w-full h-full object-cover"
  style={{ opacity: 0 }}
  src="[VIDEO_URL]"
/>
```

**Gradient overlays:**
```tsx
<div className="absolute inset-0 bg-gradient-to-b from-background via-transparent to-background" />
```

**Content (z-10):**
```
Classes: relative z-10 flex flex-col items-center pt-16 pb-24 px-4 gap-20
```

**Spacer:**
```
<div className="h-40" />   {/* exposes the video in the middle */}
```

**Logo Marquee:**
```
Wrapper: flex items-start gap-8 max-w-5xl w-full overflow-hidden

Left label (shrink-0 whitespace-nowrap):
  text-foreground/50 text-sm
  Line 1: "Relied on by brands"
  Line 2: "across the globe"
  Use <br/>

Right marquee container (overflow-hidden flex-1):
  Inner div: flex gap-16 animate-marquee whitespace-nowrap
  Content is DUPLICATED for seamless loop

Logo item structure (each brand appears twice):
  <div className="flex items-center gap-2 flex-shrink-0">
    <div className="liquid-glass w-6 h-6 rounded-lg flex items-center justify-center text-[10px] font-bold">
      {brand[0]}   {/* First letter */}
    </div>
    <span className="text-base font-semibold text-foreground">{brand}</span>
  </div>

Brands: ["Vortex", "Nimbus", "Prysma", "Cirrus", "Kynder", "Halcyn"]
Gap between items: gap-16
```

---

## 💡 Key Design Decisions

- **"Grow" is 230px** — intentionally massive, takes up most of the viewport width
- The **gradient on "Grow"** goes from near-white to blue — only place color appears in the whole design
- Video fade is **manual via requestAnimationFrame** — browser `loop` doesn't allow custom fade in/out transitions
- The marquee duplicates all brands so the scroll is seamless (when first copy scrolls off, second copy is already in position)
- `heroSecondary` and `hero` button variants must be added to `shadcn/ui button.tsx` manually

---

## 🏷️ Tags

`dark-theme` `talent-acquisition` `logo-marquee` `video-fade-loop` `gradient-text` `minimal`
