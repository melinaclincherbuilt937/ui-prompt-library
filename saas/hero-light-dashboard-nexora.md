# Nexora — Light SaaS Hero with Dashboard Preview

> **Stack:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui + Framer Motion  
> **Category:** `saas` `fintech` `dashboard`  
> **Difficulty:** Advanced  
> **Theme:** Light white background, dark charcoal text — no dark mode

---

## 📦 Dependencies

```bash
npm install framer-motion lucide-react
npx shadcn@latest init
npx shadcn@latest add button
```

---

## 🎨 Design Tokens (`src/index.css`)

```css
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Inter:wght@400;500;600&display=swap');

:root {
  --background:           0 0% 100%;
  --foreground:           210 14% 17%;
  --primary:              210 14% 17%;
  --primary-foreground:   0 0% 100%;
  --secondary:            0 0% 96%;
  --secondary-foreground: 0 0% 9%;
  --muted:                0 0% 96%;
  --muted-foreground:     184 5% 55%;
  --accent:               239 84% 67%;
  --accent-foreground:    0 0% 100%;
  --border:               0 0% 90%;
  --input:                0 0% 90%;
  --ring:                 239 84% 67%;
  --radius:               0.5rem;
  --font-display:         'Instrument Serif', serif;
  --font-body:            'Inter', sans-serif;
  --shadow-dashboard:     0 25px 80px -12px rgba(0,0,0,0.08), 0 0 0 1px rgba(0,0,0,0.06);
}

body {
  font-family: var(--font-body);
  background-color: hsl(var(--background));
  color: hsl(var(--foreground));
}
```

---

## 🌀 Reusable Animation Helper

```ts
const fadeUp = (delay: number) => ({
  initial: { opacity: 0, y: 16 },
  animate: { opacity: 1, y: 0 },
  transition: { duration: 0.6, delay, ease: "easeOut" },
});
```

---

## 🖼️ Assets

| Asset | URL |
|---|---|
| Background video | `https://d8j0ntlcm91z4.cloudfront.net/user_38xzZboKViGWJOttwIXH07lWA1P/hf_20260319_015952_e1deeb12-8fb7-4071-a42a-60779fc64ab6.mp4` |

---

## 🏗️ Page Structure

> ⚠️ The entire page is `h-screen flex flex-col overflow-hidden` — Navbar + Hero fill exactly 100vh with no scroll.

---

### 1. Navbar

```
Layout: flex items-center justify-between
Padding: px-6 md:px-12 lg:px-20 py-5
Font: font-body
```

**Left — Logo:**
```
Text: "✦ Nexora"
Style: text-xl font-semibold tracking-tight text-foreground
```

**Center — Nav links (hidden on mobile):**
```
Items: ["Home", "Pricing", "About", "Contact"]
Style: text-sm text-muted-foreground hover:text-foreground transition-colors gap-8
Hidden: hidden md:flex
```

**Right — CTA:**
```
Button: rounded-full px-5 text-sm font-medium
Variant: primary (bg-foreground text-background)
Text: "Get Started"
```

---

### 2. Hero Section

```
Position: relative flex-1 overflow-hidden
Layout: flex flex-col items-center justify-start
Padding: pt-16 px-4 (content starts below navbar, not full center)
```

**Background video:**
```tsx
<video
  autoPlay muted loop playsInline
  className="absolute inset-0 w-full h-full object-cover z-0"
  src="[VIDEO_URL]"
/>
```

**Content wrapper:**
```
className="relative z-10 flex flex-col items-center w-full"
```

**1. Badge:**
```
Motion: { initial: { opacity:0, y:10 }, animate: { opacity:1, y:0 }, transition: { duration:0.5 } }
Style: inline-flex items-center gap-1.5 rounded-full border border-border
       bg-background px-4 py-1.5 text-sm text-muted-foreground font-body mb-6
Text: "Now with GPT-5 support ✨"
```

**2. Headline:**
```
Motion: fadeUp(0.1)
Style: text-center font-display text-5xl md:text-6xl lg:text-[5rem]
       leading-[0.95] tracking-tight text-foreground max-w-xl

Text: "The Future of Smarter Automation"
"Smarter" → <span style={{ fontFamily: 'Instrument Serif', fontStyle: 'italic' }}>Smarter</span>
```

**3. Subheadline:**
```
Motion: fadeUp(0.2)
Style: mt-4 text-center text-base md:text-lg text-muted-foreground
       max-w-[650px] leading-relaxed font-body

Text: "Automate your busywork with intelligent agents that learn, adapt,
and execute—so your team can focus on what matters most."
```

**4. CTA Buttons:**
```
Motion: fadeUp(0.3)
Wrapper: mt-5 flex items-center gap-3

Primary button:
  Style: rounded-full px-6 py-5 text-sm font-medium font-body
  Variant: default (bg-foreground text-background)
  Text: "Book a demo"

Play button:
  Style: h-11 w-11 rounded-full border-0 bg-background
         shadow-[0_2px_12px_rgba(0,0,0,0.08)] hover:bg-background/80
  Icon: <Play className="h-4 w-4 fill-foreground" />
```

