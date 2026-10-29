# SEO Audit Report

**Site**: https://actorfacts.com/ (WordPress 7.1.4, All in One SEO 5.0.3, LiteSpeed Cache, Hostinger)
**Date**: 2026-10-29
**Pages analyzed**: 986. That is every URL in the XML sitemap: 766 gallery and other posts, 28 biographies, 171 tag pages, 15 categories and 6 pages. All were crawled live.
**Overall score**: **60/100**. That band means "needs significant work". The technical foundation is solid, but meta data, thin pages and internal linking hold the score down.

> This version replaces the search-index-only draft from earlier today (still in git history). The live crawl corrected several draft findings:
> - `?amp=1` pages already canonicalize to the normal URL.
> - `/category/uncategorized/` already 301s to `/uncategorized/`.
> - Biography ages now read correctly (Rashmika Mandanna: 30).
> - Biography titles have already been shortened.
> - `Person` schema is already in place.

## Score breakdown

| Area | Score | Notes |
|---|---|---|
| Crawlability & indexation | 10/15 | robots.txt, sitemap, llms.txt and 404s are fine. Paginated archives are `noindex, nofollow`, and 171 thin tag pages are indexed. |
| Meta tags & head | 7/15 | 659 titles over 60 characters. 214 pages lack a meta description and 168 have one that's too long. Every post shares the logo as its `og:image`. |
| Headings | 9/10 | Exactly one H1 on all 986 pages. |
| Images | 5/10 | 99% have alt text, but 42% use generic "(n)" alts. 63% lack width/height, only 17% are WebP, and the main image is lazy-loaded. |
| Performance | 7/10 | Good caching and TTFB. LCP is 1.8–4.2 s on throttled mobile. |
| Structured data | 8/10 | BlogPosting, Person (with birthDate and sameAs), Breadcrumb and ProfilePage are all present. Small conflicts remain. |
| Internal linking | 8/15 | 144 of 171 tag pages link to no biography. The homepage has 420 links, repeating the same 4–5 posts. |
| Mobile & accessibility | 3/5 | 16px body text and no horizontal scroll. Many tap targets are under 24px tall. |
| Content quality / E-E-A-T | 3/10 | 96% of posts are photo galleries. 289 posts have under 150 words. Nothing has been published since 7 July 2026. |

## Critical issues (must fix)

- [ ] **Paginated archives are `noindex, nofollow`.** E.g. `https://actorfacts.com/page/2/` and `https://actorfacts.com/photos/page/2/`. With 794 posts, the only internal path to older posts runs through these pages, and `nofollow` tells Google not to follow it. Older galleries and biographies then depend on the sitemap alone.
  **Fix:** in AIOSEO → Search Appearance → Advanced, switch "No-index paginated pages" to `noindex, follow`, or remove it. Never use `nofollow` on archive pagination.
- [ ] **171 tag pages are indexed with almost no unique content.** They are listed in `post_tag-sitemap.xml` and indexable. 114 have an "About {name}" block, but it is only about 20 words (median). 57 have none. None has a meta description or Open Graph tags, and **144 of 171 don't link to that person's biography**. Each one competes with the biography and gallery posts for the person's name.
  **Fix (choose one per person):**
  - (a) *Make the tag page the person's hub.* Write a 150–300-word intro, a Quick Facts table, a link to the biography, then the galleries. Add a meta description.
  - (b) *Hide it.* Set tag archives to `noindex, follow` in AIOSEO → Search Appearance → Taxonomies → Tags, and remove tags from the sitemap.

  Option (a) suits the roughly 28 people with biographies. Option (b) suits the rest.
- [ ] **Thin gallery posts make up most of the site.** 766 of 794 posts are photo galleries. Their median content is about 200 words, and 289 posts have under 150 words. At this ratio Google's helpful-content systems may treat the whole site as low-value. Some titles, e.g. `/tanya-maniktala-candid-with-wet-hair-in-maroon-towel/`, also risk SafeSearch filtering for the domain.
  **Fix:** add 150–250 words of real context to each new gallery (the event, the film, the photographer or source, and a link to the biography). Merge or `noindex` near-identical galleries. Shift the publishing mix towards biographies, film pages and reviews.
- [ ] **No new posts since 7 July 2026.** `post-sitemap.xml` was last modified on 2026-07-07, and no post has a newer `dateModified`. Sixteen weeks of silence on a news and celebrity site hurts crawl frequency and rankings.
  **Fix:** set a steady schedule, e.g. 3 biographies or film pages and 5 galleries a week, and update older biographies (filmography, awards).

## Warnings (should fix)

