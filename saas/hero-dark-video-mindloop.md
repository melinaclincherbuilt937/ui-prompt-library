# Mindloop — Dark Monochrome Newsletter Landing Page

> **Stack:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui + Framer Motion + hls.js  
> **Category:** `saas` `marketing` `newsletter`  
> **Difficulty:** Advanced  
> **Theme:** Pure black background, white foreground — zero color, zero gradients beyond monochrome

---

## 📦 Dependencies

```bash
npm install framer-motion hls.js lucide-react
npm install @fontsource/inter @fontsource/instrument-serif
npx shadcn@latest init
npx shadcn@latest add button input
```

---

## 🎨 Design Tokens (`src/index.css`)

```css
@import "@fontsource/inter/400.css";
@import "@fontsource/inter/500.css";
@import "@fontsource/inter/600.css";
@import "@fontsource/inter/700.css";
@import "@fontsource/instrument-serif/400.css";
@import "@fontsource/instrument-serif/400-italic.css";

:root {
  --background:           0 0% 0%;
  --foreground:           0 0% 100%;
  --card:                 0 0% 5%;
  --card-foreground:      0 0% 100%;
  --primary:              0 0% 100%;
  --primary-foreground:   0 0% 0%;
  --secondary:            0 0% 12%;
  --secondary-foreground: 0 0% 85%;
  --muted:                0 0% 15%;
  --muted-foreground:     0 0% 65%;
  --accent:               170 15% 45%;
  --accent-foreground:    0 0% 100%;
  --border:               0 0% 20%;
  --input:                0 0% 18%;
  --ring:                 0 0% 40%;
  --hero-subtitle:        210 17% 95%;
}
```

---

## 🌀 Liquid Glass Effect (global CSS class)

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

## 🌀 Reusable Animation Helper

```ts
const fadeUp = (delay: number) => ({
  initial: { opacity: 0, y: 20 },
  whileInView: { opacity: 1, y: 0 },
  viewport: { once: true, margin: "-100px" },
  transition: { duration: 0.6, delay, ease: "easeOut" },
});
```

---

## 🖼️ Assets

| Asset | URL |
|---|---|
| Hero background video | `https://d8j0ntlcm91z4.cloudfront.net/user_38xzZboKViGWJOttwIXH07lWA1P/hf_20260325_120549_0cd82c36-56b3-4dd9-b190-069cfc3a623f.mp4` |
| Mission section video | `https://d8j0ntlcm91z4.cloudfront.net/user_38xzZboKViGWJOttwIXH07lWA1P/hf_20260325_132944_a0d124bb-eaa1-4082-aa30-2310efb42b4b.mp4` |
| Solution section video | `https://d8j0ntlcm91z4.cloudfront.net/user_38xzZboKViGWJOttwIXH07lWA1P/hf_20260325_125119_8e5ae31c-0021-4396-bc08-f7aebeb877a2.mp4` |
| CTA background (HLS) | `https://stream.mux.com/8wrHPCX2dC3msyYU9ObwqNdm00u3ViXvOSHUMRYSEe5Q.m3u8` |
| Avatars | `src/assets/avatar-1.png`, `avatar-2.png`, `avatar-3.png` |
| Platform icons | `src/assets/icon-chatgpt.png`, `icon-perplexity.png`, `icon-google.png` |

---

## 🏗️ Page Structure (top to bottom)

### 1. Navbar — fixed, fully transparent

```
Position: fixed top-0 z-50
Padding: px-8 md:px-28 py-4
Layout: flex items-center justify-between
Background: none (fully transparent)
```

**Left — Logo:**
```
Concentric circles icon:
  Outer: w-7 h-7 rounded-full border-2 border-foreground/60
  Inner: w-3 h-3 rounded-full border border-foreground/60 (centered inside outer)
Text: "Mindloop" font-bold ml-2
```

**Center-left — Nav links:**
```
Items: ["Home", "How It Works", "Philosophy", "Use Cases"]
Separator: • dot between each link
Color: text-muted-foreground hover:text-foreground transition-colors
```

**Right — Social icons:**
```
Icons: Instagram, Linkedin, Twitter (from lucide-react)
Each wrapped in: liquid-glass w-10 h-10 rounded-full flex items-center justify-center cursor-pointer
```

