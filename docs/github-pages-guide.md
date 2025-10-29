# Complete GitHub Pages Deployment Guide

This guide walks through the full process of deploying a static website, configuring a custom domain, and setting up automated Continuous Deployment (CD).

## Table of Contents

- [Quick Start](#quick-start-checklist)
- [Understanding Internal vs. External Pages](#understanding-internal-vs-external-pages)
- [Initial Setup and Deployment](#1-initial-setup-and-deployment-from-repository-to-live-site)
- [Connecting a Custom Domain](#2-connecting-a-custom-domain-using-warbotapp-or-any-domain)
- [Configuring Your Domain with Namecheap](#configuring-your-domain-with-namecheap)
- [Automation and CI/CD](#3-automation-and-continuous-deployment-cicd)
- [Backup and Recovery](#backup-and-recovery)
- [Best Practices and Tips](#4-best-practices-and-tips)
- [Advanced Configuration](#5-advanced-configuration)
- [Troubleshooting](#troubleshooting-faq)
- [Glossary](#glossary)
- [Resources](#additional-resources)

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

## Understanding Internal vs. External Pages

GitHub Pages offers two types of websites, and understanding the difference is crucial for choosing the right setup for your needs.

### 🏠 User/Organization Pages (External Pages)

**Think of this as your "main website"** - it's hosted at the root of your GitHub Pages domain.

**What it is:**
- Your primary website that lives at `https://username.github.io`
- **One per GitHub account** (like having one main address)
- Perfect for personal portfolios, company homepages, or your main web presence

**How to create it:**
1. Create a repository named exactly `username.github.io` (replace "username" with your GitHub username)
2. Add your website files to this repository
3. Enable GitHub Pages
4. Your site will be live at `https://username.github.io`

**Example:**
```
Repository name: johndoe.github.io
Live website: https://johndoe.github.io
```

**When to use:**
- ✅ Your main personal website
- ✅ Company homepage
- ✅ When you want a clean, professional URL
- ✅ Your primary web presence

### 📁 Project Pages (Internal Pages)

**Think of this as "project-specific websites"** - they live in subdirectories of your main domain.

**What it is:**
- Individual websites for specific projects
- Hosted at `https://username.github.io/project-name/`
- **Unlimited per account** (you can have many project sites)
- Perfect for project documentation, demos, or multiple websites

**How to create it:**
1. Create a repository with any name (e.g., `my-portfolio`, `project-docs`)
2. Add your website files to this repository
3. Enable GitHub Pages
4. Your site will be live at `https://username.github.io/project-name/`

**Example:**
```
Repository name: my-portfolio
Live website: https://johndoe.github.io/my-portfolio/
```

**When to use:**
- ✅ Project documentation
- ✅ Demo websites for specific projects
- ✅ Multiple websites under one account
- ✅ Testing new designs or ideas

### 📊 Quick Comparison

| Feature | User/Organization Pages | Project Pages |
|---------|------------------------|---------------|
| **URL** | `username.github.io` | `username.github.io/project-name/` |
| **Repository Name** | Must be `username.github.io` | Any name you choose |
| **How Many?** | One per account | Unlimited |
| **Best For** | Main website | Project sites |
| **URL Cleanliness** | Very clean | Includes project name |

### 🎯 Which One Should You Choose?

**Choose User/Organization Pages if:**
- This is your main website
- You want the cleanest possible URL
- You're building a personal portfolio or company site
- You want `username.github.io` as your web address

**Choose Project Pages if:**
- You're documenting a specific project
- You want multiple websites
- You're experimenting with different designs
- You don't mind having `/project-name/` in your URL

### 💡 Pro Tip: You Can Have Both!

Many developers use both types:
- **User Page** (`username.github.io`) - Their main portfolio/homepage
- **Project Pages** (`username.github.io/project1/`, `username.github.io/project2/`) - Individual project sites

This gives you the best of both worlds!

### 🔧 Important: Path Differences

**Project Pages** live in a subdirectory, so you need to be careful with file paths:

```html
<!-- ❌ Won't work on Project Pages -->
<link rel="stylesheet" href="/style.css">
<img src="/images/logo.png" alt="Logo">

<!-- ✅ Works everywhere -->
<link rel="stylesheet" href="style.css">
<img src="images/logo.png" alt="Logo">
```

**The key:** Always use relative paths (without the leading `/`) for images, CSS, and links.

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
=======
# Complete GitHub Pages Deployment Guide

This guide walks through the full process of deploying a static website, configuring a custom domain, and setting up automated Continuous Deployment (CD).

## Table of Contents

- [Quick Start](#quick-start-checklist)
- [Initial Setup and Deployment](#1-initial-setup-and-deployment-from-repository-to-live-site)
- [Connecting a Custom Domain](#2-connecting-a-custom-domain-using-warbotapp-or-any-domain)
- [Automation and CI/CD](#3-automation-and-continuous-deployment-cicd)
- [Best Practices and Tips](#4-best-practices-and-tips)
- [Advanced Configuration](#5-advanced-configuration)
- [Troubleshooting](#troubleshooting-faq)
- [Glossary](#glossary)
- [Resources](#additional-resources)

---

## 🏗️ Understanding the Architecture

**How Everything Connects:**

```
┌──────────────────────────────────────────────────────────────┐
│                      Your Computer                            │
│                                                              │
│  ┌──────────────────┐                                       │
│  │  HTML/CSS Files  │  Edit & Test Locally                  │
│  │  - index.html    │                                       │
│  │  - resume.html   │  Preview at: http://localhost:8000  │
│  └─────────┬────────┘                                       │
└────────────┼────────────────────────────────────────────────┘
             │
             │ git push
             ↓
┌──────────────────────────────────────────────────────────────┐
│                    GitHub Repository                         │
│                                                              │
│  ┌────────────────────────────────────┐                    │
│  │  Your Code Stored Here            │                    │
│  │  - All HTML files                 │                    │
│  │  - GitHub Actions workflow        │                    │
│  └────────────────┬───────────────────┘                    │
└───────────────────┼────────────────────────────────────────┘
                    │
                    │ Auto-deploy
                    ↓
┌──────────────────────────────────────────────────────────────┐
│                  GitHub Pages (Hosting)                      │
│                                                              │
│  Live Site: https://yourname.github.io/html-practice-resume │
│  ┌────────────────────────────────────┐                    │
│  │  Browser Request                   │                    │
│  │  ↓                                 │                    │
│  │  GitHub Pages Server               │                    │
│  │  ↓                                 │                    │
│  │  Returns HTML/CSS files           │                    │
│  │  ↓                                 │                    │
│  │  User's Browser (Live Site)        │                    │
│  └────────────────────────────────────┘                    │
└──────────────────────────────────────────────────────────────┘
                    │
                    │ Optional: Custom Domain
                    ↓
┌──────────────────────────────────────────────────────────────┐
│                    Your Domain (e.g., warbot.app)           │
│                                                              │
│  DNS Points → GitHub Pages                                   │
│  https://warbot.app → https://yourname.github.io/...       │
└──────────────────────────────────────────────────────────────┘
```

> 💡 **Flow**: Edit Code → Push to GitHub → GitHub Actions Deploys → Live on GitHub Pages → Optional: Custom Domain Points to GitHub

---

## 📸 Adding Screenshots to This Guide

Throughout this guide, you'll see `📸 Screenshot Placeholder` notes. To make this guide complete with visual aids:

**How to Add Screenshots:**

1. **Take screenshots** at each marked location
2. **Save them** in a `docs/images/` folder in your repository
3. **Replace the placeholders** with Markdown image syntax:

```markdown
![Description of the image](./images/screenshot-name.png)
```

**Example Structure:**
```
docs/
├── github-pages-guide.md
└── images/
    ├── github-pages-settings.png
    ├── dns-records.png
    ├── github-actions-workflow.png
    └── deployment-success.png
```

> 💡 **Tip**: Use descriptive filenames like `github-pages-settings.png` for easy identification!

---

## Quick Start Checklist

Follow this checklist to get your site live in under 30 minutes:

- [ ] **5 min**: Ensure your main HTML file is named `index.html`
- [ ] **5 min**: Enable GitHub Pages in repository settings
- [ ] **5 min**: Verify site is live at `https://YOUR_USERNAME.github.io/html-practice-resume`
- [ ] **5 min**: Add GitHub Actions workflow for automated deployment
- [ ] **5 min**: Test deployment by making a small change
- [ ] **Optional**: Configure custom domain (adds 24-48 hours for DNS)

**Estimated Total Time**: 25-30 minutes for basic deployment

**Your Deployment Journey:**
```
┌──────────────────────────────────────────────────────────────┐
│  Phase 1: Setup (5 min)           Phase 2: Configure (5 min) │
│  ✓ Create index.html             ✓ Enable GitHub Pages       │
│  ✓ Check file structure          ✓ Select branch/folder      │
│                                   ✓ First deployment          │
└──────────────────────────────────────────────────────────────┘
         ↓                                   ↓
┌──────────────────────────────────────────────────────────────┐
│  Phase 3: Test (5 min)            Phase 4: Automate (5 min) │
│  ✓ Verify site is live            ✓ Add .github/workflows/  │
│  ✓ Test local preview             ✓ Create deploy.yml        │
│  ✓ Check all links                ✓ Enable GitHub Actions   │
└──────────────────────────────────────────────────────────────┘
         ↓                                   ↓
┌──────────────────────────────────────────────────────────────┐
│  Phase 5: Enhance (10 min)        Phase 6: Custom Domain     │
│  ✓ Add SEO tags                   ✓ Configure DNS            │
│  ✓ Add analytics (optional)       ✓ Connect domain           │
│  ✓ Optimize performance           ✓ Wait for SSL cert        │
└──────────────────────────────────────────────────────────────┘
         ↓
    🎉 LIVE SITE! 🎉
```

---

## 1. Initial Setup and Deployment (From Repository to Live Site)

### Step 1: Prepare Your Repository

1. **Ensure your repository is public or has GitHub Pages enabled**
   - Go to your repository on GitHub
   - Navigate to **Settings** → **Pages**
   - Under "Source", select which branch contains your site files
   - Typically, you'll choose:
     - `main` branch for the root directory
     - `main` branch with `/docs` folder
     - Or a dedicated `gh-pages` branch

2. **Verify your file structure**

**Ideal Structure for GitHub Pages:**
```
html-practice-resume/
│
├── index.html          ◄── Main page (required!)
├── resume.html         ◄── Your resume
├── other-files.html    ◄── Additional pages
├── feature-card.html
├── pricing-page.html
├── README.md
└── .github/
    └── workflows/
        └── deploy.yml
```

> 💡 **Tip**: If your main file is `resume.html`, rename it to `index.html` so it loads automatically as the homepage.

### Step 2: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click on **Settings** tab
3. Scroll down to **Pages** in the left sidebar

> 📸 **Screenshot Placeholder**: *Insert image showing the GitHub Pages settings page with Settings → Pages highlighted*

4. Under **Source**, select:
   - **Branch**: `main` (or `master` if that's your default)
   - **Folder**: `/ (root)` 
5. Click **Save**

**Visual Guide - GitHub Pages Settings:**
```
┌─────────────────────────────────────────────────┐
│ Your Repository Name                              │
│ Code | Issues | Pull requests | ... | Settings  │
├─────────────────────────────────────────────────┤
│                    GitHub                        │
│                                                   │
│  Settings          Pages                          │
│  ├─ General                                     │
│  ├─ Pages     ◄─── You are here                 │
│  ├─ Actions                                     │
│  └─ ...                                         │
│                                                   │
│  ┌────────────────────────────────────────────┐ │
│  │ Source                                      │ │
│  │ Branch: [main ▼]                           │ │
│  │ Folder: [/(root) ▼]                       │ │
│  │                                             │ │
│  │         [ Save ]                            │ │
│  └────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────┘
```

### Step 3: Access Your Live Site

- Your site will be available at: `https://YOUR_USERNAME.github.io/html-practice-resume/`
- It may take a few minutes for the site to be available
- GitHub will send you an email when the deployment is complete

### Step 4: Test Your Site Locally (Recommended)

Before deploying, test your HTML files locally to ensure everything works:

**For Windows (PowerShell):**
```powershell
# Navigate to your project folder
cd C:\Users\DELL\Documents\GitHub\html-practice-resume

# Start a local server
python -m http.server 8000
```

Then open `http://localhost:8000` in your browser to preview your site.

**Alternative for Windows:**
```powershell
# If Python isn't available, try:
php -S localhost:8000
```

**Visual Reference Notes:**
- ⚠️ If images aren't loading locally, check your file paths
- ⚠️ Ensure all internal links use relative paths (e.g., `./page.html` not `C:\path\to\page.html`)
- ✅ All HTML files should open correctly in your browser before deploying

### Step 5: Customize Your Site (Optional)

- If you have multiple HTML files, create a navigation menu or index page linking to all of them
- Add links between your practice files
- Style your pages to create a cohesive portfolio experience

### Common Mistakes to Avoid

- ❌ **Absolute paths**: Using `file:///C:/Users/...` in your HTML
  - ✅ **Solution**: Use relative paths like `./resume.html` or `../folder/page.html`
- ❌ **Missing index.html**: Not having an `index.html` file
  - ✅ **Solution**: Rename your main file to `index.html`
- ❌ **Case sensitivity**: Using inconsistent file name casing
  - ✅ **Solution**: Stick to lowercase filenames: `resume.html` not `Resume.HTML`
- ❌ **Broken images**: Image paths that don't match the deployed structure
  - ✅ **Solution**: Test all images load correctly in your local preview

---

## 2. Connecting a Custom Domain (Using warbot.app or Any Domain)

### Prerequisites
- A registered domain name (e.g., from Namecheap, Google Domains, GoDaddy, etc.)
- Domain registrar access to modify DNS records

### Step 1: Configure DNS Records

> 📸 **Screenshot Placeholder**: *Insert image of your domain registrar's DNS management page (FULLSTACKS, GoDaddy, Namecheap, etc.)*

Go to your domain registrar's DNS settings and add the following records:

#### Option A: Using Apex Domain (yourdomain.com)

**Visual Guide - DNS A Records:**
```
┌─────────────────────────────────────────────────────────┐
│  Domain DNS Management                                   │
│                                                         │
│  Type    Host    Points To            TTL              │
│  ─────   ─────   ─────────────────   ─────            │
│  A       @       185.199.108.153      3600             │
│  A       @       185.199.109.153      3600             │
│  A       @       185.199.110.153      3600             │
│  A       @       185.199.111.153      3600             │
│                                                         │
│  [ Add Record ] [ Save Changes ]                      │
└─────────────────────────────────────────────────────────┘
```

Add these A records:
```
Name  | Type | Value
------|------|------------
@     | A    | 185.199.108.153
@     | A    | 185.199.109.153
@     | A    | 185.199.110.153
@     | A    | 185.199.111.153
```

#### Option B: Using Subdomain (www.yourdomain.com)

**Visual Guide - DNS CNAME Record:**
```
┌─────────────────────────────────────────────────────────┐
│  Domain DNS Management                                   │
│                                                         │
│  Type     Host    Points To                    TTL     │
│  ─────    ─────   ──────────────────────────────     │
│  CNAME    www     YOUR_USERNAME.github.io      3600    │
│                                                         │
│  [ Add Record ] [ Save Changes ]                      │
└─────────────────────────────────────────────────────────┘
```

Add these CNAME records:
```
Name  | Type  | Value
------|-------|---------------------
www   | CNAME | YOUR_USERNAME.github.io
```

> 💡 **Visual Comparison**:
> ```
> Apex Domain (yourdomain.com)          vs.  Subdomain (www.yourdomain.com)
>      ↓                                          ↓
> Uses A Records (IP addresses)         Uses CNAME (domain name)
> More complex                          Simpler setup
> Both redirect to GitHub               Both redirect to GitHub
> ```

> **Note**: GitHub Pages supports both approaches. The A records are GitHub's latest IP addresses for apex domains.

### Step 2: Configure Custom Domain in GitHub

1. In your repository, go to **Settings** → **Pages**
2. Under **Custom domain**, enter your domain (e.g., `www.warbot.app` or `warbot.app`)
3. Click **Save**
4. GitHub will create a `CNAME` file in your repository

### Step 3: Wait for DNS Propagation

- DNS changes can take 24-48 hours to fully propagate
- Use tools like [dnschecker.org](https://dnschecker.org) to verify DNS propagation globally
- You can check if the domain is resolving: `ping warbot.app` (on Windows, open PowerShell)

### Step 4: Enable HTTPS (Automatic)

- GitHub Pages automatically provisions SSL certificates via Let's Encrypt
- Once DNS is configured, GitHub will enable HTTPS automatically
- You can check the "Enforce HTTPS" checkbox in Pages settings after the domain is verified

### Step 5: Update Your Links

- Update all internal links to use the custom domain
- Update social media profiles to point to your custom domain
- Submit your site to search engines (Google Search Console, Bing Webmaster Tools)

### Step 6: Optimize for Search Engines (SEO)

Add these meta tags to your HTML files to improve search engine visibility:

**In the `<head>` section of your HTML files:**

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- SEO Meta Tags -->
    <title>Your Full Name - Portfolio | Aspiring Developer</title>
    <meta name="description" content="Portfolio showcasing HTML, CSS, and web development projects by [Your Name]">
    <meta name="keywords" content="web development, HTML, CSS, portfolio, developer">
    <meta name="author" content="Your Name">
    
    <!-- Open Graph tags for social media sharing -->
    <meta property="og:title" content="Your Full Name - Portfolio">
    <meta property="og:description" content="Showcasing web development projects and skills">
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://yourdomain.com">
    
    <!-- Twitter Card tags -->
    <meta name="twitter:card" content="summary">
    <meta name="twitter:title" content="Your Full Name - Portfolio">
    <meta name="twitter:description" content="Showcasing web development projects">
</head>
```

**Benefits:**
- ✅ Better search engine ranking
- ✅ Professional appearance when shared on social media
- ✅ More clickable search results

### Step 7: Set Up Analytics (Optional)

Track your website visitors with Google Analytics:

1. **Get a Google Analytics Tracking ID:**
   - Go to [Google Analytics](https://analytics.google.com)
   - Create an account and property
   - Get your Measurement ID (e.g., `G-XXXXXXXXXX`)

2. **Add the tracking code to your HTML:**
   
   Add this before the closing `</head>` tag:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

3. **Verify tracking:**
   - Visit your live site
   - Check Google Analytics dashboard (data may take 24-48 hours to appear)

---

## Configuring Your Domain with Namecheap

This section provides detailed, step-by-step instructions for configuring your custom domain with Namecheap to point to your GitHub Pages site.

### Prerequisites

- A domain registered with Namecheap
- Access to your Namecheap account
- Your GitHub Pages site already deployed
- Your GitHub username (for the CNAME record)

### Step 1: Access Your Namecheap Account

1. **Log in to Namecheap**
   - Go to [namecheap.com](https://www.namecheap.com)
   - Click **Sign In** in the top right corner
   - Enter your username/email and password

2. **Navigate to Domain List**
   - Once logged in, click **Domain List** in the left sidebar
   - Find your domain in the list
   - Click **Manage** next to your domain

### Step 2: Access DNS Settings

1. **Go to Advanced DNS**
   - In your domain management page, click the **Advanced DNS** tab
   - You'll see a list of existing DNS records

2. **Clear Existing Records (if needed)**
   - Delete any existing A records pointing to parking pages
   - Delete any conflicting CNAME records
   - Common records to remove:
     - A records pointing to `198.54.xxx.xxx` (parking page)
     - CNAME records for `@` pointing to `parkingpage.namecheap.com`

### Step 3: Add A Records for Apex Domain

**For your root domain (e.g., `example.com`):**

1. **Click "Add New Record"**
2. **Create four A records** with these exact values:

| Type | Host | Value | TTL |
|------|------|-------|-----|
| A Record | @ | `185.199.108.153` | Automatic |
| A Record | @ | `185.199.109.153` | Automatic |
| A Record | @ | `185.199.110.153` | Automatic |
| A Record | @ | `185.199.111.153` | Automatic |

**Visual Guide - Adding A Records in Namecheap:**
```
┌─────────────────────────────────────────────────────────┐
│  Advanced DNS - example.com                              │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Type: [A Record ▼]                              │   │
│  │ Host: [@        ]                               │   │
│  │ Value: [185.199.108.153]                        │   │
│  │ TTL: [Automatic ▼]                              │   │
│  │                    [ Add Record ]               │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  Repeat for: 185.199.109.153, 185.199.110.153,         │
│              185.199.111.153                            │
└─────────────────────────────────────────────────────────┘
```

### Step 4: Add CNAME Record for WWW Subdomain

**For your www subdomain (e.g., `www.example.com`):**

1. **Click "Add New Record"**
2. **Create one CNAME record:**

| Type | Host | Value | TTL |
|------|------|-------|-----|
| CNAME Record | www | `YOUR_USERNAME.github.io.` | Automatic |

**Important Notes:**
- Replace `YOUR_USERNAME` with your actual GitHub username
- **Include the trailing dot (.)** at the end of the value
- Example: If your username is `johndoe`, use `johndoe.github.io.`

**Visual Guide - Adding CNAME Record in Namecheap:**
```
┌─────────────────────────────────────────────────────────┐
│  Advanced DNS - example.com                              │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Type: [CNAME Record ▼]                         │   │
│  │ Host: [www      ]                              │   │
│  │ Value: [johndoe.github.io.    ]                │   │
│  │ TTL: [Automatic ▼]                            │   │
│  │                    [ Add Record ]             │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

### Step 5: Save Your Changes

1. **Review all records** - You should now have:
   - 4 A records for `@` pointing to GitHub's IP addresses
   - 1 CNAME record for `www` pointing to your GitHub Pages

2. **Click "Save All Changes"**
   - Look for a green checkmark or "Save All Changes" button
   - Changes typically take 5-30 minutes to propagate

### Step 6: Configure Domain in GitHub

1. **Go to your GitHub repository**
2. **Navigate to Settings → Pages**
3. **Under "Custom domain"**, enter your domain:
   - For apex domain: `example.com`
   - For www subdomain: `www.example.com`
4. **Click Save**
5. **Wait for verification** (can take up to 24 hours)

### Step 7: Enable HTTPS

1. **After DNS propagation** (check with [DNS Checker](https://dnschecker.org))
2. **Return to Settings → Pages**
3. **Check "Enforce HTTPS"** checkbox
4. **Wait for SSL certificate** (automatic via Let's Encrypt)

### Troubleshooting Namecheap-Specific Issues

**Common Problems and Solutions:**

#### Problem: Site shows parking page
**Solution:**
- Remove the default parking page CNAME record
- Ensure no A records point to `198.54.xxx.xxx`

#### Problem: www subdomain not working
**Solution:**
- Verify CNAME record has trailing dot: `username.github.io.`
- Check TTL is set to "Automatic" or a low value (300-3600)

#### Problem: Domain not verifying in GitHub
**Solution:**
- Wait 24-48 hours for full DNS propagation
- Use [DNS Checker](https://dnschecker.org) to verify records globally
- Ensure no conflicting records exist

#### Problem: HTTPS not enabling
**Solution:**
- Wait for DNS to fully propagate
- Uncheck and recheck "Enforce HTTPS" after 24 hours
- Clear browser cache

### Verification Steps

**Test your configuration:**

1. **Check DNS propagation:**
   ```bash
   # Windows PowerShell
   nslookup example.com
   nslookup www.example.com
   ```

2. **Verify with online tools:**
   - [DNS Checker](https://dnschecker.org) - Check global propagation
   - [WhatsMyDNS](https://www.whatsmydns.net/) - Alternative DNS checker

3. **Test your site:**
   - Visit `http://example.com` (should redirect to HTTPS)
   - Visit `https://example.com` (should show your site)
   - Visit `https://www.example.com` (should also work)

### Final DNS Record Summary

Your Namecheap DNS should look like this:

```
Type       Host    Value                    TTL
A          @       185.199.108.153          Automatic
A          @       185.199.109.153          Automatic
A          @       185.199.110.153          Automatic
A          @       185.199.111.153          Automatic
CNAME      www     YOUR_USERNAME.github.io. Automatic
```

**Pro Tips:**
- ⚠️ **Always include the trailing dot** in CNAME values
- ✅ **Use "Automatic" TTL** for faster propagation
- ✅ **Test both apex and www** versions of your domain
- ✅ **Wait patiently** - DNS changes can take up to 48 hours

---

## 3. Automation and Continuous Deployment (CI/CD)

### Why CI/CD?

- Automatic deployment on every push
- No manual steps required
- Consistent deployment process
- Easy rollback capabilities

### Step 1: Create GitHub Actions Workflow

> 📸 **Screenshot Placeholder**: *Insert image showing the GitHub repository file explorer with .github/workflows folder structure*

Create the following directory structure in your repository:

**Visual Guide - Creating Workflow Files:**
```
html-practice-resume/
│
├── index.html
├── resume.html
└── .github/                ← Create this folder
    └── workflows/           ← Create this folder
        └── deploy.yml      ← Create this file

Steps:
1. In GitHub, click "Add file" → "Create new file"
2. Type: .github/workflows/deploy.yml
3. Copy and paste the workflow code below
4. Click "Commit new file"
```

**Directory Structure Visualization:**
```
┌─────────────────────────────────────────┐
│  Repository Files                        │
│  ┌────────────────────────────────┐    │
│  │ html-practice-resume/          │    │
│  │ ├── index.html                 │    │
│  │ ├── resume.html                │    │
│  │ ├── .github/ ← Create          │    │
│  │ │   └── workflows/ ← Create    │    │
│  │ │       └── deploy.yml          │    │
│  │ └── README.md                   │    │
│  └────────────────────────────────┘    │
└─────────────────────────────────────────┘
```

### Step 2: GitHub Actions Configuration

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  # Runs on pushes targeting the main branch
  push:
    branches: [ main ]
  
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Setup Node.js (optional, if you use build tools)
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      
      # Add any build steps here if needed
      # For example, if you're using a static site generator
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
  
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

### Step 3: Alternative Simple Deployment (No Build Steps)

If you just want to deploy static HTML files without any build process:
>>>>>>> Stashed changes

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

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v4
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

The DNS configuration varies slightly by registrar. Below are detailed instructions for the most common providers.

#### Option A: Namecheap (Recommended)

If your domain is registered with Namecheap, follow these steps:

1. **Log in to Namecheap**
   - Go to [namecheap.com](https://www.namecheap.com) and sign in
   - Click **Domain List** in the left sidebar
   - Find your domain and click **Manage**

2. **Access DNS Settings**
   - Click on the **Advanced DNS** tab
   - You'll see a list of DNS records

3. **Add A Records for Apex Domain**
   
   Click **Add New Record** and create these four A records:
   
   | Type | Host | Value | TTL |
   |------|------|-------|-----|
   | A Record | @ | `185.199.108.153` | Automatic |
   | A Record | @ | `185.199.109.153` | Automatic |
   | A Record | @ | `185.199.110.153` | Automatic |
   | A Record | @ | `185.199.111.153` | Automatic |
   
   **Note:** The `@` symbol represents your root domain (e.g., `yourname.com`)

4. **Add CNAME Record for WWW Subdomain**
   
   Click **Add New Record** and create:
   
   | Type | Host | Value | TTL |
   |------|------|-------|-----|
   | CNAME Record | www | `<username>.github.io.` | Automatic |
   
   **Important:** Replace `<username>` with your GitHub username. Add a trailing dot (`.`) at the end.
   
   Example: If your username is `octocat`, use `octocat.github.io.`

5. **Remove Conflicting Records**
   - Delete any existing A records pointing to parking pages (often `198.54.xxx.xxx`)
   - Delete any existing CNAME records for `@` or `www` that conflict
   - Common conflicting record: CNAME @ pointing to `parkingpage.namecheap.com`

6. **Save Changes**
   - Click the green checkmark or **Save All Changes** button
   - Changes can take 5-30 minutes to propagate

**Namecheap-Specific Tips:**
- ⚠️ Namecheap's parking page can interfere. Make sure to remove the default parking page CNAME.
- ✅ Keep "URL Redirect Record" disabled unless you're explicitly redirecting
- ✅ TTL set to "Automatic" is fine (usually 30 minutes)

#### Option B: Google Domains

1. **Access DNS Settings**
   - Go to [domains.google.com](https://domains.google.com)
   - Select your domain → Click **DNS** in the left menu

2. **Add Custom Records**
   
   Scroll to **Custom resource records** and add:
   
   **For apex domain:**
   ```
   Name: @
   Type: A
   TTL: 1H
   Data: 185.199.108.153
         185.199.109.153
         185.199.110.153
         185.199.111.153
   ```
   
   **For www subdomain:**
   ```
   Name: www
   Type: CNAME
   TTL: 1H
   Data: <username>.github.io.
   ```

#### Option C: Cloudflare

1. **Access DNS Settings**
   - Log in to Cloudflare
   - Select your domain
   - Go to **DNS** tab

2. **Add Records**
   
   Click **Add record** for each:
   
   **A Records:**
   - Type: `A`, Name: `@`, IPv4: `185.199.108.153`, Proxy: Off (DNS only)
   - Repeat for: `.109.153`, `.110.153`, `.111.153`
   
   **CNAME Record:**
   - Type: `CNAME`, Name: `www`, Target: `<username>.github.io`, Proxy: Off

   **Important:** Set Proxy status to "DNS only" (grey cloud), not "Proxied" (orange cloud)

#### General DNS Record Summary

No matter which registrar you use, you need these records:

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
=======
### Step 4: Enable GitHub Actions in Repository Settings

1. Go to **Settings** → **Actions** → **General**
2. Under **Workflow permissions**, select:
   - **Read and write permissions**
   - **Allow GitHub Actions to create and approve pull requests**
3. Click **Save**

### Step 5: Update GitHub Pages Source

1. Go to **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions** instead of a branch
3. Click **Save**

### Step 6: Test the Workflow

**Visual Guide - The Deployment Flow:**
```
┌─────────────────────────────────────────────────────────┐
│                    Deployment Flow                        │
│                                                         │
│  1. Edit Files         2. Commit & Push                 │
│     ↓                       ↓                            │
│  index.html              git push                       │
│  + resume.html            to GitHub                     │
│                                                         │
│  3. GitHub Actions       4. Build & Deploy               │
│     Triggered              ↓                            │
│     ↓                  Processing...                    │
│  Workflow Runs           ✓ Build Complete              │
│     ↓                       ↓                            │
│  5. Live Site Updated!                                  │
│     ↓                                                     │
│  ✅ https://yourusername.github.io/html-practice-resume │
└─────────────────────────────────────────────────────────┘
```

1. Make a small change to your HTML files
2. Commit and push the changes
3. Go to the **Actions** tab in your repository

> 📸 **Screenshot Placeholder**: *Insert image of GitHub Actions tab showing a running workflow with green checkmarks*

4. Watch the workflow run and deploy your site
5. Your site will update automatically!

**What You'll See in Actions Tab:**
```
┌─────────────────────────────────────────────────────┐
│  Actions | Pull requests | Security                  │
│  ┌────────────────────────────────────────────────┐ │
│  │ Deploy to GitHub Pages      [●] in progress    │ │
│  │ ┌──────────────────────────────────────────┐  │ │
│  │ │ ✓ Checkout code                         │  │ │
│  │ │ ✓ Setup Pages                           │  │ │
│  │ │ ✓ Upload artifact                       │  │ │
│  │ │ ● Deploy to GitHub Pages  ...running   │  │ │
│  │ └──────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────┘
```

---

## Backup and Recovery

Protecting your website from data loss is crucial. This section covers multiple backup strategies to ensure your GitHub Pages site is always recoverable.

### Why Backup Your Site?

**Common scenarios where backups save you:**
- 🗑️ **Accidental deletion** of files or entire repository
- 🔧 **Broken deployments** that corrupt your site
- 💻 **Computer crashes** before pushing changes
- 🔄 **Reverting to previous versions** when new changes break things
- 📦 **Moving to different hosting** or platforms

### 🏠 Built-in GitHub Backup (Automatic)

**The good news:** GitHub automatically backs up your repository!

**What GitHub provides:**
- ✅ **Complete repository history** - Every commit is saved
- ✅ **Branch protection** - Multiple versions of your code
- ✅ **Automatic replication** - GitHub stores copies in multiple data centers
- ✅ **Version control** - You can revert to any previous version

**How to access your backups:**
1. Go to your repository on GitHub
2. Click **Commits** to see all your changes
3. Click any commit to see what changed
4. Use **Releases** to create tagged backups

### 💾 Local Backup Strategies

#### Method 1: Clone Your Repository Locally

**Create a local copy of your entire site:**

```bash
# Clone your repository to your computer
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME

# This gives you a complete local backup
# You can work offline and push changes later
```

**Benefits:**
- ✅ Complete offline access
- ✅ Work without internet
- ✅ Local development environment
- ✅ Easy to restore if GitHub has issues

#### Method 2: Regular Local Backups

**Set up a backup routine:**

```bash
# Create a backup folder
mkdir ~/website-backups
cd ~/website-backups

# Clone your site (or update existing clone)
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
# OR if you already have it:
cd YOUR_REPO_NAME
git pull origin main

# Create a timestamped backup
cp -r YOUR_REPO_NAME YOUR_REPO_NAME-backup-$(date +%Y%m%d)
```

**Windows PowerShell version:**
```powershell
# Create backup folder
New-Item -ItemType Directory -Path "C:\website-backups" -Force
cd C:\website-backups

# Clone or update
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
# OR
cd YOUR_REPO_NAME
git pull origin main

# Create timestamped backup
Copy-Item -Path "YOUR_REPO_NAME" -Destination "YOUR_REPO_NAME-backup-$(Get-Date -Format 'yyyyMMdd')" -Recurse
```

### 🔄 Automated Backup Solutions

#### Method 1: GitHub Actions Backup

**Create an automated backup workflow:**

Create `.github/workflows/backup.yml`:

```yaml
name: Automated Backup

on:
  schedule:
    # Run every Sunday at 2 AM UTC
    - cron: '0 2 * * 0'
  workflow_dispatch: # Allow manual runs

jobs:
  backup:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Get full history
      
      - name: Create backup archive
        run: |
          tar -czf backup-$(date +%Y%m%d).tar.gz .
      
      - name: Upload backup as artifact
        uses: actions/upload-artifact@v4
        with:
          name: site-backup-$(date +%Y%m%d)
          path: backup-$(date +%Y%m%d).tar.gz
          retention-days: 30
```

**Benefits:**
- ✅ Automatic weekly backups
- ✅ Stored as GitHub artifacts
- ✅ 30-day retention
- ✅ Manual trigger option

#### Method 2: Mirror to Another Repository

**Create a backup repository:**

```yaml
name: Mirror to Backup Repository

on:
  push:
    branches: [ main ]
  schedule:
    - cron: '0 0 * * *' # Daily at midnight

jobs:
  mirror:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout source
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      
      - name: Push to backup repository
        run: |
          git remote add backup https://github.com/YOUR_USERNAME/YOUR_REPO_NAME-backup.git
          git push backup main
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### 📦 Export Your Site Files

#### Method 1: Download Repository as ZIP

**Manual backup method:**

1. Go to your repository on GitHub
2. Click **Code** → **Download ZIP**
3. Save the ZIP file to your computer
4. Extract when needed

**When to use:**
- ✅ Quick one-time backup
- ✅ Sharing your site files
- ✅ Moving to different hosting

#### Method 2: Export Built Site

**For sites with build processes:**

```bash
# If using a build tool like Jekyll, Next.js, etc.
npm run build
# or
bundle exec jekyll build

# Copy the built files (usually _site/, out/, dist/, or public/)
cp -r _site ~/website-backups/site-$(date +%Y%m%d)
```

### 🔄 Recovery Procedures

#### Scenario 1: Repository Deleted

**If your entire repository is deleted:**

1. **Check if it's in your trash:**
   - Go to GitHub → Settings → Repositories
   - Look for deleted repositories

2. **Restore from local backup:**
   ```bash
   cd ~/website-backups/YOUR_REPO_NAME
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
   git push -u origin main
   ```

3. **Recreate repository:**
   - Create new repository on GitHub
   - Push your local files to the new repository

#### Scenario 2: Files Accidentally Deleted

**Recover deleted files:**

```bash
# See what was deleted
git log --oneline

# Find the commit before deletion
git checkout COMMIT_HASH

# Copy the files you need
cp -r recovered-files/ ../current-version/

# Go back to latest version
git checkout main

# Add the recovered files
git add recovered-files/
git commit -m "Restore accidentally deleted files"
git push origin main
```

#### Scenario 3: Broken Deployment

**Revert to previous working version:**

```bash
# See recent commits
git log --oneline

# Revert to previous commit
git revert COMMIT_HASH

# Or reset to previous commit (more drastic)
git reset --hard COMMIT_HASH
git push --force origin main
```

**Using GitHub interface:**
1. Go to **Commits** in your repository
2. Find the last working commit
3. Click **Revert** to undo changes
4. Or click **Browse files** to see old version

### 🛡️ Best Practices for Backup

#### 1. Follow the 3-2-1 Rule

- **3 copies** of your data
- **2 different storage types** (local + cloud)
- **1 offsite backup** (GitHub counts as offsite)

#### 2. Regular Backup Schedule

**Recommended schedule:**
- ✅ **Daily:** Automatic Git commits (you're already doing this!)
- ✅ **Weekly:** Download repository ZIP
- ✅ **Monthly:** Full local backup
- ✅ **Before major changes:** Manual backup

#### 3. Test Your Backups

**Regularly verify backups work:**

```bash
# Test restoring from backup
cd ~/website-backups/YOUR_REPO_NAME-backup-20241201
python -m http.server 8000
# Visit http://localhost:8000 to verify it works
```

#### 4. Document Your Backup Process

**Create a backup checklist:**

```markdown
# My Website Backup Checklist

## Daily
- [ ] Commit and push changes to GitHub

## Weekly  
- [ ] Download repository ZIP
- [ ] Test local backup works

## Monthly
- [ ] Create full local backup
- [ ] Verify GitHub Actions backup ran
- [ ] Test recovery process

## Before Major Changes
- [ ] Create manual backup
- [ ] Document what I'm changing
- [ ] Test changes locally first
```

### 🚨 Emergency Recovery Kit

**Keep this information handy:**

```markdown
# Emergency Recovery Information

## Repository Details
- Repository URL: https://github.com/USERNAME/REPO_NAME
- Local backup location: ~/website-backups/REPO_NAME
- Last backup date: [Update regularly]

## Key Commands
- Clone repository: git clone https://github.com/USERNAME/REPO_NAME.git
- Restore from backup: git checkout COMMIT_HASH
- Revert changes: git revert COMMIT_HASH

## Important Files
- Main page: index.html
- Styles: css/style.css
- Images: images/
- Configuration: .github/workflows/

## Contact Information
- GitHub Support: https://support.github.com
- Domain registrar: [Your registrar's support]
```

### 💡 Pro Tips

**Additional backup strategies:**

1. **Use GitHub Releases:**
   - Create releases for major milestones
   - Download release archives as backups
   - Tag important versions

2. **Multiple GitHub Accounts:**
   - Fork your repository to another account
   - Automatic backup every time you push

3. **Cloud Storage Sync:**
   - Sync your local backup folder to Google Drive, Dropbox, etc.
   - Automatic cloud backup of your local files

4. **Domain and DNS Backup:**
   - Document your DNS settings
   - Screenshot your domain registrar settings
   - Keep CNAME file content saved

**Remember:** The best backup is the one you actually use regularly. Start with simple local backups and gradually add more sophisticated solutions as your site grows!

---

## 4. Best Practices and Tips

### Repository Organization

**Best Practice Structure:**
```
html-practice-resume/
│
├── index.html          ← Homepage
├── resume.html         ← Portfolio/resume
├── about.html          ← Additional pages
├── projects.html
│
├── css/                ← Stylesheets
│   └── styles.css
│
├── images/             ← Images and assets
│   ├── profile.jpg
│   └── projects/
│
├── js/                 ← JavaScript files
│   └── main.js
│
├── .github/
│   └── workflows/
│       └── deploy.yml  ← CI/CD config
│
├── README.md           ← Project documentation
└── .gitignore          ← Ignore unnecessary files
```

**Benefits:**
- ✅ Keep your repository clean and organized
- ✅ Use descriptive commit messages
- ✅ Create meaningful folder structures
- ✅ Add a comprehensive README.md

### Git Workflow

```bash
# Clone your repository (if not already cloned)
git clone https://github.com/YOUR_USERNAME/html-practice-resume.git
cd html-practice-resume

# Make changes to your files
# Edit resume.html, add new files, etc.

# Add and commit changes
git add .
git commit -m "Add new feature: [description]"

# Push to GitHub
git push origin main

# GitHub Actions will automatically deploy!
```

### Customization Tips

1. **Add an index.html** with links to all your practice files
2. **Style your pages** with CSS for better presentation
3. **Add metadata** to your HTML files for SEO
4. **Include a sitemap** for search engines
5. **Test your links** to ensure everything works

### Monitoring Your Site

- Use GitHub's Pages settings to monitor build status
- Check the Actions tab for deployment logs
- Monitor your custom domain's SSL certificate status
- Set up Google Analytics to track visitors (optional)

### Troubleshooting

- **Site not updating?** Check the Actions tab for build errors
- **Domain not working?** Verify DNS records with `nslookup` or dig
- **HTTPS issues?** Wait for Let's Encrypt certificate provisioning (can take up to 24 hours)
- **Build failures?** Check the workflow logs in the Actions tab

---

## 5. Advanced Configuration

### Using a Custom Domain with CNAME

If using a custom domain, the `CNAME` file in your repository root should look like:

```
www.warbot.app
```

Or for apex domain:
```
warbot.app
```

### Jekyll Configuration (Optional)

If you want to use Jekyll for static site generation, create a `_config.yml`:

```yaml
title: "Your Portfolio"
theme: minima
plugins:
  - jekyll-sitemap
  - jekyll-feed
```

### Exclude Files from Deployment

Create a `.gitignore`:

```
.DS_Store
*.log
node_modules/
.env
>>>>>>> Stashed changes
```

---

<<<<<<< Updated upstream
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
=======
## Troubleshooting FAQ

### 🔍 Troubleshooting Decision Tree

**Quick Diagnostic Flow:**
```
                     Site Not Working?
                           |
         ┌─────────────────┴─────────────────┐
         │                                   │
    Shows 404 Error              Shows "Not Found" Error
         │                                   │
         ↓                                   ↓
┌────────────────────┐              ┌────────────────────┐
│ Check Steps:       │              │ Check Steps:       │
│ 1. index.html      │              │ 1. Is it public?    │
│ 2. Pages enabled?  │              │ 2. Correct branch? │
│ 3. Wait 10-15 min  │              │ 3. File structure? │
└────────┬───────────┘              └────────────────────┘
         │
         ↓
    Build Failed?
         │
         ↓
┌────────────────────┐
│ Check Actions tab  │
│ for error logs     │
└────────────────────┘
```

### Your Build Failed

**Q: GitHub Actions workflow is failing with "build failed" error**  
**A:** 
1. Check the Actions tab for detailed error logs
2. Common causes:
   - Missing `index.html` file in root
   - Invalid HTML syntax
   - File name with spaces (use hyphens instead: `my-page.html`)
3. Fix the error and push again

**Q: My site is showing a 404 error**  
**A:**
- Ensure you have an `index.html` file in the root directory
- Check that GitHub Pages is enabled in Settings → Pages
- Wait 10-15 minutes for the first deployment to complete
- If using a branch, ensure the branch exists and contains files

### Your Custom Domain Isn't Working

**Q: Custom domain shows "Not Secure" or certificate error**  
**A:**
- Wait 24-48 hours for DNS propagation and SSL certificate provisioning
- Verify your DNS records are correct using `nslookup yourdomain.com`
- Check GitHub Pages settings show your custom domain as verified
- Clear your browser cache

**Q: Site loads on GitHub URL but not on custom domain**  
**A:**
- Verify DNS records are correctly configured
- Check the CNAME file in your repository root
- Use [dnschecker.org](https://dnschecker.org) to check global DNS propagation
- Try accessing your site from a different network/incognito mode

### Your Site Isn't Updating

**Q: Changes I made aren't showing on the live site**  
**A:**
- Hard refresh your browser: `Ctrl+F5` (Windows) or `Cmd+Shift+R` (Mac)
- Check that you committed and pushed to the correct branch
- Verify the GitHub Actions workflow completed successfully
- It can take 5-10 minutes for changes to propagate

**Q: Local files look different from deployed site**  
**A:**
- Check for relative path issues (absolute paths won't work on GitHub Pages)
- Ensure all linked files (CSS, JS, images) are committed to the repository
- Verify case sensitivity in file names (GitHub Pages is case-sensitive for paths)

### Advanced Issues

**Q: "Repository not found" error when accessing the site**  
**A:**
- Check that your repository is public (or you have Pages enabled for private repos)
- Verify you're using the correct username in the URL
- Ensure GitHub Pages is enabled in Settings → Pages

**Q: Images or assets aren't loading**  
**A:**
- Use relative paths: `./images/photo.jpg` not absolute paths
- Check that files are committed to Git
- Verify file extensions are correct and lowercase
- Test locally first to identify the issue

---

## Glossary

**Branch**: A parallel version of your code repository. The `main` branch is typically your production code.

**CI/CD (Continuous Integration/Continuous Deployment)**: Automated processes that build, test, and deploy your code whenever you make changes.

**DNS (Domain Name System)**: The system that translates domain names (like `warbot.app`) into IP addresses.

**Domain Registrar**: The company where you purchased your domain name (e.g., GoDaddy, Namecheap).

**GitHub Actions**: Automation service provided by GitHub to run tasks on your code.

**GitHub Pages**: Free web hosting service provided by GitHub for static websites.

**HTTPS**: Secure version of HTTP that encrypts data between your site and visitors.

**Jekyll**: Static site generator that GitHub Pages supports for building sites from Markdown and Liquid templates.

**Repository (Repo)**: A project folder on GitHub containing all your files and version history.

**SSL Certificate**: Digital certificate that enables HTTPS encryption for your website.

**Static Site**: A website that serves pre-built HTML files without server-side processing.
>>>>>>> Stashed changes

---

## Additional Resources

<<<<<<< Updated upstream
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
=======
### Learning Resources

- **HTML & CSS**: [MDN Web Docs](https://developer.mozilla.org/) - Comprehensive documentation
- **Git Basics**: [GitHub's Git Handbook](https://guides.github.com/introduction/git-handbook/)
- **Git Commands Cheat Sheet**: [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)

### Testing & Validation Tools

- **HTML Validator**: [W3C Markup Validator](https://validator.w3.org/)
- **CSS Validator**: [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
- **Mobile Responsiveness**: [Google Mobile-Friendly Test](https://search.google.com/test/mobile-friendly)
- **Performance**: [PageSpeed Insights](https://pagespeed.web.dev/)

### Deployment Tools

- **DNS Checker**: [DNS Checker](https://dnschecker.org/) - Verify DNS propagation worldwide
- **SSL Checker**: [SSL Labs](https://www.ssllabs.com/ssltest/) - Test your SSL certificate
- **Domain Status**: [WhatsMyDNS.net](https://www.whatsmydns.net/) - Check DNS records globally

### GitHub Resources

- **GitHub Pages Documentation**: [Pages Docs](https://docs.github.com/en/pages)
- **GitHub Actions Documentation**: [Actions Docs](https://docs.github.com/en/actions)
- **Community Support**: [GitHub Community Forum](https://github.community/)

### SEO & Analytics

- **Google Search Console**: [Search Console](https://search.google.com/search-console) - Monitor search performance
- **Google Analytics**: [Analytics](https://analytics.google.com/) - Track website visitors
- **Bing Webmaster Tools**: [Webmaster Tools](https://www.bing.com/webmasters/) - Submit to Bing

### Design Inspiration

- **Color Palettes**: [Coolors.co](https://coolors.co/) - Generate color schemes
- **Fonts**: [Google Fonts](https://fonts.google.com/) - Free web fonts
- **Icons**: [Font Awesome](https://fontawesome.com/) - Icon library
- **Placeholder Images**: [Unsplash](https://unsplash.com/) - Free high-quality photos

---

## Summary

### What You've Accomplished

By following this guide, you now have:

- ✅ **A live website** deployed on GitHub Pages with your unique URL
- ✅ **Automated deployments** that update your site on every push
- ✅ **Custom domain** configured (optional, but makes your site professional)
- ✅ **HTTPS/SSL encryption** for secure browsing
- ✅ **SEO optimization** for better search engine visibility
- ✅ **Analytics tracking** to monitor your visitors (optional)
- ✅ **Knowledge** to maintain, update, and expand your site

### Your Site URLs

- **GitHub Pages**: `https://YOUR_USERNAME.github.io/html-practice-resume`
- **Custom Domain**: `https://warbot.app` (or your chosen domain)

### Next Steps

1. **Share your site** with friends, family, and potential employers
2. **Keep learning** by adding new features and improving your projects
3. **Update regularly** with new projects and improvements
4. **Monitor performance** using the analytics tools you've set up
5. **Stay updated** by following web development best practices

### Remember

- Always test locally before deploying
- Use relative paths for all internal links and assets
- Commit often with descriptive commit messages
- Keep learning and improving your skills!

Happy deploying! 🚀

---

**Document Version**: 2.0  
**Last Updated**: Based on current GitHub Pages and Actions features  
**For Questions**: Refer to the [Troubleshooting FAQ](#troubleshooting-faq) section above

>>>>>>> Stashed changes
