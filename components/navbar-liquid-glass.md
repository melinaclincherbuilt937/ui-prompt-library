# Navbar — Fixed Transparent with Liquid Glass Icons

> **Stack:** React + TypeScript + Tailwind CSS + lucide-react  
> **Category:** `component` `navigation`  
> **Difficulty:** Beginner  
> **Works with:** Any dark-theme page

---

## 📦 Dependencies

```bash
npm install lucide-react
```

---

## 🎨 Required Design Tokens

This component expects these CSS variables to already be defined in your `index.css`:

```css
:root {
  --foreground:       0 0% 100%;
  --muted-foreground: 0 0% 65%;
  --background:       0 0% 0%;
}
```

---

## 🌀 Required Utility Class

Add `.liquid-glass` to your `index.css`:

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

## 🏗️ Component Spec

```
Position: fixed top-0 left-0 right-0 z-50
Background: none (fully transparent)
Padding: px-8 md:px-28 py-4
Layout: flex items-center justify-between
```

### Left — Logo

```
Layout: flex items-center gap-3

Concentric circles icon:
  Outer ring: w-7 h-7 rounded-full border-2 border-foreground/60
              flex items-center justify-center
  Inner ring: w-3 h-3 rounded-full border border-foreground/60

Brand name:
  Text: "Mindloop" (replace with your brand)
  Style: font-bold text-base text-foreground
```

```tsx
<div className="flex items-center gap-3">
  <div className="w-7 h-7 rounded-full border-2 border-foreground/60 flex items-center justify-center">
    <div className="w-3 h-3 rounded-full border border-foreground/60" />
  </div>
  <span className="font-bold text-base text-foreground">Mindloop</span>
</div>
```

---

### Center — Nav Links

```
Items: ["Home", "How It Works", "Philosophy", "Use Cases"]
         (replace with your links)
Separator: • character between each link
Color: text-muted-foreground hover:text-foreground
Transition: transition-colors duration-200
Layout: hidden md:flex items-center gap-3
```

```tsx
const links = ["Home", "How It Works", "Philosophy", "Use Cases"]

<nav className="hidden md:flex items-center gap-3">
  {links.map((link, i) => (
    <React.Fragment key={link}>
      <a
        href="#"
        className="text-sm text-muted-foreground hover:text-foreground transition-colors cursor-pointer"
      >
        {link}
      </a>
      {i < links.length - 1 && (
        <span className="text-muted-foreground/40 text-xs">•</span>
      )}
    </React.Fragment>
  ))}
</nav>
```

---

### Right — Social Icon Buttons

```
Icons: Instagram, Linkedin, Twitter (from lucide-react)
Each button:
  Size: w-10 h-10
  Shape: rounded-full
  Style: liquid-glass
  Layout: flex items-center justify-center
  Cursor: cursor-pointer
Icon size: w-4 h-4 text-foreground/80
Gap between buttons: gap-2
```

```tsx
import { Instagram, Linkedin, Twitter } from "lucide-react"

<div className="flex items-center gap-2">
  {[Instagram, Linkedin, Twitter].map((Icon, i) => (
    <button
      key={i}
      className="liquid-glass w-10 h-10 rounded-full flex items-center justify-center cursor-pointer"
    >
      <Icon className="w-4 h-4 text-foreground/80" />
    </button>
  ))}
</div>
```

---

## 💡 Key Design Decisions

- **No background at all** — the navbar is invisible until content scrolls under it, at which point the `backdrop-filter: blur` on liquid glass buttons creates a subtle depth effect
- **Dots as separators** — cleaner than `|` pipes, less visual noise than full dividers
- **Fixed + z-50** — always on top of video backgrounds and hero sections
- On mobile, nav links are `hidden md:flex` — only the logo and icons show on small screens

---

## 🔧 Customisation

| Thing to change | Where |
|---|---|
| Brand name | Replace `"Mindloop"` string |
| Nav links | Edit the `links` array |
| Social icons | Swap lucide icons |
| Icon style | Change `w-10 h-10` for size |
| Padding | Change `px-8 md:px-28` |

---

## 🏷️ Tags

`navbar` `fixed` `transparent` `liquid-glass` `dark-theme` `lucide-react`
