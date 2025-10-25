# GitHub Pages Deployment Guide

A practical, step-by-step guide to publishing your website using GitHub Pages — from creating your first repo to deploying live on the web.

---

## Table of Contents
1. [What is GitHub Pages?](#what-is-github-pages)
2. [Quick Start: Zero to Published Site](#quick-start-zero-to-published-site)
3. [Repository Setup and Structure](#repository-setup-and-structure)
4. [Enabling GitHub Pages](#enabling-github-pages)
5. [Automatic Builds from Main Branch](#automatic-builds-from-main-branch)
6. [Custom Domain Configuration](#custom-domain-configuration)
7. [Using Frameworks (Next.js, Astro, etc.)](#using-frameworks-nextjs-astro-etc)
8. [Version Control & Team Collaboration](#version-control--team-collaboration)
9. [Troubleshooting Common Issues](#troubleshooting-common-issues)

---

## What is GitHub Pages?

GitHub Pages is a free static site hosting service that takes HTML, CSS, and JavaScript files directly from a GitHub repository and publishes them as a website. Perfect for:
- Personal portfolios
- Project documentation
- Simple landing pages
- Static blogs
- Prototypes and demos

**Key benefits:**
- ✅ Free hosting with SSL
- ✅ Automatic deployment from your repo
- ✅ Custom domain support
- ✅ Version controlled deployment

---

## Quick Start: Zero to Published Site

### Prerequisites
- A GitHub account ([Sign up here](https://github.com/join))
- Basic familiarity with HTML/CSS
- Git installed locally (optional, but recommended)

### The Fastest Path (5 minutes)

1. **Create a new repository** on GitHub
   - Click the `+` icon in the top right → "New repository"
   - Name it: `my-website` (or `<username>.github.io` for a personal site)
   - Make it Public
   - Check "Add a README file"
   - Click "Create repository"

2. **Add an `index.html` file**
   - Click "Add file" → "Create new file"
   - Name it `index.html`
   - Paste this starter code:
   
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>My GitHub Pages Site</title>
       <style>
           body {
               font-family: system-ui, -apple-system, sans-serif;
               max-width: 800px;
               margin: 50px auto;
               padding: 20px;
               line-height: 1.6;
           }
           h1 { color: #2c3e50; }
       </style>
   </head>
   <body>
       <h1>Welcome to My Website!</h1>
       <p>This site is hosted on GitHub Pages.</p>
   </body>
   </html>
   ```
   
   - Commit directly to `main` branch

3. **Enable GitHub Pages**
   - Go to repository Settings → Pages (in the left sidebar)
   - Under "Source", select `Deploy from a branch`
   - Select branch: `main` and folder: `/ (root)`
   - Click Save

4. **Visit your site!**
   - Your site will be live at: `https://<username>.github.io/<repository-name>/`
   - It may take 1-2 minutes for the first deployment

---

## Repository Setup and Structure

### Recommended Project Structure

Here's a clean, organized structure for your GitHub Pages site:

```
my-website/
├── index.html              # Homepage (required)
├── about.html              # Other pages
├── contact.html
├── assets/                 # Assets directory
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── main.js
│   └── images/
│       ├── logo.png
│       └── hero.jpg
├── docs/                   # Documentation (optional)
│   └── guide.md
├── README.md               # Project description
└── .gitignore              # Files to ignore
```

### Important Files

#### `index.html` (Required)
This is your homepage. GitHub Pages looks for this file at your site's root.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Portfolio</title>
    <link rel="stylesheet" href="assets/css/style.css">
</head>
<body>
    <nav>
        <a href="index.html">Home</a>
        <a href="about.html">About</a>
        <a href="contact.html">Contact</a>
    </nav>
    <main>
        <h1>Welcome!</h1>
        <p>Your content here...</p>
    </main>
    <script src="assets/js/main.js"></script>
</body>
</html>
```

#### `.gitignore` (Recommended)
Exclude files you don't want to deploy:

```gitignore
# OS files
.DS_Store
Thumbs.db

# IDE files
.vscode/
.idea/

# Development files
node_modules/
.env
*.log

# Build artifacts (if using a framework)
.next/
.cache/
dist/
```

#### `README.md` (Best Practice)
Describe your project so visitors to your repo understand what it's about:

```markdown
# My Portfolio Website

A personal portfolio showcasing my web development projects.

**Live Site:** https://username.github.io/my-website/

## Features
- Responsive design
- Project gallery
- Contact form

## Local Development
1. Clone the repo: `git clone https://github.com/username/my-website.git`
2. Open `index.html` in your browser
```

---

## Enabling GitHub Pages

### Method 1: From a Branch (Recommended for Simple Sites)

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under **Source**, select:
   - Branch: `main`
   - Folder: `/ (root)` or `/docs` (if your HTML is in a docs folder)
4. Click **Save**
5. Your site will be published to `https://<username>.github.io/<repo-name>/`

### Method 2: GitHub Actions (For Custom Builds)

For more control (e.g., using build tools), use GitHub Actions. Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

Then in **Settings → Pages**, set Source to "GitHub Actions".

---

## Automatic Builds from Main Branch

GitHub Pages automatically rebuilds your site when you push to the configured branch (usually `main`).

### How It Works

```
Developer pushes to main
         ↓
GitHub detects changes
         ↓
Builds site automatically
         ↓
Deploys to GitHub Pages
         ↓
Site is live! 🎉
```

### Viewing Build Status

1. Go to your repository
2. Click the **Actions** tab
3. You'll see "pages build and deployment" workflows
4. Click on any run to see details and logs

### Triggering a Rebuild

If your site isn't updating:
- Make a small change (e.g., add a space to README)
- Commit and push to `main`
- Or use **Actions** tab → "pages build and deployment" → "Re-run jobs"

---

## Custom Domain Configuration

Want your site at `www.yourname.com` instead of `username.github.io`?

### Step 1: Purchase a Domain

Buy a domain from:
- [Namecheap](https://www.namecheap.com)
- [Google Domains](https://domains.google)
- [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/)

### Step 2: Configure DNS

In your domain registrar's DNS settings, add these records:

**For apex domain (`yourname.com`):**
```
Type: A
Name: @
Value: 185.199.108.153

Type: A
Name: @
Value: 185.199.109.153

Type: A
Name: @
Value: 185.199.110.153

Type: A
Name: @
Value: 185.199.111.153
```

**For subdomain (`www.yourname.com`):**
```
Type: CNAME
Name: www
Value: <username>.github.io
```

### Step 3: Configure on GitHub

1. Go to **Settings → Pages**
2. Under **Custom domain**, enter: `www.yourname.com`
3. Click **Save**
4. Wait for DNS check (can take up to 24 hours)
5. Once verified, check **Enforce HTTPS**

### Step 4: Add CNAME File (Automatic)

GitHub will create a `CNAME` file in your repo automatically. If you need to create it manually:

```
www.yourname.com
```

**Pro Tip:** DNS propagation can take 24-48 hours. Use [DNS Checker](https://dnschecker.org) to monitor progress.

---

## Using Frameworks (Next.js, Astro, etc.)

GitHub Pages supports static sites. Here's how to deploy sites built with modern frameworks:

### Next.js Static Export

1. **Configure `next.config.js`:**
   ```javascript
   /** @type {import('next').NextConfig} */
   const nextConfig = {
     output: 'export',
     basePath: '/your-repo-name', // Only if not using custom domain
     images: {
       unoptimized: true,
     },
   }
   
   module.exports = nextConfig
   ```

2. **Build your site:**
   ```bash
   npm run build
   ```
   This creates an `out/` directory with static files.

3. **Create `.github/workflows/nextjs.yml`:**
   ```yaml
   name: Deploy Next.js to GitHub Pages

   on:
     push:
       branches: [ main ]

   permissions:
     contents: read
     pages: write
     id-token: write

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         
         - name: Setup Node.js
           uses: actions/setup-node@v4
           with:
             node-version: '20'
             cache: 'npm'
         
         - name: Install dependencies
           run: npm ci
         
         - name: Build
           run: npm run build
         
         - name: Setup Pages
           uses: actions/configure-pages@v4
         
         - name: Upload artifact
           uses: actions/upload-pages-artifact@v3
           with:
             path: ./out
         
         - name: Deploy to GitHub Pages
           uses: actions/deploy-pages@v4
   ```

### Astro

Astro has excellent GitHub Pages support built-in!

1. **Configure `astro.config.mjs`:**
   ```javascript
   import { defineConfig } from 'astro/config';

   export default defineConfig({
     site: 'https://username.github.io',
     base: '/your-repo-name', // Remove if using custom domain
   });
   ```

2. **Use the official GitHub Action:**
   Create `.github/workflows/deploy.yml`:
   ```yaml
   name: Deploy Astro to GitHub Pages

   on:
     push:
       branches: [ main ]

   permissions:
     contents: read
     pages: write
     id-token: write

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout
           uses: actions/checkout@v4
         
         - name: Setup Node
           uses: actions/setup-node@v4
           with:
             node-version: 20
         
         - name: Install dependencies
           run: npm ci
         
         - name: Build
           run: npm run build
         
         - name: Upload Pages artifact
           uses: actions/upload-pages-artifact@v3
           with:
             path: dist
     
     deploy:
       needs: build
       runs-on: ubuntu-latest
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       steps:
         - name: Deploy to GitHub Pages
           id: deployment
           uses: actions/deploy-pages@v4
   ```

### Other Static Site Generators

**Jekyll** (Ruby): Supported by default, no config needed!
**Hugo** (Go): Build to `public/`, deploy that folder
**Gatsby** (React): Build to `public/`, similar to Next.js
**VuePress** (Vue): Build to `docs/.vuepress/dist/`

**General Pattern:**
1. Configure your framework to output static HTML/CSS/JS
2. Set the correct `basePath` for your repo name
3. Use GitHub Actions to build and deploy the output directory

---

## Version Control & Team Collaboration

### Working with Interns and Team Members

#### 1. Branch Protection Rules

Protect your `main` branch to prevent accidental overwrites:

1. Go to **Settings → Branches**
2. Click **Add rule**
3. Branch name pattern: `main`
4. Enable:
   - ✅ Require a pull request before merging
   - ✅ Require approvals (1+)
   - ✅ Dismiss stale pull request approvals when new commits are pushed

#### 2. Collaborative Workflow

**For Team Members:**

```bash
# Clone the repository
git clone https://github.com/username/project.git
cd project

# Create a feature branch
git checkout -b feature/add-about-page

# Make changes to files
# ... edit index.html, add about.html ...

# Stage and commit changes
git add .
git commit -m "Add about page with team bios"

# Push to GitHub
git push origin feature/add-about-page

# Open a pull request on GitHub
# Get it reviewed and merge
```

**For Interns (Simplified):**

```bash
# 1. Fork the repository on GitHub (click Fork button)
# 2. Clone YOUR fork
git clone https://github.com/YOUR-USERNAME/project.git

# 3. Make changes
# ... edit files ...

# 4. Commit and push
git add .
git commit -m "Update homepage hero section"
git push origin main

# 5. Create Pull Request from your fork to original repo
```

#### 3. Issue and Project Management

Use GitHub Issues to organize work:

```markdown
**Issue Title:** Add contact form to website

**Description:**
Create a functional contact form on the contact.html page.

**Requirements:**
- [ ] Name field
- [ ] Email field (with validation)
- [ ] Message textarea
- [ ] Submit button
- [ ] Form submission handling

**Assignee:** @intern-username
**Labels:** enhancement, good first issue
```

#### 4. Code Review Best Practices

When reviewing pull requests:
- ✅ Check HTML is valid (use [W3C Validator](https://validator.w3.org/))
- ✅ Test responsive design
- ✅ Verify links work
- ✅ Check for accessibility (alt text, semantic HTML)
- ✅ Review commit messages are clear

#### 5. Keeping Forks in Sync

If team members forked the repo:

```bash
# Add original repo as "upstream"
git remote add upstream https://github.com/original-owner/project.git

# Fetch latest changes
git fetch upstream

# Merge into your main branch
git checkout main
git merge upstream/main

# Push to your fork
git push origin main
```

---

## Troubleshooting Common Issues

### Site Not Updating

**Problem:** You pushed changes but the site still shows old content.

**Solutions:**
1. **Clear browser cache:** Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
2. **Check Actions tab:** Look for failed deployments
3. **Verify branch:** Settings → Pages, ensure correct branch is selected
4. **Wait:** Initial deployments can take 10 minutes

### 404 Page Not Found

**Problem:** Visiting your site shows "404 - File not found"

**Solutions:**
1. **Check file name:** Must be `index.html` (lowercase)
2. **Check location:** Should be in root or `/docs` depending on settings
3. **Verify Pages is enabled:** Settings → Pages should show your site URL
4. **Check branch:** Make sure you're pushing to the correct branch

### Broken Links and Images

**Problem:** Internal links or images don't load.

**Solutions:**
1. **Use relative paths:**
   ```html
   <!-- ✅ Good -->
   <img src="assets/images/logo.png" alt="Logo">
   <a href="about.html">About</a>
   
   <!-- ❌ Bad (absolute paths) -->
   <img src="/assets/images/logo.png" alt="Logo">
   ```

2. **If using a repo name (not custom domain):**
   ```html
   <!-- Add base tag in <head> -->
   <base href="/your-repo-name/">
   
   <!-- Or use Jekyll/framework features to handle basePath -->
   ```

### CSS/JS Not Loading

**Problem:** Styles or scripts don't apply.

**Solutions:**
1. **Check paths in HTML:**
   ```html
   <!-- ✅ Relative path -->
   <link rel="stylesheet" href="assets/css/style.css">
   
   <!-- ❌ Absolute path (won't work with repo name) -->
   <link rel="stylesheet" href="/assets/css/style.css">
   ```

2. **Verify file names match:** Linux servers are case-sensitive
   - `Style.css` ≠ `style.css`

3. **Check browser console:** F12 → Console tab for errors

### Custom Domain Not Working

**Problem:** Custom domain shows 404 or doesn't resolve.

**Solutions:**
1. **Verify DNS records:** Use [DNS Checker](https://dnschecker.org)
2. **Wait for propagation:** Can take up to 48 hours
3. **Check CNAME file:** Should contain only your domain name
4. **Ensure HTTPS:** Uncheck/recheck "Enforce HTTPS" after DNS propagates

### Build Failures with GitHub Actions

**Problem:** Action workflow fails.

**Solutions:**
1. **Check workflow logs:** Actions tab → Click failed run
2. **Common issues:**
   - Missing `package.json` dependencies
   - Wrong Node.js version
   - Incorrect build script
3. **Test locally first:**
   ```bash
   npm install
   npm run build
   # If this works, your Action should too
   ```

---

## Quick Reference Commands

```bash
# Clone a repository
git clone https://github.com/username/repo.git

# Check status
git status

# Stage all changes
git add .

# Commit changes
git commit -m "Your descriptive message"

# Push to GitHub (triggers deployment)
git push origin main

# Create a new branch
git checkout -b feature-name

# Switch branches
git checkout main

# Pull latest changes
git pull origin main

# View deployment URL
# Settings → Pages → Your site is live at...
```

---

## Additional Resources

- **GitHub Pages Docs:** https://docs.github.com/en/pages
- **GitHub Actions Docs:** https://docs.github.com/en/actions
- **W3C HTML Validator:** https://validator.w3.org/
- **Free Images:** [Unsplash](https://unsplash.com), [Pexels](https://pexels.com)
- **Icons:** [Font Awesome](https://fontawesome.com), [Heroicons](https://heroicons.com)
- **Learning Resources:**
  - [MDN Web Docs](https://developer.mozilla.org/)
  - [freeCodeCamp](https://www.freecodecamp.org/)
  - [Web.dev](https://web.dev/)

---

## Need Help?

- **GitHub Community:** https://github.community/
- **Stack Overflow:** Tag questions with `github-pages`
- **Repository Issues:** Open an issue in your repo for team discussion

---

**Last Updated:** October 2025

Happy deploying! 🚀
