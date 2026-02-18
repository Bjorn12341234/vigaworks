# Viga Works — vigaworks.com

Official website for Viga Works AB. Static site hosted on GitHub Pages.

## Structure

```
/                    → Landing page
/games               → Game catalog
/hnefatafl           → Hnefatafl product page
/forest-clicker      → Forest Clicker product page
/support             → Support & contact info
/privacy             → Privacy policy
/terms               → Terms of use
404.html             → Custom 404 page
style.css            → Shared stylesheet
favicon.svg          → Site favicon
CNAME                → Custom domain config
```

## Run locally

Any static file server works. For example:

```bash
# Python
python3 -m http.server 8000

# Node (npx)
npx serve .

# Then open http://localhost:8000
```

## Deploy

The site is published via GitHub Pages from the root of the `main` branch.

1. Push changes to `main`.
2. GitHub Pages will automatically deploy.
3. The `CNAME` file points to `vigaworks.com`.

### GitHub Pages settings

In the repo → Settings → Pages:
- **Source:** Deploy from a branch
- **Branch:** `main` / `/ (root)`
- **Custom domain:** `vigaworks.com`
- **Enforce HTTPS:** ✓

## DNS setup for HostUp

To point `vigaworks.com` to GitHub Pages, add these DNS records in your HostUp control panel:

### A records (apex domain)

| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

### CNAME record (www subdomain)

| Type | Name | Value |
|------|------|-------|
| CNAME | www | Bjorn12341234.github.io |

### Verification checklist

After setting up DNS:

- [ ] A records point to all four GitHub Pages IPs
- [ ] CNAME for `www` points to `Bjorn12341234.github.io`
- [ ] Wait for DNS propagation (can take up to 48 hours, usually faster)
- [ ] In GitHub repo → Settings → Pages, set custom domain to `vigaworks.com`
- [ ] Check "Enforce HTTPS" once the certificate is provisioned
- [ ] Verify: `https://vigaworks.com` loads the landing page
- [ ] Verify: `https://vigaworks.com/privacy` loads the privacy policy
- [ ] Verify: `https://vigaworks.com/support` loads the support page
- [ ] Verify: `https://vigaworks.com/terms` loads the terms page
- [ ] Verify: `https://vigaworks.com/games` lists games
- [ ] Verify: `https://vigaworks.com/nonexistent` shows the 404 page

You can check DNS propagation with:
```bash
dig vigaworks.com +short
# Should return the four GitHub Pages IPs
```

## Add a new game page

1. Create a new directory: `mkdir my-game`
2. Copy an existing game page: `cp hnefatafl/index.html my-game/index.html`
3. Edit `my-game/index.html`:
   - Update `<title>`, `<meta name="description">`, and OG tags
   - Update the heading, description, and status
4. Add a card for the game in `games/index.html`:
   ```html
   <a href="/my-game" class="card game-card">
     <span class="badge">In Development</span>
     <h3>My Game</h3>
     <p class="text-small text-dim">Short description of the game.</p>
   </a>
   ```
5. Add a game-specific disclosure section in `privacy/index.html`:
   - Copy one of the existing disclosure tables
   - Update the heading and fill in what the game collects
6. Commit and push to `main`.

## Tech

- Plain HTML + CSS, no build step
- System fonts only (no external fonts)
- No external JavaScript
- No frameworks or dependencies
- Accessible: semantic HTML, focus styles, skip-to-content links
