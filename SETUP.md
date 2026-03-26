# Setting Up the GitHub Repo

Step-by-step to publish this as a public open-source repo on your GitHub (@P-r-e-m-i-u-m).

---

## Step 1 — Create the repo on GitHub

1. Go to https://github.com/new
2. Repository name: `ui-prompt-library`
3. Description: `Open-source collection of production-grade UI prompts for React + Tailwind + shadcn/ui`
4. Set to **Public**
5. ❌ Do NOT initialize with README (we have our own)
6. Click **Create repository**

---

## Step 2 — Initialize locally and push

```bash
cd ui-prompt-library

git init
git add .
git commit -S -s -m "feat: initial commit - UI prompt library with 3 SaaS prompts"

git remote add origin https://github.com/P-r-e-m-i-u-m/ui-prompt-library
git branch -M main
git push -u origin main
```

---

## Step 3 — Add repo topics (for discoverability)

On your repo page → click the gear icon next to "About" → add these topics:

```
react tailwindcss shadcn-ui framer-motion prompt-engineering
ui-components landing-page saas open-source typescript
```

---

## Step 4 — Pin it on your profile

Go to your GitHub profile → click "Customize your pins" → add `ui-prompt-library`

---

## Step 5 — Share it

Post on LinkedIn:
```
Just open-sourced my UI Prompt Library 🎨

A collection of production-grade prompts for building landing pages
with React + Tailwind + shadcn/ui + Framer Motion.

Copy a prompt → paste into Claude or GPT → get a full working page.

3 prompts so far, more coming. Contributions welcome!

→ github.com/P-r-e-m-i-u-m/ui-prompt-library

#OpenSource #React #TailwindCSS #AI #Frontend
```

---

## Optional: Add a GitHub Actions CI

Create `.github/workflows/validate.yml` to check that all `.md` files have required sections:

```yaml
name: Validate Prompts
on: [push, pull_request]
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Check prompt files have required sections
        run: |
          for f in saas/*.md components/*.md; do
            if [ "$f" = "saas/README.md" ] || [ "$f" = "components/README.md" ]; then
              continue
            fi
            echo "Checking $f..."
            grep -q "## 📦 Dependencies" "$f" || (echo "MISSING Dependencies in $f" && exit 1)
            grep -q "## 🎨 Design Tokens" "$f" || (echo "MISSING Design Tokens in $f" && exit 1)
            grep -q "## 🏗️ Page Structure" "$f" || (echo "MISSING Page Structure in $f" && exit 1)
          done
          echo "All prompts valid!"
```