**5. Dashboard Preview:**
```
Motion: { initial: { opacity:0, y:30 }, animate: { opacity:1, y:0 }, transition: { duration:0.8, delay:0.5 } }
Wrapper: mt-8 w-full max-w-5xl

Frosted glass container (inline styles):
  background: "rgba(255, 255, 255, 0.4)"
  border: "1px solid rgba(255, 255, 255, 0.5)"
  boxShadow: "var(--shadow-dashboard)"
  borderRadius: "1rem"
  padding: "12px" (md: "16px")
  overflow: "hidden"
```

**Dashboard internals** — all coded in React, `text-[11px] select-none pointer-events-none`:

```
Top bar (flex items-center px-3 py-2 border-b gap-2):
  - Logo box: rounded bg-foreground text-background w-5 h-5 text-[10px] flex items-center justify-center → "N"
  - "Nexora" text-[11px] font-semibold + ChevronDown w-3 h-3
  - Divider
  - Search: rounded bg-secondary px-2 py-1 text-muted-foreground text-[10px] flex items-center gap-1
    → Search icon w-3 h-3 + "Search..." + "⌘K" in rounded bg-muted
  - Spacer (flex-1)
  - "Move Money" button: text-[10px] rounded-full bg-accent text-accent-foreground px-3 py-1
  - Bell icon w-4 h-4
  - Avatar: w-6 h-6 rounded-full bg-secondary flex items-center justify-center text-[9px] font-semibold → "JB"

Main area (flex flex-1 overflow-hidden):

  Sidebar (w-40 border-r p-2 flex flex-col gap-0.5):
    Items with icon placeholders (w-3 h-3 rounded-sm bg-muted-foreground/20):
      - Home (active: bg-secondary rounded px-2 py-1)
      - Tasks + badge "10" (rounded-full bg-accent text-accent-foreground text-[8px] px-1)
      - Transactions
      - Payments + ChevronRight
      - Cards
      - Capital
      - Accounts + ChevronRight
    Section label "Workflows" text-[9px] uppercase tracking-wider text-muted-foreground mt-3 mb-1 px-2:
      - Trake rutes
      - Payments
      - Notifications
      - Settings

  Main content (flex-1 bg-secondary/30 p-3 overflow-hidden flex flex-col gap-3):

    Greeting:
      "Welcome, Jane" text-sm font-semibold

    Action buttons row (flex gap-1.5 flex-wrap):
      ["Send", "Request", "Transfer", "Deposit", "Pay Bill", "Create Invoice"]
      Each: rounded-full text-[10px] px-3 py-1 bg-background border border-border
      "Send": bg-accent text-accent-foreground (highlighted)
      + "Customize" text-[10px] text-muted-foreground ml-auto

    Two cards (flex gap-3):

      Balance card (flex-1 basis-0 bg-background rounded-lg p-3):
        Header: "Mercury Balance" text-[10px] text-muted-foreground + CheckCircle w-3 h-3 text-green-500
        Amount: "$8,450,190" text-base font-semibold + ".32" text-xs text-muted-foreground
        Stats row: "Last 30 Days" | "+$1.8M" text-green-600 | "-$900K" text-red-500
        SVG area chart (h-20 w-full):
          path d="M0,60 C20,55 40,20 80,25 C120,30 140,45 180,40 C220,35 240,15 280,20 C320,25 340,50 380,45"
          Stroke: hsl(var(--accent)), strokeWidth="1.5", fill="none"
          Fill path (same path + L380,80 L0,80 Z):
            linearGradient id="chartGrad" from accent at 15% opacity to transparent

      Accounts card (flex-1 basis-0 bg-background rounded-lg p-3):
        Header: "Accounts" text-[10px] font-semibold + Plus w-3 h-3 + MoreHorizontal w-3 h-3
        Three rows (py-3 flex justify-between text-xs, no dividers):
          - Credit · $98,125.50
          - Treasury · $6,750,200.00
          - Operations · $1,592,864.82
        Colors: label text-muted-foreground, amount text-foreground font-medium

    Transactions table:
      Header: "Recent Transactions" text-xs font-semibold
      Table (w-full text-[10px]):
        Columns: Date | Description | Amount | Status
        Rows:
          Mar 15 | AWS Infrastructure | -$5,200 | Pending (amber badge)
          Mar 14 | Client Payment | +$125,000 | Completed (green badge)
          Mar 13 | Payroll | -$85,450 | Completed (green badge)
          Mar 12 | Office Supplies | -$1,200 | Completed (green badge)
        Badge style: rounded-full px-2 py-0.5 text-[9px]
          Pending: bg-amber-100 text-amber-700
          Completed: bg-green-100 text-green-700
```

---

## 💡 Key Design Decisions

- The dashboard **intentionally overflows** the bottom of the viewport — it's clipped by `overflow-hidden` on the parent for a dramatic partial-reveal effect
- The SVG chart uses a **hand-crafted cubic Bézier path** — no chart library needed
- Light only — no dark mode
- All colors use `hsl(var(--token))` — never raw hex values in components
- The frosted glass container uses `rgba` directly (not Tailwind) because the opacity needs to be very precise

---

## 🏷️ Tags

`light-theme` `saas` `fintech` `dashboard-preview` `video-background` `framer-motion` `svg-chart`
