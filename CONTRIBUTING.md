# Contributing to UI Prompt Library

Thanks for wanting to contribute! Every prompt added helps the whole community build faster.

---

## What Makes a Good Prompt

- **Specific** — exact Tailwind classes, HSL color values, px sizes
- **Complete** — covers every section from navbar to footer
- **Working** — tested with at least one AI (Claude or GPT)
- **Original** — your own design or a clearly credited recreation

---

## How to Submit a Prompt

### Step 1 — Fork the repo
```bash
git clone https://github.com/P-r-e-m-i-u-m/ui-prompt-library
cd ui-prompt-library
git checkout -b feat/add-[your-prompt-name]
```

### Step 2 — Copy the template
```bash
cp templates/PROMPT_TEMPLATE.md saas/your-prompt-name.md
# or components/ if it's a component
```

### Step 3 — Fill it in
Every section of the template must be filled in. See existing prompts for reference.

Minimum required:
- [ ] Stack
- [ ] Dependencies (exact npm commands)
- [ ] Design tokens (all CSS variables)
- [ ] All asset URLs
- [ ] Section-by-section spec
- [ ] Key design decisions

### Step 4 — Update the index
Add a row to [`saas/README.md`](./saas/README.md) or [`components/README.md`](./components/README.md).

### Step 5 — PR
```bash
git add .
git commit -m "feat: add [prompt name] prompt"
git push origin feat/add-[your-prompt-name]
```

Open a PR with:
- Title: `feat: add [prompt name]`
- Description: one sentence about what it builds + which AI you tested with

---

## Quality Bar

Before submitting, test your prompt by pasting it into Claude and checking:
- Does it generate runnable code?
- Are all sections present?
- Are design tokens correctly applied?

---

## What NOT to Submit

- Prompts that ask for components that require paid APIs
- Vague prompts without exact class names
- Duplicate prompts with only minor variations

---

## Credit

Your GitHub username will be added to the prompt file header and the main README contributors section after merge.
