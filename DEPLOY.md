# Deploying mnshot.ai

End-to-end path: local repo → GitHub → Cloudflare Pages → custom domain on Namecheap.

---

## 1. Clean up and initialize git locally

A partial `.git/` directory was created while we were working — clear it and start fresh from your own Terminal.

```bash
cd ~/projects/mnshot.ai
rm -rf .git
git init -b main
git add .gitignore README.md DEPLOY.md index.html
git commit -m "Initial commit: mnshot.ai marketing site"
```

## 2. Create a GitHub repo and push

**Option A — GitHub CLI (fastest, if you have `gh` installed):**

```bash
gh auth status           # if not signed in: gh auth login
gh repo create mnshot.ai --public --source=. --remote=origin --push
```

**Option B — GitHub web UI:**

1. Go to [github.com/new](https://github.com/new).
2. Name: `mnshot.ai`. Visibility: public (or private, your call). Leave everything else blank — no README, no .gitignore.
3. Create the repo, then in Terminal:

```bash
git remote add origin git@github.com:<your-username>/mnshot.ai.git
git push -u origin main
```

## 3. Deploy via Cloudflare Pages

1. Sign in to [dash.cloudflare.com](https://dash.cloudflare.com) (create an account if needed — free tier is fine).
2. **Workers & Pages → Create application → Pages → Connect to Git.**
3. Authorise Cloudflare to read your GitHub, pick the `mnshot.ai` repo.
4. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave blank)*
   - **Build output directory:** `/`
5. Save and deploy. You'll get a `<project>.pages.dev` URL in ~1 minute.

## 4. Point mnshot.ai at Cloudflare

### 4a. Move the domain onto Cloudflare (nameservers)

1. In Cloudflare: **Websites → Add a site → `mnshot.ai` → Free plan → Continue.**
2. Cloudflare shows you two nameservers, e.g. `xxx.ns.cloudflare.com` / `yyy.ns.cloudflare.com`.
3. In Namecheap: **Domain List → Manage (mnshot.ai) → Nameservers → Custom DNS.** Paste Cloudflare's two nameservers, save.
4. Nameserver propagation takes anywhere from a few minutes to a few hours. Cloudflare emails you when it completes.

### 4b. Attach the custom domain to Pages

1. Back in Cloudflare Pages → your `mnshot.ai` project → **Custom domains → Set up a custom domain.**
2. Enter `mnshot.ai`. Cloudflare adds the DNS records automatically (because the zone is also on Cloudflare now).
3. Repeat for `www.mnshot.ai` if you want the `www` subdomain. Optionally add a redirect rule: `www.mnshot.ai/*` → `https://mnshot.ai/$1` (permanent).
4. HTTPS is issued automatically.

### 4c. (Later) aether.mnshot.ai

When Aether is ready, create a second Pages project (or a Worker) and attach `aether.mnshot.ai` as a custom domain the same way.

---

## Iterating after launch

The site is a single `index.html`. To change something:

```bash
# edit index.html
git add index.html
git commit -m "..."
git push
```

Cloudflare Pages auto-deploys on push to `main` — each push is live in under a minute.
