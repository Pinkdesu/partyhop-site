# partyhop-site

Static website for https://partyhop.app, hosted on GitHub Pages.

| Page | URL |
|---|---|
| Landing | https://partyhop.app/ |
| Privacy Policy | https://partyhop.app/privacy |
| Terms of Use | https://partyhop.app/terms |

Plain HTML, no build step. Edit the files and push to `main`.

## Setup (once)

1. Push this repository to GitHub.
2. Settings → Pages → Source: Deploy from a branch, branch `main`, folder `/ (root)`.
3. Custom domain: `partyhop.app` (already in `CNAME`), then turn on Enforce HTTPS once the certificate is issued.
4. DNS at the domain registrar:
   - `A` records for `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `AAAA` records for `@` (optional): `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`
   - `CNAME` for `www`: `<github-username>.github.io`

`.app` domains require HTTPS, so the site opens only after GitHub issues the certificate (usually within an hour).