- [ ] **Every post shares the site logo as `og:image`.** All 794 posts and 6 pages use `cropped-ActorFactor-Logo-2.png`, so every Facebook, WhatsApp, X and Pinterest share shows the logo instead of the actress or actor. This is a big loss of click-through for a photo site.
  **Fix:** AIOSEO → Social Networks → Facebook → "Default Post Image Source" = **Featured Image** (or "First image in content"), and do the same for Twitter. Tag and category pages (186) have no `og:image` at all.
- [ ] **214 pages are missing meta descriptions:** all 171 tags, 42 posts and 1 category. Set an AIOSEO template for tags, e.g. `#taxonomy_title biography, latest photos, movies and news on ActorFacts.`
- [ ] **8 biographies have auto-generated junk descriptions** built from their headings and Instagram embed text, e.g. Kriti Sanon: "Kriti Sanon Wiki Kriti Sanon Physical Stats Personal Life … View this post on Instagram A post shared by Kriti Sanon 🦋". Affected:
  - `kriti-sanon-…`
  - `deepthi-sunaina-…`
  - `jacqueline-fernandez-…`
  - `sai-pallavi-…`
  - `katrina-kaif-…`
  - `kajal-aggarwal-…`
  - `pooja-kannan-…`
  - plus 1 more

  Write a manual 140–155-character description for each.
- [ ] **168 meta descriptions are over 160 characters**, including 27 of 28 biographies. Rashmika Mandanna's is 209 and Prabhas's 199. Google truncates them.
- [ ] **659 titles are over 60 characters.** Gallery titles have a median of 67 and 311 are over 70 (max 98), e.g. "Deepika Pilli Looks Gorgeous in Pink Lehenga Latest Photos - ActorFacts" (71).
  **Fix:** shorter patterns such as `{Name} in Pink Lehenga: Latest Photos | ActorFacts`. Use the brand suffix on every post: some biographies (e.g. Kriti Sanon) drop it while others keep it.
- [ ] **The main image is lazy-loaded, which slows LCP.** LiteSpeed lazy-loads the first content image (the hero) on every post. On a throttled mobile test, the Prabhas biography reached **LCP 4.2 s**, the threshold for "poor". The LCP element was the lazy-loaded `Prabhas-4-683x1024.jpg`.
  **Fix:** in LiteSpeed Cache → Page Optimization → Media, enable **Viewport Images (VPI)**, or exclude the first content image from lazy load. Add `fetchpriority="high"` to the featured image.
- [ ] **Images:**
  - 7,875 of 12,588 content images (63%) lack `width`/`height`. Enable LiteSpeed "Add Missing Sizes".
  - Only 2,100 (17%) are WebP or AVIF. Enable LiteSpeed Image Optimization → "Image WebP Replacement" and run bulk optimization.
  - 5,274 alt texts are just the post title plus "(n)". Describe each photo instead, e.g. "Deepika Pilli in a pink lehenga at a studio photoshoot". Galleries live or die on image search, and descriptive alts are the main ranking signal there.
- [ ] **Duplicate and competing content:**
  - `/priya-shukla-sunset-beach-look-elegant-flow-dress-photos/` and `…-photos-2/` share the same title and description. Merge them and 301 one to the other.
  - Priyanka Chopra has **two biographies**, `/priyanka-chopra-jonas-biography-bollywood-to-hollywood-success-story/` and `/priyanka-chopra-biography-age-height-…-actorfacts/`. Merge them into one and 301 the other.
- [ ] **The homepage has 420 links that repeat the same 4–5 posts.** "Deepika Pilli Looks Gorgeous in Pink Lehenga" appears as an H3 in 8 sections, and the "Bollywood" and "Hollywood" blocks show the same Telugu photoshoots. Give each section its own category query, and cut the page to about 150 links.
- [ ] **The Uncategorized category is indexed and in the sitemap** (`/uncategorized/`). Assign its posts to real categories, then `noindex` or delete it.
- [ ] **The About page meta description is "Please contact us"** (17 characters), even though the page has a solid editorial section. Write a real description, e.g. "ActorFacts covers verified biographies, filmographies and photos of South Indian and Bollywood stars. Meet our team and editorial standards."
- [ ] **Personal Gmail in the Organization schema.** The schema includes `"email": "techroots91@gmail.com"`. Use a domain address such as `editor@actorfacts.com`, set in AIOSEO → General → Organization.

## Opportunities (nice to have)

