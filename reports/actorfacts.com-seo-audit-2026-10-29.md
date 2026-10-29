# SEO Audit Report

**Site**: actorfacts.com (WordPress)
**Date**: 2026-10-29
**Pages analyzed**: 35 indexed URLs, seen through search results (no direct crawl)
**Overall score**: **~45/100 (provisional)**. That band means "critical SEO issues". The score covers only what could be observed. About half the checklist could not be verified (see [Not verified](#not-verified)).

## How this audit was done

- **No direct crawl.** The audit environment's network policy blocks `actorfacts.com`, so I couldn't read raw HTML, response headers, `robots.txt`, the sitemap or page speed.
- **No Semrush data.** The connected Semrush account has no API units left, so its Site Audit, Domain Overview and Organic reports returned nothing.
- **What the findings rest on:** 10 `site:` and topic searches, using the titles, URLs, snippets and structured data that search engines have stored for the site. That shows how search engines currently see the site. It is a sample, not a full crawl.

## Critical issues (must fix)

- [ ] **Duplicate URLs indexed through AMP.** `?amp=1` versions of pages are indexed alongside the normal URLs, e.g. [`/kajal-aggarwal-biography-…-actorfacts/?amp=1`](https://actorfacts.com/kajal-aggarwal-biography-age-height-weight-family-career-filmography-controversies-more-actorfacts/?amp=1). Either the AMP page's canonical doesn't point to the normal URL, or the normal page lacks `rel="amphtml"`.
  **Fix:** Google no longer favours AMP, so the simplest option is to turn off the AMP plugin (or its "Paired/Reader" mode) and 301 `?amp=1` to the clean URL. If you keep AMP, make sure each AMP page has `<link rel="canonical">` pointing to the normal URL.
- [ ] **The same category is indexed under two URLs.** Both [`/uncategorized/`](https://actorfacts.com/uncategorized/) and [`/category/uncategorized/`](https://actorfacts.com/category/uncategorized/) are indexed. The category base was probably removed at some point (a Rank Math/Yoast "strip category base" setting) and the old URLs never got redirected.
  **Fix:** choose one structure and 301 the other, then set Uncategorized to `noindex` (or move its posts into real categories and delete it).
- [ ] **Thin archive pages compete with the biographies.** Pages such as [`/kajol/`](https://actorfacts.com/kajol/), [`/delna-davis/`](https://actorfacts.com/delna-davis/), [`/avneet-kaur/`](https://actorfacts.com/avneet-kaur/), [`/anveshi-jain/`](https://actorfacts.com/anveshi-jain/), [`/mamitha-baiju/`](https://actorfacts.com/mamitha-baiju/), [`/deepti-sati/`](https://actorfacts.com/deepti-sati/), [`/sonal-chauhan/`](https://actorfacts.com/sonal-chauhan/), [`/trupti-ravindra/`](https://actorfacts.com/trupti-ravindra/) and [`/kushitha-kallapu/`](https://actorfacts.com/kushitha-kallapu/) are lists of gallery posts (tag archives with the base removed, it appears) with no unique text. Where a biography also exists, the two pages compete for the person's name, and neither ranks. Earlier tests found ActorFacts in the top ~10 for 0 of 7 actor-name queries.
  **Fix:** for each person, make **one** indexable page. Either (a) add 150–300 words of unique intro text to the tag archive and link to the biography, or (b) `noindex, follow` tag archives and link the galleries from the biography.
- [ ] **Ages are fixed text and already wrong.** The Rashmika Mandanna biography shows "Age: 29 Years". Born 5 April 1996, she is 30. Every biography with a fixed age goes stale on the subject's birthday, which undermines trust (and E-E-A-T).
  **Fix:** compute ages from `birthDate` with a shortcode or theme template, and show "as of {current date}".

## Warnings (should fix)

- [ ] **Titles are far too long.** Biography titles run to about 93 characters before the brand suffix, e.g. "Kriti Sanon Biography, Age, Height, Weight, Family, Career, Filmography, Controversies & More". Google cuts titles at about 60 characters, so everything after "Career" is lost.
  **Fix:** `{Name} Biography: Age, Height, Family & Movies` (≈45–58 characters), with the SEO plugin adding ` - ActorFacts`.
- [ ] **Slugs are very long, and the brand appears twice.** E.g. `/kriti-sanon-biography-age-height-weight-family-career-filmography-controversies-more-actorfacts/` (95 characters). The same template is used on Priyanka Chopra, Kajal Aggarwal, Soundarya Sharma, Pragya Jaiswal, Rashmika Mandanna, Jacqueline Fernandez and Amala Paul.
  **Fix:** for new posts, use `/{name}-biography/`. For existing ones, change the slug **only with a 301** from the old URL (Rank Math and Yoast Premium do this automatically, or use the Redirection plugin). Don't break URLs that already rank.
- [ ] **Three different biography templates.** (A) "…Biography, Age, Height, Weight, Family, Career, Filmography, Controversies & More", (B) "…Biography: Age, Height, Weight, Body Measurements, Affairs, Family", (C) "Prabhas Biography: Pan-Indian Star & Baahubali Legend". Keyword-stuffed patterns (A) and (B) look like the low-trust competitor sites. Pattern (C), a real description, is the best.
- [ ] **Brand suffix used inconsistently on titles.** Some indexed titles end in "- ActorFacts", but others don't ("Preity Mukhundhan Stuns in Maroon Dress", "Anushka Sen Shimmery Yellow Dress", all the Pattern A biographies). Set one title template in the SEO plugin for each post type.
- [ ] **The Cast & Crew section has no cast or crew content.** [`/cast-crew/`](https://actorfacts.com/cast-crew/) lists photoshoots and biographies, but no film cast lists or crew pages. The homepage title promises "Movie Cast and Crew, Cinema News". Either build that content (film pages with `Movie` schema and cast lists) or remove it from the title and navigation.
- [ ] **Content is mostly gallery posts.** Most recent posts are photoshoot galleries ("…Stuns in Black Saree and Golden Blouse Photos"). They have little text, attract little search demand outside image search, and put the site in a spam-heavy search space. Celebrity photos are also usually copyrighted, so check that you have the rights to use them.
- [ ] **No Hollywood or Bollywood category pages are indexed**, though the navigation lists them. Only [`/photos/kollywood/`](https://actorfacts.com/photos/kollywood/) and [`/photos/sandalwood/`](https://actorfacts.com/photos/sandalwood/) appear. Check that those categories have posts and aren't set to `noindex` by mistake.
- [ ] **Possibly stale publishing.** The newest posts in the indexed homepage are dated 7 July 2026. If nothing has gone up since, a regular schedule (even 2–3 good biographies a week) matters more than anything else on this list.
- [ ] **Personal Gmail in the Organization schema.** `"email": "techroots91@gmail.com"` is exposed in the homepage JSON-LD. Use a domain address.

## Opportunities (nice to have)

- [ ] **Add `Person` schema to biographies.** The pages currently carry `Article` schema (articleSection "Actress, Biography, …"). Add a `Person` entity with `birthDate`, `birthPlace`, `jobTitle`, `image`, and `sameAs` (Wikipedia, IMDb, Wikidata, official Instagram), and wrap it in `ProfilePage`. The `/searchfit-seo:schema-markup` command can generate this.
- [ ] **Add FAQ sections** on biographies ("How old is…", "What is … 's first movie?"). They're useful for AI answers and People Also Ask, even without FAQ rich results.
- [ ] **Link galleries and biographies to each other.** Every gallery post should link to that person's biography, and each biography should link to their latest galleries.
- [ ] **Quick Facts table with sources** at the top of each biography, plus a "Last verified" date.
- [ ] **Turn Hollywood, Bollywood, Kollywood etc. into proper hubs**, with an intro, a table of featured biographies and links to the newest galleries, rather than bare post lists.
- [ ] **Strengthen the About page**: name the editor or authors, explain how facts are verified, and add a corrections policy and contact details. Create author pages.

## Passing

- The site is indexed: the homepage, the main sections and many biographies are in search results.
- Breadcrumbs are in place (Home › Biography › Actress), as seen in the structured data.
- Article and Organization JSON-LD are present (an SEO plugin is outputting schema).
- Biographies include filmography tables (year, film, language), which suit rich results and AI extraction.
- The homepage title and description are clear and descriptive.
- The photo categories are grouped sensibly by film industry (Kollywood, Sandalwood, etc.).

## Not verified

These need direct access (allow `actorfacts.com` and `www.actorfacts.com` in the session's network settings) or Semrush API units:

- [ ] `robots.txt` contents and any AI or search bot blocks
- [ ] Whether `sitemap.xml` exists, what it covers, and whether AMP and tag URLs are excluded
- [ ] `www` → apex redirect, HTTPS redirect, status codes
- [ ] Canonical tags on normal, AMP and paginated URLs
- [ ] Meta description length and uniqueness on each page
- [ ] Open Graph and Twitter Card tags
- [ ] H1 count and heading hierarchy
- [ ] Image `alt` text, formats (WebP/AVIF), width/height, lazy loading
- [ ] Core Web Vitals, render-blocking CSS/JS, ad scripts
- [ ] Broken internal links, orphan pages, links per page
- [ ] Mobile layout, tap targets, font size, contrast

## Priority order

1. Fix the AMP duplicates and the duplicate Uncategorized URLs (an hour in plugin settings plus redirects).
2. Decide one URL per person; `noindex` or improve the thin tag archives.
3. Switch fixed ages to calculated ages.
4. Shorten title templates in the SEO plugin. The site-wide change takes minutes.
5. Add Person schema and link galleries and biographies to each other.
6. Restart regular publishing, with a focus on emerging South Indian actors, where competition is weakest.
