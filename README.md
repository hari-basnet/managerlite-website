# Manager Lite — marketing site

Static site: landing page, Privacy Policy, Terms & Conditions, Contact.
Plain HTML/CSS, no build step — GitHub Pages serves it as-is.

## Deploy

1. Create a **public** repo (e.g. `managerlite-website`) and push this folder to it.
2. Repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch:
   `main` / `(root)` → Save.
3. Still on that page, under **Custom domain**, enter `managerlite.com` and
   save (this repo already has a `CNAME` file with that value, so GitHub
   should detect it automatically — the field just confirms/re-writes it).
4. Check **Enforce HTTPS** once GitHub finishes issuing the certificate
   (can take a few minutes to a few hours after DNS is set up).

## DNS (Namecheap)

Namecheap → Domain List → `managerlite.com` → **Manage** → **Advanced DNS**
→ add these records (remove any existing A/CNAME records on the same hosts
first — you can't have two records competing for the same host):

| Type | Host | Value | TTL |
| ---- | ---- | ----- | --- |
| A | @ | 185.199.108.153 | Automatic |
| A | @ | 185.199.109.153 | Automatic |
| A | @ | 185.199.110.153 | Automatic |
| A | @ | 185.199.111.153 | Automatic |
| CNAME | www | `<your-github-username>.github.io.` | Automatic |

The four `A` records point the bare `managerlite.com` (host `@`) at GitHub
Pages' servers — these four IPs are GitHub's standard, documented Pages
IPs and are the same for every GitHub Pages site. The `www` CNAME makes
`www.managerlite.com` work too and redirect to the bare domain.

DNS propagation can take anywhere from a few minutes to ~24 hours. GitHub
Pages won't be able to provision the HTTPS certificate until DNS resolves
correctly, so the "Enforce HTTPS" checkbox may be greyed out until then —
that's expected, not a bug.

## Before going live

- [ ] `terms.html` has a `[TODO]` placeholder for governing law/jurisdiction
      — fill in before publishing.
- [ ] Add real App Store / Play Store links to `index.html` once both are
      live (search for "Coming soon" / `#notify`).
- [ ] Contact form (`contact.html`) currently opens the visitor's email app
      via a `mailto:` link — zero setup, always works, but requires them to
      have a mail client configured. If you want in-page submission instead
      (no email app popup), sign up for a free form backend like
      [Formspree](https://formspree.io) and swap the form's submit handler
      to POST to your Formspree endpoint instead.
- [ ] Once `privacy.html` is live at its final URL, paste that URL into
      `managerlite/docs/app-store-listing.md` §8 (the main app repo) and
      into both App Store Connect and Play Console's privacy policy fields.