---

### 2. Hero Section — full viewport height

```
Height: min-h-screen
Position: relative overflow-hidden
```

**Background video:**
```tsx
<video
  autoPlay muted loop playsInline
  className="absolute inset-0 w-full h-full object-cover z-0"
  src="[HERO_VIDEO_URL]"
/>
```

**Bottom fade:**
```
<div className="absolute bottom-0 left-0 right-0 h-64 bg-gradient-to-t from-background to-transparent z-[1]" />
```

**Content (centered, z-10):**
```
className="relative z-10 flex flex-col items-center text-center pt-28 md:pt-32 px-4"
```

**Avatar social proof row:**
```
3 overlapping avatars: -space-x-2, each w-8 h-8 rounded-full border-2 border-background
Text: "7,000+ people already subscribed" — text-muted-foreground text-sm ml-3
Wrap in: flex items-center mb-6
```

**Heading:**
```
Size: text-5xl md:text-7xl lg:text-8xl
Weight: font-medium
Tracking: tracking-[-2px]
Text: "Get Inspired with Us"
"Inspired" → <span className="font-serif italic font-normal">Inspired</span>
```

**Subtitle:**
```
Size: text-lg
Color: style={{ color: "hsl(var(--hero-subtitle))" }}
Max-width: max-w-xl mx-auto mt-4 mb-8
Text: "Join our feed for meaningful updates, news around technology and a shared journey toward depth and direction."
```

**Email subscribe form:**
```
Wrapper: liquid-glass rounded-full p-2 max-w-lg w-full flex items-center gap-2
Input: flex-1 bg-transparent border-none outline-none text-foreground placeholder:text-muted-foreground px-4 text-sm
Button: bg-foreground text-background rounded-full px-8 py-3 text-sm font-medium
         whileHover={{ scale: 1.03 }} whileTap={{ scale: 0.98 }}
Text: "SUBSCRIBE"
```

---

### 3. "Search has changed" Section

```
Padding: pt-52 md:pt-64 pb-6 md:pb-9
Text align: center
```

**Heading:**
```
Size: text-5xl md:text-7xl lg:text-8xl
Text: "Search has changed. Have you?"
"changed." → <span className="font-serif italic">changed.</span>
```

**Subtitle:**
```
Size: text-lg
Color: text-muted-foreground
Max-width: max-w-2xl mx-auto mb-24
Text: "The way people find information has fundamentally shifted. Are you ready?"
```

**3 Platform cards (grid):**
```
Grid: grid md:grid-cols-3 gap-12 md:gap-8 mb-20
Each card: flex flex-col items-center text-center gap-4
  Icon image: w-[200px] h-[200px] object-contain
  Platform name: font-semibold text-base
  Description: text-muted-foreground text-sm max-w-[200px]
```

| Platform | Icon | Description |
|---|---|---|
| ChatGPT | `icon-chatgpt.png` | "Conversational AI that answers directly, no links needed." |
| Perplexity | `icon-perplexity.png` | "AI search that cites sources and skips the noise." |
| Google AI | `icon-google.png` | "Search with AI overviews replacing traditional results." |

**Bottom tagline:**
```
Text: "If you don't answer the questions, someone else will."
Size: text-sm
Color: text-muted-foreground
```

---

### 4. Mission Section — scroll-driven word reveal

```
Padding: pt-0 pb-32 md:pb-44
```

**Video:**
```tsx
<video
  autoPlay muted loop playsInline
  className="w-[800px] h-[800px] object-cover mx-auto mb-16"
  src="[MISSION_VIDEO_URL]"
/>
```

**Scroll reveal setup:**
```ts
const ref = useRef(null)
const { scrollYProgress } = useScroll({ target: ref, offset: ["start end", "end start"] })
```

**Paragraph 1 (word-by-word opacity reveal):**
```
Size: text-2xl md:text-4xl lg:text-5xl
Weight: font-medium
Tracking: tracking-[-1px]
Max-width: max-w-4xl mx-auto

Text: "We're building a space where curiosity meets clarity — where readers
find depth, writers find reach, and every newsletter becomes a conversation
worth having."

Highlighted words (opacity 1 always): "curiosity", "meets", "clarity"
All other words: opacity controlled by useTransform(scrollYProgress, [0.1, 0.5], [0.15, 1])
```

