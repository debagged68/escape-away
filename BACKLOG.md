# Escape Away — Performance backlog

## P1 — Public website image loading and page responsiveness (2026-10-20)

**User report:** Property photographs appear/render slowly, and page activity could feel faster. Applies to the public website, **not** Content Manager or Review Manager.

**Status:** Open. Repository code inspected; no live Lighthouse/real-device timings collected yet, so the following are hypotheses and recommended actions, not verified performance measurements.

### Measure first
- Run PageSpeed Insights/Lighthouse mobile and desktop on the home page and representative deeper pages; capture LCP, INP, CLS, TTFB, total transferred image bytes, JS bytes, and largest network requests.
- Use a throttled mobile connection and a real iPhone; inspect cold and warm cache and interactions (navigation, gallery, scroll, any interactive maps).
- Record baseline screenshots and timings before changing the site's design.

### Acceptance criteria
- Mobile LCP <= 2.5 s (75th percentile, where field data is available); INP <= 200 ms; CLS <= 0.1.
- Visibly faster initial photographic content and responsive page activity on a mid-range iPhone over mobile data.
- Preserve correct images, crops, accessibility, copyright credits, SEO and content.
- No layout regressions, broken routes, or excessive preload competition.
- Publish measured before/after changes to the backlog and verify on the deployed AWS Amplify URL.

### Findings from code inspection
- Homepage is one static `index.html` with inline CSS and no JavaScript. This is a strong baseline for page interactivity; heavy JS is unlikely to be the primary source of delay.
- Two photographs use plain `<img>` tags: `assets/oast-cottage.jpg` (976x732) has `fetchpriority="high"`; `assets/windwhistle.jpg` (1500x1125) has neither `loading="lazy"` nor `decoding="async"`.
- Both photos have explicit `width`/`height` attributes, which helps reserve space. Neither has `srcset`/`sizes`, so mobile phones may download the same full-size image as desktop.
- Property photograph hover transitions use CSS transforms; these are relatively lightweight but should be checked for reduced-motion accessibility.
- No runtime React hydration on this site, so first priority should be image encoding and delivery rather than rewriting the page framework.

### Recommended work (in priority order)
1. Measure actual byte sizes and timings for `assets/oast-cottage.jpg` and `assets/windwhistle.jpg` in the deployed site.
2. Generate optimised AVIF/WebP variants at mobile/tablet/desktop widths; use `<picture>` or `srcset` with appropriate `sizes` and a JPEG fallback, maintaining crop/alt text.
3. Retain high priority only for the image confirmed to be LCP. Add `decoding="async"` and `loading="lazy"` to genuinely offscreen images; do not lazy-load the actual LCP image.
4. Audit cache headers for assets deployed through Amplify CDN; use long-lived immutable caching with content-hashed asset names, or shorter TTLs when image filenames remain stable.
5. Check image height/crop and CSS transitions on iPhone; respect `prefers-reduced-motion`.
6. Avoid adding heavyweight scripts/frameworks as a 'performance fix'; this static page should remain lightweight.