- [ ] **Tag pages carry two competing JSON-LD blocks**: the AIOSEO graph says `CollectionPage`, and a second block says `ProfilePage`. Keep one, preferably `ProfilePage` with a `Person` mainEntity, and disable the other's schema output for tags.
- [ ] **Biographies are the strongest content (median 982 words), but there are only 28.** Scale them, starting with emerging Telugu and Kannada names where the competitors are weak templated sites.
- [ ] **Turn the movie pages into a real Cast & Crew section.** `/baahubali-the-beginning/` already has Cast and Crew sections but no meta description. Add `Movie` schema, a synopsis and links to each cast member's page.
- [ ] **Small tap targets on mobile**: 284 links or buttons on the homepage and 79–97 on posts are under 24px tall (Google's minimum is 24px and the target is 48px). Increase padding on footer, menu and tag links.
- [ ] **Empty-anchor internal links**: 8–30 per page, probably image-only links. Make sure each linked image has alt text, or add `aria-label`.
- [ ] **Curate `llms.txt`.** It exists (AIOSEO-generated) but lists the newest gallery posts. Put the biography hub, category hubs and top biographies first.
- [ ] **Homepage H1 is just "ActorFacts".** Use "ActorFacts: Actor Biographies, Celebrity Photos & Cinema News", which is more descriptive.
- [ ] **Move biographies to short slugs** (`/rashmika-mandanna-biography/`) with 301s. This is optional and only worth doing when a page is being reworked anyway, since the current titles are already good.

## Passing

- `robots.txt` is clean (only `/wp-admin/` blocked), lists both sitemaps, and blocks no search or AI crawlers. There's no Cloudflare in front of the site, which runs on Hostinger's CDN.
- The XML sitemap index exists, and **985 of 986 URLs return 200**. The one exception was a timeout that succeeded on retry. No broken URLs, no redirect chains.
- `llms.txt` exists.
- A proper **404** with `noindex` for missing pages. Search results pages are `noindex`. `/tag/x/` 301s to `/x/`.
- **Canonicals are self-referencing on all 986 pages.** AMP `?amp=1` variants point back to the clean URL.
- **Exactly one H1 on every page**, with no empty headings and a logical H2/H3 order on biographies (Wiki, Physical Stats, Family, Filmography, Awards).
- **Strong structured data on biographies**: `BlogPosting`, a `Person` entity with `birthDate`, `birthPlace`, `jobTitle`, `nationality` and `sameAs`, a named author (Ravi Varma), and `BreadcrumbList`.
- **Biography titles have been fixed** to "{Name} Biography: Age, Family, Career & Films" (50–66 characters), and ages now read correctly (Rashmika Mandanna: 30).
- **Good performance basics**: LiteSpeed page cache (HIT), 10KB used-CSS, only 1 external script (gtag) and no render-blocking JS. HTML is about 45–60KB compressed, with a 0.4–0.7 s warm TTFB. CLS is near 0 (0.001–0.067). The homepage LCP is 1.8 s on throttled mobile.
- **Mobile**: correct viewport, 16px body text, no horizontal scroll.
- **Twitter Card** (`summary_large_image`) and Open Graph tags are present on posts and pages.
- **Clear site architecture**: Photos → Tollywood, Kollywood, Mollywood, Bollywood, Sandalwood, Hollywood and Influencers; Biography → Actor and Actress; Reviews; Cast & Crew.

## Fix order

1. **Today, in AIOSEO settings (about 30 minutes):**
   - change pagination to `noindex, follow`;
   - set the social image to Featured Image;
   - add a meta description template for tags;
   - fix the About page description and the Organization email.
2. **This week:**
   - decide hub or `noindex` for tag pages;
   - merge the duplicate Priya Shukla and Priyanka Chopra pages;
   - rewrite the 8 junk biography descriptions;
   - turn on LiteSpeed VPI, Add Missing Sizes and WebP.
3. **This month:**
   - restart publishing;
   - add context text to galleries;
   - give each homepage section its own query;
   - write descriptive image alts for new galleries.
4. **Ongoing:**
   - expand biographies;
   - build the movie/Cast & Crew section with `Movie` schema.

## Method

All 986 sitemap URLs were fetched live and parsed for titles, descriptions, canonicals, robots meta, Open Graph, headings, content word count, images and JSON-LD. Spot checks covered redirects, AMP, pagination, 404s and search results. Lab vitals came from headless Chromium emulating a Pixel 5 (4× CPU throttle, 1.6 Mbps, 150 ms RTT) on the homepage, one biography, one gallery and one tag page. These are lab numbers from a non-Indian location. Real-user Core Web Vitals are in Google Search Console → Core Web Vitals.

**Not checked:**
- the `www.actorfacts.com` → `actorfacts.com` and `http` → `https` redirects (only the apex domain was allowed in the audit environment);
- backlinks;
- Search Console coverage data.