**Paragraph 2:**
```
Size: text-xl md:text-2xl lg:text-3xl
Weight: font-medium
Margin: mt-10
Max-width: max-w-3xl mx-auto

Text: "A platform where content, community, and insight flow together — with
less noise, less friction, and more meaning for everyone involved."

Same scroll-driven word opacity as paragraph 1.
```

---

### 5. Solution Section

```
Padding: py-32 md:py-44
Border: border-t border-border/30
```

**Label:**
```
Text: "SOLUTION"
Style: text-xs tracking-[3px] uppercase text-muted-foreground mb-4
```

**Heading:**
```
Size: text-4xl md:text-6xl
Text: "The platform for meaningful content"
"meaningful" → <span className="font-serif italic">meaningful</span>
```

**Video:**
```tsx
<video
  autoPlay muted loop playsInline
  className="w-full rounded-2xl aspect-[3/1] object-cover my-12"
  src="[SOLUTION_VIDEO_URL]"
/>
```

**4-column feature grid:**
```
Grid: grid md:grid-cols-4 gap-8 mt-12

Features:
1. Curated Feed — "Every post hand-picked for depth and relevance."
2. Writer Tools — "Everything you need to publish, grow, and earn."
3. Community — "Connect with readers who actually care."
4. Distribution — "Reach beyond your list with built-in amplification."

Each: title font-semibold text-base, description text-muted-foreground text-sm mt-2
```

---

### 6. CTA Section — HLS background video

```
Padding: py-32 md:py-44
Border: border-t border-border/30
Position: relative overflow-hidden
```

**HLS video setup:**
```tsx
// In useEffect:
if (Hls.isSupported()) {
  const hls = new Hls()
  hls.loadSource("https://stream.mux.com/8wrHPCX2dC3msyYU9ObwqNdm00u3ViXvOSHUMRYSEe5Q.m3u8")
  hls.attachMedia(videoRef.current)
} else if (video.canPlayType('application/vnd.apple.mpegurl')) {
  // Safari native HLS fallback
  video.src = hlsUrl
}

// Video element:
<video
  ref={videoRef}
  autoPlay muted loop playsInline
  className="absolute inset-0 w-full h-full object-cover z-0"
/>
```

**Overlay:**
```
<div className="absolute inset-0 bg-background/45 z-[1]" />
```

**Content (z-10, centered):**
```
Concentric circles icon (same as navbar but larger: w-10 h-10 outer, w-5 h-5 inner)
Heading: "Start Your Journey" → "Journey" in serif italic
           text-4xl md:text-6xl font-medium tracking-[-1px] my-4
Subtitle: text-muted-foreground text-lg max-w-md mx-auto mb-8
          "Join thousands of readers and writers building something meaningful."

Buttons (flex gap-4 justify-center):
  Primary: bg-foreground text-background rounded-lg px-8 py-3.5 font-medium
           Text: "Subscribe Now"
  Secondary: liquid-glass rounded-lg px-8 py-3.5
             Text: "Start Writing"
```

---

### 7. Footer

```
Padding: py-12 px-8 md:px-28
Layout: flex justify-between items-center
Border: border-t border-border/30
```

```
Left: "© 2026 Mindloop. All rights reserved." — text-muted-foreground text-sm
Right: Links ["Privacy", "Terms", "Contact"]
       text-muted-foreground text-sm hover:text-foreground
       gap-6 flex
```

---

## 💡 Key Design Decisions

- The **entire theme is monochrome** — no color, no gradients except black-to-transparent fades
- Liquid glass uses `rgba(255,255,255,0.01)` — nearly invisible background, the effect comes from the `::before` gradient border only
- Scroll word reveal: each `<span>` gets its own `useTransform` with a slightly offset scroll range to create a wave effect
- HLS video in the CTA requires `hls.js` for Chrome/Firefox; Safari handles `.m3u8` natively
- Font pairing: **Inter** (sans) for all UI text, **Instrument Serif italic** only for accent words in headings — never for body text

---

## 🏷️ Tags

`dark-theme` `monochrome` `newsletter` `video-background` `scroll-animation` `hls` `framer-motion`
