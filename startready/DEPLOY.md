# StartReady Australia — Netlify Deployment Guide

## What's in This Package

```
startready/
├── public/
│   └── index.html              ← The entire app (one file)
├── netlify/
│   └── functions/
│       └── generate-report.js  ← Secure API proxy (hides your API key)
└── netlify.toml                ← Netlify configuration
```

---

## Step 1 — Get an Anthropic API Key

1. Go to https://console.anthropic.com
2. Sign up or log in
3. Click **API Keys** in the left sidebar
4. Click **Create Key** → copy and save it somewhere safe
5. Add billing credits (the app uses Claude Sonnet — roughly $0.01–0.03 per report generated)

---

## Step 2 — Upload to GitHub

You need a free GitHub account. GitHub stores your code so Netlify can deploy it.

1. Go to https://github.com and create a free account if you don't have one
2. Click the **+** button → **New repository**
3. Name it `startready` → click **Create repository**
4. Click **uploading an existing file** on the next screen
5. Upload the entire `startready` folder (drag all files in)
   - Make sure the folder structure is preserved:
     - `public/index.html`
     - `netlify/functions/generate-report.js`
     - `netlify.toml`
6. Click **Commit changes**

---

## Step 3 — Deploy on Netlify

1. Go to https://netlify.com and create a free account
2. Click **Add new site** → **Import an existing project**
3. Click **GitHub** and authorise Netlify
4. Select your `startready` repository
5. Netlify will auto-detect the settings from `netlify.toml`:
   - **Publish directory:** `public`
   - **Functions directory:** `netlify/functions`
6. Click **Deploy site**
7. Wait ~60 seconds — your site will be live at a URL like `https://random-name-123.netlify.app`

---

## Step 4 — Add Your API Key (Critical)

This is what makes the AI report work. Your API key must be stored securely — never in the code.

1. In Netlify, go to your site dashboard
2. Click **Site configuration** → **Environment variables**
3. Click **Add a variable**
4. Set:
   - **Key:** `ANTHROPIC_API_KEY`
   - **Value:** your API key from Step 1 (starts with `sk-ant-...`)
5. Click **Save**
6. Go to **Deploys** tab → click **Trigger deploy** → **Deploy site**

Your app is now fully live and working. ✓

---

## Step 5 — Custom Domain (Optional)

1. In Netlify go to **Domain management** → **Add a domain**
2. Enter your domain (e.g. `startready.com.au`)
3. Follow the DNS instructions Netlify provides
4. Free SSL certificate is added automatically

---

## Testing the App

Once deployed, go through the quiz yourself and verify:
- Questions advance correctly
- Follow-up questions appear when triggered
- The "Generating..." screen appears after finishing
- A full AI report is generated with scores, strengths, gaps, and next steps
- Print/PDF button works
- Email button opens your mail client

---

## Costs

| Item | Cost |
|------|------|
| Netlify hosting | Free (Starter plan) |
| Custom domain | ~$20–30/year (optional) |
| Anthropic API | ~$0.01–0.03 per report |

For 100 reports/month: approximately $1–3 in API costs.

---

## Need Help?

If anything doesn't work, the most common issues are:
1. **API key not saved** — double-check Step 4 and re-deploy
2. **File structure wrong on GitHub** — make sure `netlify.toml` is at the root level
3. **Function not deploying** — check the Netlify **Functions** tab to confirm `generate-report` appears

---

*Built with StartReady Australia · Powered by Claude AI*
