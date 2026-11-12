# partyhop-site

Static site https://partyhop.app on GitHub Pages: plain HTML, no build step, no JS frameworks. Pages: `/` (landing), `/privacy`, `/terms`, `/help`, `/signin`, `404.html`, `.well-known/`. Details and the deploy checks are in `README.md`.

## Rules

- Every page copies the `<head>` styles of the others (Nunito, the `:root` tokens with the dark theme, header brand, footer links). Keep one look; a new page takes the same skeleton.
- Privacy and Terms are English only (legal texts). Do not translate them unless asked.
- **`/help` ("Where to find help") has a section for every language of the mobile app.** Each language is one `<section id="<code>" lang="<code>">` (`en`, `ru`, …: the same codes as the app's i18n files `partyhop/src/shared/i18n/<code>.json`), plus a link in the language nav at the top. The app opens `https://partyhop.app/help#<code>` for its current language. When a language is added to the app, add its section here in the same commit series: the same blocks as English (emergency number, Find a Helpline, Alcoholics Anonymous of that country or the worldwide finder, Al-Anon, national helplines of the countries where the language is mainly spoken, the "not a medical service" note), translated, and check that every link and phone number opens and is current. Never put a resource or number you have not checked.
- Links to help resources must be free, non-commercial and confidential services (helplines, AA, Al-Anon, health authorities). No clinics, ads or paid programs.
- The `/help` page is promised in the Terms (section 3) and linked from the app profile; never remove or move it without changing both.
- `.well-known/apple-app-site-association` and `assetlinks.json` must stay valid JSON and be served without a redirect (see README).
- Optimize images before adding (SVGO for SVG, TinyPNG or an equivalent for PNG).
- Commits: no Claude co-author lines.
