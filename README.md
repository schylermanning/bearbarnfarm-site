# Bear Barn Farm site

A two-page static website for the [Bear Barn Farm Etsy shop](https://www.etsy.com/shop/BearBarnFarm), hosted on GitHub Pages at [bearbarnfarm.com](http://bearbarnfarm.com/).

This repo is public, and GitHub Pages serves every file in it, including this one. Keep keys, customer details and private plans out of it.

## Purpose

- Give the shop a home page on its own domain.
- Publish a [privacy policy](http://bearbarnfarm.com/privacy/) that covers the shop and the Bear Barn Farm Pin Scheduler, our private tool for posting Pins to our own Pinterest account.

This site is not a store. Sales happen on Etsy. The Pin Scheduler's code is not in this repo.

## Status

Last checked November 23, 2026, about 5:45 PM Eastern.

| Item | Status |
| --- | --- |
| Home page and privacy policy | Live over HTTP |
| GitHub Pages | Built from `main`, root folder |
| `bearbarnfarm.com` DNS | Four A records resolving |
| `www.bearbarnfarm.com` | Redirects to `bearbarnfarm.com` |
| HTTPS certificate | Not issued yet |
| Enforce HTTPS | Off until the certificate is issued |

## Plan

### Phase 1: Build and publish (done)

- [x] Write the home page and privacy policy
- [x] Create the public repo and push `main`
- [x] Turn on GitHub Pages with the custom domain

### Phase 2: Connect the domain (done)

- [x] Add four A records for the main domain
- [x] Add the `www` CNAME
- [x] Confirm the existing email records are still in place
- [x] Confirm both pages load on the domain

### Phase 3: Turn on HTTPS (waiting on GitHub)

- [ ] GitHub issues the certificate
- [ ] Turn on Enforce HTTPS
- [ ] Confirm `https://bearbarnfarm.com/` and `https://bearbarnfarm.com/privacy/` load
- [ ] Change the `http://` site links in this README to `https://`

If no certificate appears within a day, remove and re-add the custom domain in **Settings > Pages**.

### Phase 4: Use the privacy policy link

- [ ] Once HTTPS works, use `https://bearbarnfarm.com/privacy/` wherever the Pin Scheduler needs a privacy policy link

## Files

| File | What it is |
| --- | --- |
| `index.html` | Home page |
| `privacy/index.html` | Privacy policy, served at `/privacy/` |
| `logo.jpg` | Shop logo, also used as the browser-tab icon |
| `CNAME` | Custom domain for GitHub Pages; don't delete |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |
| `README.md` | This file |

## Design

Each page carries its own inline CSS, so make style changes in both files. Headings use Bitter (600 and 700) and body text uses Source Sans 3, both from Google Fonts. The layout is one column, up to 40rem wide with 16px side padding.

| Color | Light | Dark |
| --- | --- | --- |
| Background | `#fbf8f3` | `#1d1915` |
| Text | `#2c241c` | `#ece4d8` |
| Muted | `#6b5d4f` | `#b3a593` |
| Accent | `#8a5a2b` | `#d49a5c` |

Dark mode follows the visitor's device setting.

## DNS records for this site

| Type | Name | Value |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `schylermanning.github.io` |

Other records on the domain run email. Leave them alone when editing these.

## Making changes

Preview from the repo folder, then open http://localhost:8000/:

```bash
python3 -m http.server 8000
```

Publish by committing and pushing to `main`. GitHub Pages rebuilds on its own:

```bash
git push origin main
```

When the privacy policy changes, update the "Last updated" date at the top of that page.

## Checking the site

Pages and certificate status:

```bash
gh api repos/schylermanning/bearbarnfarm-site/pages --jq '{status,cname,https_certificate,https_enforced}'
```

Turn on Enforce HTTPS, only after the certificate is issued:

```bash
gh api -X PUT repos/schylermanning/bearbarnfarm-site/pages -F https_enforced=true
```
