# Cars24 Supply Dashboard — Vercel Deployment

## One-time setup (15 minutes)

### Step 1 — Push to GitHub
1. Create a new **private** repo on github.com (e.g. `cars24-dashboard`)
2. Upload all these files to it (drag and drop in the GitHub web UI works fine)

### Step 2 — Deploy to Vercel
1. Go to vercel.com → "Add New Project"
2. Import your GitHub repo
3. Framework preset: **Next.js** (auto-detected)
4. Click **Deploy** — first deploy takes ~2 minutes

### Step 3 — Add Vercel KV (free database)
1. In your Vercel project → **Storage** tab → **Create Database** → **KV**
2. Name it anything (e.g. `cars24-kv`) → Create
3. Vercel automatically adds the KV env vars to your project
4. Trigger a redeploy: **Deployments** → **Redeploy** on the latest

### Step 4 — Set your upload secret (optional but recommended)
1. Vercel project → **Settings** → **Environment Variables**
2. Add: `UPLOAD_SECRET` = `some-secret-only-you-know`
3. Update `API_UPLOAD_SECRET` in `public/dashboard.html` to match
4. Redeploy

---

## Daily usage

**You (data owner):**
1. Open your Vercel URL
2. Click **⬆ Upload Data** → pick your CSV/Excel export
3. Dashboard says "SYNCED — team can see this"
4. Done. Everyone with the link now sees the new data.

**Team:**
- Just open the Vercel URL. Data loads automatically.
- No upload needed. No login needed.

---

## Files in this project

```
cars24-dashboard/
├── pages/
│   ├── index.js          ← redirects to dashboard.html
│   └── api/
│       ├── upload.js     ← POST /api/upload  (you call this when uploading)
│       └── data.js       ← GET  /api/data    (team fetches from this)
├── public/
│   └── dashboard.html    ← the full dashboard (replace with new version anytime)
├── package.json
└── next.config.js
```

## Updating the dashboard
If you get a new `leadership-snapshot.html` from Claude, just replace
`public/dashboard.html` with it and push to GitHub — Vercel redeploys automatically.
