# RainOrg Website — Setup Guide (GitHub Pages + GoDaddy + Contact Form)

This guide walks you through putting the site live on **www.rainorg.com** using
GitHub Pages (free hosting) and your existing GoDaddy domain, and activating
the contact form so submissions land in your inbox.

## What you have

- `index.html` — the full website.
- `assets/logo.png` — your RainOrg logo (transparent background).
- `assets/mauricio-headshot.jpg` — your headshot, from the Brand Kit.
- `CNAME` — tells GitHub Pages which custom domain to serve (already set to `rainorg.com`).

**Important:** `index.html` references the logo and headshot as `assets/logo.png`
and `assets/mauricio-headshot.jpg`. Keep the `assets` folder in the same
location as `index.html` when you upload to GitHub, or the images won't show.

## Step 1 — Create the GitHub repository

1. Log into GitHub.
2. Click **New repository**.
3. Name it whatever you like (e.g. `rainorg-website`). Keep it **Public**
   (GitHub Pages requires a public repo on the free plan, unless you have
   GitHub Pro/Team).
4. Don't initialize with a README — you already have files to upload.

## Step 2 — Upload the files

Easiest way (no command line needed):

1. On the new repo's page, click **Add file → Upload files**.
2. Drag in `index.html` and `CNAME`, plus the whole `assets` folder
   (drag the folder itself — GitHub's uploader preserves the folder structure).
3. Commit directly to the `main` branch.

(If you prefer git commands: `git init`, `git add .`, `git commit -m "Initial site"`,
`git remote add origin <your-repo-url>`, `git push -u origin main`.)

## Step 3 — Turn on GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under "Build and deployment," set **Source** to `Deploy from a branch`.
3. Branch: `main`, folder: `/ (root)`. Save.
4. GitHub will give you a temporary URL like `https://yourusername.github.io/rainorg-website/`.
   Confirm the site loads there first before moving to your domain.
5. Still on the Pages settings screen, under "Custom domain," enter
   `rainorg.com` and save. (This step re-writes the CNAME file for you if it's
   not already there — you've already got one uploaded, so it should just
   confirm it.)

## Step 4 — Point your GoDaddy domain to GitHub

In GoDaddy, go to **My Products → rainorg.com → DNS → Manage DNS**, and set:

**A records** (root domain `rainorg.com`) — add these four A records, all pointing to `@`:

| Type | Name | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**CNAME record** (for the `www` version):

| Type | Name | Value |
|---|---|---|
| CNAME | www | yourusername.github.io |

Remove any existing A records or "parked page" records GoDaddy put there by
default — they'll conflict.

DNS changes can take anywhere from a few minutes to a few hours to propagate.

## Step 5 — Enforce HTTPS

Back in GitHub → Settings → Pages, once GitHub detects the DNS is pointed
correctly, check **Enforce HTTPS**. This gives you the padlock/SSL certificate
automatically, at no cost.

## Step 6 — Activate the contact form

The form uses **FormSubmit** (formsubmit.co) — a free service that forwards
form submissions straight to an email address, with no backend or signup
required. It's already wired to `mauricio@rainorg.com` in `index.html`.

**One-time activation:** the *first* time anyone submits the form after it
goes live, FormSubmit will send a confirmation email to `mauricio@rainorg.com`
asking you to click a link to activate that address. Do this yourself once
(fill out the form on your live site, then check your inbox and click
"Activate Form") — after that, every future submission goes straight through
with no extra clicks.

A couple of settings already built in:
- `_captcha: true` — adds a basic spam-prevention checkbox.
- `_template: table` — formats the email nicely as a table instead of raw text.

If you'd rather not depend on a third-party form service at all, two
alternatives if this ever becomes a problem:
- **Web3Forms** (web3forms.com) — similar free service, requires grabbing an
  access key first (sent to your email) rather than working with zero signup.
- A simple **Power Automate flow** connected to a Microsoft Form, since you
  already have Microsoft 365 — more setup, but keeps everything inside
  Microsoft's ecosystem.

## Updating the site later

Any time you want to change text, images, or styling: edit `index.html`
directly on GitHub (there's a pencil/edit icon on the file page) or upload a
replacement file. GitHub Pages rebuilds automatically within a minute or two
of any commit to `main`.

## Content and branding

- Colors, fonts (Poppins), logo, headshot, slogan, and the "About Mauricio"
  bio are all pulled from your RainOrg Brand Kit and LinkedIn profile — no
  more placeholders.
- The LinkedIn "About" text was adapted for a client-facing consulting site
  (it drops the "actively seeking a role" language, since this page is
  positioning you as a consultant/founder, not a job seeker). Re-read it and
  adjust the wording, achievements, or service list any time it needs
  tightening.
- The services list (HR, social media, platform management, newsletters,
  events, fractional leadership) follows the audience and service list noted
  in your Brand Kit guide (nonprofits). Adjust if your target audience is
  broader than nonprofits.
