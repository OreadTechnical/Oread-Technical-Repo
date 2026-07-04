# Deploy Oread Technical to GitHub Pages

This guide walks through pushing the site to [Oread-Technical-Repo](https://github.com/OreadTechnical/Oread-Technical-Repo) and launching it at **www.oreadtechnical.com**.

---

## Prerequisites

- Jeremy (or you) has **write access** to the `OreadTechnical` GitHub organization
- The domain **oreadtechnical.com** is registered at Namecheap (already done)
- [Git](https://git-scm.com/) installed locally

---

## Step 1 — Push the site to GitHub

Open Terminal and run these commands from the project folder:

```bash
cd "/Users/nicholaswerne/Documents/Personal/For Others/Jeremy"

# Initialize git (first time only)
git init
git branch -M main

# Stage all site files
git add index.html css/ js/ assets/ CNAME .nojekyll README.md DEPLOYMENT.md

# Create the first commit
git commit -m "Launch Oread Technical website with résumé and services"

# Connect to Jeremy's repo (first time only)
git remote add origin https://github.com/OreadTechnical/Oread-Technical-Repo.git

# Push to GitHub — you will be prompted to sign in
git push -u origin main
```

If the remote already exists from a previous attempt:

```bash
git remote set-url origin https://github.com/OreadTechnical/Oread-Technical-Repo.git
git push -u origin main
```

> **Auth tip:** GitHub no longer accepts account passwords for `git push`. Use a [Personal Access Token](https://github.com/settings/tokens) as the password, or sign in via the GitHub CLI (`gh auth login`).

---

## Step 2 — Enable GitHub Pages

1. Go to https://github.com/OreadTechnical/Oread-Technical-Repo
2. Click **Settings** → **Pages** (left sidebar)
3. Under **Build and deployment**:
   - **Source:** Deploy from a branch
   - **Branch:** `main` → `/ (root)` → **Save**
4. Wait 1–3 minutes. The site will be live at:
   - `https://oreadtechnical.github.io/Oread-Technical-Repo/` (temporary URL)

---

## Step 3 — Connect the custom domain

Still on the **Pages** settings page:

1. Under **Custom domain**, enter: `www.oreadtechnical.com`
2. Click **Save**
3. Check **Enforce HTTPS** once the certificate is issued (may take up to 24 hours)

The `CNAME` file in this repo tells GitHub Pages to serve the site at that domain.

---

## Step 4 — Configure DNS at Namecheap

Log in to [Namecheap](https://www.namecheap.com/) → **Domain List** → **oreadtechnical.com** → **Manage** → **Advanced DNS**.

### For `www.oreadtechnical.com` (required)

| Type  | Host | Value                         | TTL  |
|-------|------|-------------------------------|------|
| CNAME | www  | `oreadtechnical.github.io.`   | Auto |

> Include the trailing dot on the CNAME value if Namecheap requires it.

### For bare `oreadtechnical.com` (optional — redirects to www)

Add four **A records** pointing the apex domain to GitHub Pages:

| Type | Host | Value           | TTL  |
|------|------|-----------------|------|
| A    | @    | 185.199.108.153 | Auto |
| A    | @    | 185.199.109.153 | Auto |
| A    | @    | 185.199.110.153 | Auto |
| A    | @    | 185.199.111.153 | Auto |

Then in GitHub Pages settings, you can also add `oreadtechnical.com` as a second custom domain so both work.

**Remove** any existing parking-page records Namecheap may have added.

DNS changes can take 15 minutes to 48 hours to propagate.

---

## Step 5 — Verify

1. Visit https://www.oreadtechnical.com — you should see the Oread Technical site
2. Click **Download résumé** — the DOCX should download
3. In GitHub → repo → **Settings** → **Pages**, confirm the green checkmark: *"Your site is live at..."*

Use https://www.whatsmydns.net/ to check if the CNAME has propagated globally.

---

## Updating the site later

After editing files locally:

```bash
cd "/Users/nicholaswerne/Documents/Personal/For Others/Jeremy"
git add -A
git commit -m "Describe your change"
git push
```

GitHub Pages rebuilds automatically within a minute or two.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| 404 on GitHub Pages URL | Confirm branch is `main`, folder is `/ (root)`, and `index.html` is at repo root |
| Domain shows Namecheap parking page | DNS not updated yet — check CNAME record for `www` |
| HTTPS not available | Wait for DNS + certificate; ensure **Enforce HTTPS** is checked |
| Push rejected (auth) | Use a Personal Access Token or `gh auth login` |
| Resume download 404 | Ensure `assets/Jeremy_deNoyelles_Resume_2026.docx` was committed |

---

## Quick reference

| Item | Value |
|------|-------|
| GitHub repo | https://github.com/OreadTechnical/Oread-Technical-Repo |
| Live site | https://www.oreadtechnical.com |
| Contact | oreadtech@gmail.com · (316) 210-7077 |
