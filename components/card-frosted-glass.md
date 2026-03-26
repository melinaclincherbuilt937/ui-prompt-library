# Card — Frosted Glass Stat / Feature Card

> **Stack:** React + TypeScript + Tailwind CSS + Framer Motion  
> **Category:** `component` `card`  
> **Difficulty:** Beginner  
> **Works with:** Any dark-theme page

---

## 📦 Dependencies

```bash
npm install framer-motion
```

---

## 🎨 Required Design Tokens

```css
:root {
  --card:             0 0% 5%;
  --card-foreground:  0 0% 100%;
  --muted-foreground: 0 0% 65%;
  --border:           0 0% 20%;
}
```

---

## 🏗️ Component Spec

### Variant A — Stat Card

```
Container:
  Background: hsl(var(--card))
  Border: border border-border/40
  Radius: rounded-2xl
  Padding: p-6
  Hover: hover:border-border/80 transition-colors duration-300
  Motion: whileHover={{ y: -4 }} transition={{ duration: 0.2 }}

Label (top):
  Style: text-xs text-muted-foreground uppercase tracking-[2px] mb-3

Value (big number):
  Style: text-4xl font-medium text-foreground mb-1

Sub-label:
  Style: text-sm text-muted-foreground
```

```tsx
import { motion } from "framer-motion"

interface StatCardProps {
  label: string
  value: string
  sublabel: string
}

export function StatCard({ label, value, sublabel }: StatCardProps) {
  return (
    <motion.div
      whileHover={{ y: -4 }}
      transition={{ duration: 0.2 }}
      className="bg-card border border-border/40 rounded-2xl p-6
                 hover:border-border/80 transition-colors duration-300"
    >
      <p className="text-xs text-muted-foreground uppercase tracking-[2px] mb-3">
        {label}
      </p>
      <p className="text-4xl font-medium text-foreground mb-1">
        {value}
      </p>
      <p className="text-sm text-muted-foreground">
        {sublabel}
      </p>
    </motion.div>
  )
}
```

**Example usage:**
```tsx
<StatCard label="Subscribers" value="7,000+" sublabel="across 40 countries" />
<StatCard label="Open Rate" value="68%" sublabel="industry avg is 21%" />
<StatCard label="Issues" value="142" sublabel="published since 2022" />
```

---

### Variant B — Feature Card (icon + title + description)

```
Container:
  Same base as Stat Card
  Layout: flex flex-col gap-4

Icon container:
  Size: w-10 h-10
  Shape: rounded-xl
  Background: hsl(var(--muted))
  Layout: flex items-center justify-center
  Icon: w-5 h-5 text-foreground/80 (lucide-react icon)

Title:
  Style: font-semibold text-base text-foreground

Description:
  Style: text-sm text-muted-foreground leading-relaxed
```

```tsx
import { motion } from "framer-motion"
import { LucideIcon } from "lucide-react"

interface FeatureCardProps {
  icon: LucideIcon
  title: string
  description: string
}

export function FeatureCard({ icon: Icon, title, description }: FeatureCardProps) {
  return (
    <motion.div
      whileHover={{ y: -4 }}
      transition={{ duration: 0.2 }}
      className="bg-card border border-border/40 rounded-2xl p-6
                 hover:border-border/80 transition-colors duration-300
                 flex flex-col gap-4"
    >
      <div className="w-10 h-10 rounded-xl bg-muted flex items-center justify-center">
        <Icon className="w-5 h-5 text-foreground/80" />
      </div>
      <div>
        <p className="font-semibold text-base text-foreground mb-1">{title}</p>
        <p className="text-sm text-muted-foreground leading-relaxed">{description}</p>
      </div>
    </motion.div>
  )
}
```

**Example usage:**
```tsx
import { Rss, PenLine, Users, Send } from "lucide-react"

<FeatureCard icon={Rss} title="Curated Feed" description="Every post hand-picked for depth and relevance." />
<FeatureCard icon={PenLine} title="Writer Tools" description="Everything you need to publish, grow, and earn." />
<FeatureCard icon={Users} title="Community" description="Connect with readers who actually care." />
<FeatureCard icon={Send} title="Distribution" description="Reach beyond your list with built-in amplification." />
```

---

### Grid layout for both variants

```tsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
  {/* cards here */}
</div>
```

---

## 💡 Key Design Decisions

- `y: -4` lift on hover gives tactile feedback without being distracting
- `border-border/40` at rest → `border-border/80` on hover — subtle border brightening instead of a glow effect
- `rounded-2xl` matches the design language of most shadcn/ui components
- No shadow — the dark background makes shadows invisible; border is the depth cue

---

## 🔧 Customisation

| Thing to change | How |
|---|---|
| Hover lift amount | Change `y: -4` |
| Add glow on hover | Add `hover:shadow-[0_0_30px_rgba(255,255,255,0.05)]` |
| Background opacity | Change `bg-card` to `bg-card/60` for more transparency |
| Border radius | Change `rounded-2xl` to `rounded-xl` or `rounded-3xl` |

---

## 🏷️ Tags

`card` `dark-theme` `framer-motion` `hover-animation` `stat` `feature-grid`
