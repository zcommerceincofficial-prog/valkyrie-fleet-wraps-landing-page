# Site log — Valkyrie Fleet Wraps, main (Google Ads) landing page

Live at https://valkriewraps.xyz (Cloudflare Pages project
`valkyrie-fleet-wraps-landing-page`). Built by mirroring live production HTML, no
`site/` raw export and no build step — `index.html` / `thank-you.html` are served
directly.

- **2026-09-12** — Synced this repo to match what was actually live (it had drifted:
  old JPG/PNG assets, missing fonts, no B2B 2-step form). Made Vehicle Type and
  Company Name required to match the meta variant, added the same B2B-qualifying
  second form step (Company Role, Industry, both required) and "business vehicles
  only" copy. Verified with a real test submission (name "Test Main Ignore") —
  webhook 204 (`FvnVnnGvT8TrWzmIlMXz` / `6004111c-fd5a-45bb-b769-e3e681774f4a`),
  landed on `/thank-you`.
- **2026-09-12** — Ran `scripts/machine-layer-check.mjs` against the live domain.
  Found and fixed the same skipped heading level as the meta variant (H1 straight to
  H3 on the hero form card, same source pattern) — bumped to H2/H3, updated the
  matching CSS selectors. Added LocalBusiness JSON-LD schema (none existed). Added
  meta description and canonical to `thank-you.html` (both missing). No real
  `robots.txt` or `sitemap.xml` existed, so Cloudflare Pages fell back to serving the
  full `index.html` at those paths — added real files (this site IS meant to be
  indexed, so `Allow: /` plus a `Sitemap:` line, unlike the meta variant) plus a real
  `404.html`. Added `_headers` for security headers.
  Confirmed a Cloudflare zone-level "Managed Content" / AI Crawl Control feature is
  merging its own AI-crawler block (blocks GPTBot, ClaudeBot, Google-Extended, etc.,
  allows normal search engines) in front of our robots.txt on the custom domain only
  — not a repo bug, a dashboard setting on the valkriewraps.xyz zone. Left it as is
  (protects content from AI scraping without blocking real search crawlers); flagged
  to the client rather than changed.
  Deployed, probed, re-ran the check live: all page-level checks pass.
  `scripts/mobile-qa.mjs` run pending against both live pages, all 8 viewports.
