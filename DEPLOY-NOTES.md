# Rugby Code, deployment notes

Live now at: https://businessboosterlk.github.io/rugbycode/

## Why no CNAME yet (do not add one blindly)
rugbycode.co.nz already serves a LIVE site (nginx, HTTP 200, checked 2026-07-16).
Committing a CNAME file would break the github.io URL before DNS moves, and moving
the domain is Aaron's business decision. Ship on the subpath first, upgrade later.

## Custom-domain upgrade path (when Aaron says go)
1. Aaron sets these DNS records at his registrar (send him this block):
   - For the apex `rugbycode.co.nz`, four A records:
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
   - For `www.rugbycode.co.nz`, one CNAME record pointing to:
     businessboosterlk.github.io
2. We add a file named `CNAME` (content: `rugbycode.co.nz`) to this repo root and
   set the custom domain + Enforce HTTPS in the repo's Pages settings.
3. Then swap the SEO base URL across the site (canonical, og:url, og:image, all
   JSON-LD @id/url values, sitemap.xml, llms.txt) from
   `https://businessboosterlk.github.io/rugbycode/` to `https://rugbycode.co.nz/`,
   and add root robots.txt (allow all + AI crawlers, link the sitemap).
   Note: his current hosting will stop serving the old site once DNS moves.

## Launch checklist (whoever runs it)
- [ ] Google Search Console: verify the property, paste the verification code into
      the commented `google-site-verification` slot in index.html, redeploy.
- [ ] Submit sitemap.xml directly in Search Console (subpath sites cannot use a
      robots.txt sitemap link; direct submission is the correct route).
- [ ] GA4: create the property, paste the gtag.js snippet into the commented GA4
      slot in index.html, redeploy.
- [ ] Confirm with Aaron: the four stat-bar numbers (500+ players, 50+ coaches,
      12 countries, 15+ years) and the six testimonials came from his existing
      site file; get his written OK that they are accurate before any paid promo.
