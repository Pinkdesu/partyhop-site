# partyhop-site

Static website for https://partyhop.app, hosted on GitHub Pages.

| Page | URL |
|---|---|
| Landing | https://partyhop.app/ |
| Privacy Policy | https://partyhop.app/privacy |
| Terms of Use | https://partyhop.app/terms |
| Where to find help (alcohol support links; `#ru` for Russian) | https://partyhop.app/help |
| Open the app (fallback of app links) | https://partyhop.app/signin |

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

## App links (`.well-known`)

Links to `https://partyhop.app/signin…` and `https://partyhop.app/auth/…` (the buttons in the
API's emails) open the PartyHop app when it is installed; otherwise `/signin` shows a page with
a button to `partyhop://signin`. `.nojekyll` makes GitHub Pages serve the `.well-known` folder.

- `.well-known/apple-app-site-association` (no extension, JSON): iOS Universal Links for the app
  `M75QRZJ26X.com.partyhop.app` (Team ID + bundle id) on the paths `/signin*` and `/auth/*`, plus
  `webcredentials` for password autofill. The app needs `ios.associatedDomains:
  ["applinks:partyhop.app"]` in `app.json` and the Associated Domains capability of its App ID.
- `.well-known/assetlinks.json`: Android App Links for the package `com.partyhop.app`. It holds
  only the SHA-256 of the debug key now. **Before a release add the SHA-256 of the EAS upload
  key (`eas credentials -p android`) and of Google Play App Signing (Play Console → Test and
  release → App integrity).** The app needs an `android.intentFilters` entry with `autoVerify`
  for `https://partyhop.app`.

Check after a deploy:

```bash
curl -I https://partyhop.app/.well-known/apple-app-site-association
```

It must answer `200` with no redirect. GitHub Pages serves the file as
`application/octet-stream`; Apple's CDN reads it anyway as long as it is valid JSON.

- What Apple's CDN sees (it caches for a while):
  https://app-site-association.cdn-apple.com/a/v1/partyhop.app
- What Google sees:
  https://digitalassetlinks.googleapis.com/v1/statements:list?source.web.site=https://partyhop.app&relation=delegate_permission/common.handle_all_urls
