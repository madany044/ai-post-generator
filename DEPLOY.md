# PostCraft AI — Deployment Guide
## Deploy with your own API key (viewers need no key)

---

## Your final folder structure

```
postcraft/
├── index.html                  ← main app (frontend)
├── netlify.toml                ← netlify config
├── .gitignore                  ← keeps .env out of GitHub
└── netlify/
    └── functions/
        └── generate.js         ← serverless proxy (holds your key)
```

---

## Step 1 — Push to GitHub (private repo)

Your repo is already private. Just make sure all these files are in it.

```bash
# If starting fresh
git init
git add .
git commit -m "PostCraft AI - initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main

# If repo already exists, just add new files
git add .
git commit -m "Add Netlify function and config"
git push
```

Your API key is NOT in any of these files — it is safe to push.

---

## Step 2 — Connect repo to Netlify

1. Go to https://netlify.com and sign up free (use GitHub login)
2. Click "Add new site" → "Import an existing project"
3. Choose GitHub → select your postcraft repo
4. Build settings (leave as default — netlify.toml handles it):
   - Build command: (leave empty)
   - Publish directory: .
5. Click "Deploy site"

---

## Step 3 — Add your Gemini API key in Netlify

This is the important step — key lives here, never in code.

1. In Netlify dashboard → your site → "Site configuration"
2. Click "Environment variables" in the left menu
3. Click "Add a variable"
4. Key:   GEMINI_API_KEY
5. Value: AIzaSy... (paste your full Gemini key)
6. Click "Save"
7. Go to "Deploys" → click "Trigger deploy" → "Deploy site"

Your key is now server-side only. Nobody can see it — not in GitHub, not in browser source.

---

## Step 4 — Get your live link

After deploy (takes ~1 minute):
- Netlify gives you a URL like: https://wonderful-fox-123.netlify.app
- You can rename it: Site configuration → Domain management → change site name
- Example: https://postcraft-ai.netlify.app

Share this link. Viewers can use the app fully — no API key needed on their end.

---

## How it works (for your LinkedIn post / interview)

```
Viewer opens your link
       ↓
Browser (index.html) sends prompt to /.netlify/functions/generate
       ↓
Netlify Function (generate.js) adds your secret key + calls Gemini API
       ↓
Gemini returns generated posts
       ↓
Browser displays results
```

Your key never touches the browser. The viewer never sees it.

---

## To update the app later

Just push to GitHub — Netlify auto-redeploys.

```bash
# Make your changes to index.html, then:
git add .
git commit -m "Update app"
git push
# Netlify detects push and redeploys automatically
```

---

## Gemini Free Tier Limits (with your key)

- 10 requests per minute
- 250 requests per day
- Cost: Rs.0

For a demo this is more than enough. If many people use it, you can upgrade Gemini to paid (~Rs.0.02 per generation) or add a simple request counter.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| "API key not configured on server" | Check Netlify env variable is named exactly GEMINI_API_KEY |
| "Function not found" | Check netlify/functions/generate.js path is correct |
| App loads but generate fails | Trigger a fresh deploy after adding env variable |
| Want custom domain | Netlify → Domain management → add your domain |

---

## Summary of what each file does

| File | Purpose |
|---|---|
| index.html | The full app UI — calls /api/generate |
| netlify/functions/generate.js | Serverless function — holds key, calls Gemini |
| netlify.toml | Tells Netlify where files are |
| .gitignore | Prevents .env from being pushed to GitHub |
