# PerspectiveSocial.com - Launch Guide

Everything in this folder is your complete website. Follow these steps in order. Total time: ~30 minutes, all free except the domains you already own.

## What's in the folder

```
perspectivesocial/
├── index.html          → the website (one page, brand guide applied)
├── data/
│   ├── portfolio.json  → your case studies (currently: Ristlin)
│   └── settings.json   → contact email, booking link, hero text
├── admin/
│   ├── index.html      → your CMS panel (perspectivesocial.com/admin)
│   └── config.yml      → CMS configuration
├── images/uploads/     → where CMS uploads land
└── netlify.toml        → hosting config + .ie → .com redirects
```

## Step 1 - Put the site on GitHub (5 min)

1. Create a free account at github.com (if you don't have one).
2. New repository → name it `perspectivesocial` → Private → Create.
3. On the repo page: "uploading an existing file" → drag the entire contents of this folder in → Commit.

Important: upload the folder *contents* (index.html at the root of the repo), not the folder itself.

## Step 2 - Deploy on Netlify (5 min)

1. Sign up at netlify.com with your GitHub account.
2. "Add new site" → "Import an existing project" → GitHub → select `perspectivesocial`.
3. Leave build settings empty (it's a static site) → Deploy.
4. You'll get a temporary URL like `random-name.netlify.app` - the site is live. Check it looks right.

## Step 3 - Turn on the CMS login (5 min)

The CMS lives at `/admin` and uses Netlify Identity so only you can edit.

1. In Netlify: Site configuration → Identity → Enable Identity.
2. Identity → Registration → set to **Invite only**.
3. Identity → Services → **Enable Git Gateway**.
4. Identity → Invite users → invite ristlin.ro@gmail.com → accept the email invite and set a password.
5. Go to `yoursite.netlify.app/admin` → log in → you'll see "Portfolio / Clients" and "Site Settings".

Adding a new client later = log in to /admin → Portfolio → "Add Clients" → fill the card → Publish. The site updates itself in about a minute.

## Step 4 - Connect perspectivesocial.com (Namecheap)

1. In Netlify: Domain management → Add a domain → `perspectivesocial.com` → also add `www.perspectivesocial.com`.
2. Netlify shows you DNS values. In Namecheap: Domain List → perspectivesocial.com → Advanced DNS, then add:

| Type  | Host | Value |
|-------|------|-------------------------------|
| A     | @    | 75.2.60.5 (Netlify's load balancer - confirm the IP Netlify shows you) |
| CNAME | www  | `your-site-name.netlify.app` |

3. Delete any existing parking/URL-forward records on those hosts.
4. Back in Netlify, wait for verification, then enable HTTPS (automatic, free Let's Encrypt). DNS can take up to a few hours.

## Step 5 - Redirect perspectivesocial.ie (Blacknight)

Two options:

**Option A - simplest:** in the Blacknight control panel, use their "web forwarding / URL redirect" feature to send perspectivesocial.ie (and www) to https://perspectivesocial.com with a 301. Done - skip the rest.

**Option B - cleaner (redirect handled by Netlify):**
1. In Netlify Domain management, add `perspectivesocial.ie` and `www.perspectivesocial.ie` as domain aliases.
2. At Blacknight, point the .ie DNS at Netlify exactly like Step 4 (A record @ → Netlify IP, CNAME www → your netlify.app address).
3. The `netlify.toml` in this folder already contains the 301 rules, so all .ie traffic lands on perspectivesocial.com automatically. Better for SEO consistency.

## Step 6 - Before you announce it

- Update `data/settings.json` (or via /admin → Site Settings): real contact email, and your Calendly/Cal.com link if you want "Book a Call" to go to a calendar instead of email.
- Add a cover image to the Ristlin card via /admin (16:10 crop looks best).
- Set up the email address (e.g. hello@perspectivesocial.com) - Namecheap offers email forwarding free, or use Google Workspace.

## Editing content later

| What | Where |
|------|-------|
| Add/edit portfolio clients | perspectivesocial.com/admin → Portfolio |
| Contact email / booking link / hero text | perspectivesocial.com/admin → Site Settings |
| Services, about text, structural changes | edit `index.html` (ask Claude) |
