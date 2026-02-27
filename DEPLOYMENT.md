# Deploying Attune Website to GitHub

Your project is now ready to be hosted on GitHub. Follow these steps:

## Step 1: Create a GitHub Repository

1. Go to [GitHub.com](https://github.com) and sign in
2. Click the **+** icon in the top-right corner and select **New repository**
3. Name it: `attune-website` (or your preferred name)
4. Add description: "The first pre-prosthetic EMG training platform"
5. Choose **Public** (so it's accessible)
6. **Do NOT** initialize with README, .gitignore, or license (we already have these)
7. Click **Create repository**

## Step 2: Push to GitHub

In your terminal, run these commands from the project root:

```bash
cd "/Users/ashleyyang/Downloads/attune-website (1)"

# Add the remote repository
git remote add origin https://github.com/YOUR_USERNAME/attune-website.git

# Rename branch to main (optional but recommended)
git branch -m master main

# Push to GitHub
git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.

## Step 3: Deploy with GitHub Pages

### Option A: Deploy Static Build (Recommended for Production)

1. Install `gh-pages` package:
```bash
npm install --save-dev gh-pages
```

2. Update `package.json` scripts:
```json
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d dist/public",
  "build": "vite build",
  "dev": "vite"
}
```

3. Update `vite.config.ts` to set the base path:
```typescript
export default defineConfig({
  base: '/attune-website/',  // Add this line
  // ... rest of config
})
```

4. Deploy:
```bash
npm run deploy
```

5. In GitHub, go to **Settings → Pages** and select:
   - Source: **Deploy from a branch**
   - Branch: **gh-pages**
   - Folder: **/(root)**

Your site will be live at: `https://YOUR_USERNAME.github.io/attune-website/`

### Option B: Deploy with Vercel (Easier, Recommended)

1. Go to [Vercel.com](https://vercel.com) and sign in with GitHub
2. Click "New Project"
3. Import your GitHub repository
4. Vercel will auto-detect it's a Vite project
5. Keep default settings and click "Deploy"

Your site will be live at a unique Vercel URL (much cleaner than GitHub Pages).

### Option C: Deploy with Netlify

1. Go to [Netlify.com](https://netlify.com) and sign in with GitHub
2. Click "New site from Git"
3. Select your repository
4. Build command: `npm run build`
5. Publish directory: `dist/public`
6. Click "Deploy"

Your site will be live at a Netlify URL.

## Making Updates

After deploying, any future changes:

```bash
# Make your changes, then:
git add -A
git commit -m "Your change description"
git push origin main

# For GitHub Pages built with gh-pages:
npm run deploy

# For Vercel/Netlify: They auto-deploy on push!
```

## Recommended Deployment

For the Attune website, I recommend **Vercel** because:
- ✅ Automatic previews for pull requests
- ✅ Serverless functions (future-proof if you add a backend)
- ✅ Automatic HTTPS
- ✅ Fast CDN globally
- ✅ Free tier is generous
- ✅ Cleaner custom domain setup

All three options are free and easy to set up!
