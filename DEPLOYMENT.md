# 🚀 Deployment Guide

## Quick Setup Options

### Option 1: GitHub Pages (Recommended for Static Hosting)
**Free, automatic deployments on every git push**

#### Steps:
1. **Push your code to GitHub** (see below)
2. **Enable GitHub Pages:**
   - Go to: https://github.com/trentbecknell/soul-lab-/settings/pages
   - Under "Source", select "GitHub Actions"
   - Click "Save"
3. **Wait for deployment** (check Actions tab)
4. **Your site will be live at:** `https://trentbecknell.github.io/soul-lab-/`

**Pros:** Free, automatic, great for static sites
**Cons:** Public only, no server-side processing

---

### Option 2: Railway (For Full App Hosting)
**Easy deployment with custom domains**

#### Steps:
1. **Install Railway CLI** (optional):
   ```bash
   npm install -g @railway/cli
   ```

2. **Deploy via GitHub:**
   - Go to: https://railway.app
   - Click "New Project" → "Deploy from GitHub repo"
   - Select `trentbecknell/soul-lab-`
   - Railway will auto-detect settings from `railway.json`

3. **Or deploy via CLI:**
   ```bash
   railway login
   railway init
   railway up
   ```

4. **Get your URL:**
   - Railway provides: `soul-lab-production.up.railway.app`
   - Or add custom domain in Railway dashboard

**Pros:** Custom domains, environment variables, server capabilities
**Cons:** Free tier limits (500 hours/month)

---

## Git Commands to Push Code

```bash
# Add all files
git add .

# Commit changes
git commit -m "Initial Soul Lab deployment with Detroit Dough samples"

# Push to GitHub
git push origin main
```

After pushing, GitHub Actions will automatically deploy to GitHub Pages!

---

## File Structure for Deployment

```
soul-lab-/
├── index.html              # Main app
├── downloads/for app/      # Drum samples (will be deployed)
├── package.json            # Metadata
├── Procfile                # Railway start command
├── railway.json            # Railway config
├── runtime.txt             # Python version
└── .github/
    └── workflows/
        └── deploy.yml      # GitHub Actions deployment
```

---

## Updating After Deployment

**GitHub Pages:**
```bash
# Make changes to code
git add .
git commit -m "Update: added new feature"
git push origin main
# GitHub Actions auto-deploys in ~1 minute
```

**Railway:**
- Automatically redeploys on git push
- Or use: `railway up` for immediate deploy

---

## Testing Deployments

### GitHub Pages
- **Check build status:** https://github.com/trentbecknell/soul-lab-/actions
- **View site:** https://trentbecknell.github.io/soul-lab-/
- **Takes:** ~1-2 minutes after push

### Railway
- **Check logs:** Railway dashboard → Deployments
- **View site:** Your Railway URL
- **Takes:** ~2-3 minutes for first deploy, <1 min for updates

---

## Troubleshooting

### GitHub Pages Not Working?
1. Check Settings → Pages → Source is "GitHub Actions"
2. Check Actions tab for failed builds
3. Make sure `index.html` is in root directory ✅

### Railway Not Working?
1. Check Procfile has correct start command
2. Verify $PORT environment variable is used
3. Check Railway logs for errors

### Samples Not Loading?
- Make sure `downloads/for app/` folder is committed to git
- Check browser console for 404 errors
- Verify file paths are relative (not absolute)

---

## Custom Domain Setup

### GitHub Pages
1. Go to Settings → Pages
2. Add custom domain (e.g., `soullab.music`)
3. Configure DNS:
   - Add CNAME record pointing to `trentbecknell.github.io`

### Railway
1. Go to project Settings → Domains
2. Click "Add Domain"
3. Follow DNS configuration steps

---

## Environment Variables (Railway Only)

If you need to add secrets:
```bash
railway variables set API_KEY=your_key_here
```

---

## Which Should You Use?

**Use GitHub Pages if:**
- ✅ You want free hosting
- ✅ Your app is purely static (HTML/CSS/JS)
- ✅ You're okay with public repos

**Use Railway if:**
- ✅ You need server-side features
- ✅ You want custom domains easily
- ✅ You need environment variables
- ✅ You want private repos

**Use Both:**
- GitHub Pages for main site
- Railway for API/backend if needed later

---

## Next Steps

1. **Choose your platform** (GitHub Pages recommended to start)
2. **Run git commands** (see above)
3. **Enable deployment** (GitHub Pages settings or Railway connect)
4. **Share your live link!** 🎵

Your live site will be at:
- **GitHub Pages:** `https://trentbecknell.github.io/soul-lab-/`
- **Railway:** `https://soul-lab-production.up.railway.app/` (or custom)

**Ready to deploy? Run the git commands above!**
