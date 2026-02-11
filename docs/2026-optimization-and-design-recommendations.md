# 2026 recommendations for performance and visual improvements

## Current state (quick audit)

- The site uses Astro static rendering with MDX and sitemap integration, which is a strong baseline for performance.
- Main CSS is globally loaded with a classic blog typography setup.
- Blog list and post pages already use `astro:assets` images with explicit dimensions.
- Header and footer still contain template social links (Astro accounts), not brand links.
- The `site` URL in Astro config is still `https://example.com`.

## Priority 1 (high impact, low-medium effort)

1. **Set the real production domain in `astro.config.mjs`**
   - Why: fixes canonical, Open Graph URLs, sitemap, and RSS links for SEO and sharing.
   - 2026 trend: stricter social/search canonicalization and AI overviews rely on clean metadata.

2. **Implement modern image strategy (LCP-first)**
   - Keep first above-the-fold image eager/high-priority, lazy-load the rest.
   - Generate AVIF/WebP variants and use responsive sizes to reduce bytes on mobile.
   - 2026 trend: Core Web Vitals weighting and mobile-first image efficiency are still critical.

3. **Add critical CSS extraction strategy**
   - Keep base layout styles inline/minimal and defer non-critical decorative rules.
   - Reduce render-blocking CSS for first paint, especially on blog index.

4. **Enable font subsetting + modern format fallback**
   - Move to WOFF2 first and keep WOFF as fallback.
   - Subset to only used glyph ranges (Latin/Cyrillic as needed) to reduce transfer size.

## Priority 2 (high UX impact)

5. **Add color themes (dark/light/system) with design tokens**
   - Use CSS custom properties and `prefers-color-scheme` with manual toggle.
   - 2026 expectation: dark mode and system theme parity are standard.

6. **Upgrade visual language to a modern “editorial card” style**
   - Slightly larger whitespace rhythm, tighter line-length control, soft shadow scales, clearer CTAs.
   - Add consistent card treatment for post list items with subtle hover elevation.

7. **Improve navigation clarity**
   - Add sticky header on larger screens.
   - Add a visible “Latest post” or “Start here” CTA on home page.

8. **Replace template social links with real brand channels**
   - Improves trust and avoids bounce from irrelevant links.

## Priority 3 (content discoverability + engagement)

9. **Add structured data (JSON-LD)**
   - `WebSite`, `Blog`, `BlogPosting`, and `Person` schema where relevant.
   - 2026 trend: AI-assisted search surfaces structured entities more aggressively.

10. **Add related-post blocks and reading-time chips**
    - Improve session depth and internal linking.

11. **Create topic pages (tags/series)**
    - Better crawl paths and content clustering for technical/fantasy themes.

## Priority 4 (advanced performance)

12. **Adopt partial hydration/islands only where interactive UI is needed**
    - Keep most pages static, hydrate only specific components.

13. **Use edge caching strategy with immutable asset policy**
    - Long cache for hashed assets + smart revalidation for content pages.

14. **Add performance budgets in CI**
    - Fail builds if JS/CSS/image budgets exceed thresholds.

## Suggested phased roadmap

### Sprint 1 (1-2 days)
- Set real domain in Astro config.
- Replace template social links.
- Tune hero image loading and lazy strategy.
- Add basic dark mode token set.

### Sprint 2 (2-4 days)
- JSON-LD for blog/post pages.
- Typography + spacing polish for home/blog list.
- Related posts + reading time.

### Sprint 3 (ongoing)
- Font subsetting and image format automation.
- CI performance budgets and Lighthouse monitoring.
- Topic/series landing pages for content clustering.

## Success metrics to track

- LCP under 1.8s (mobile p75)
- INP under 150ms (mobile p75)
- CLS under 0.05
- +15-25% increase in pages/session after related posts and improved navigation
- Better social preview consistency after canonical/OG fixes
