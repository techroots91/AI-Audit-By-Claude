# AI Visibility Audit: actorfacts.com

**Date:** 2026-10-10
**Target:** www.actorfacts.com (indexed as `https://actorfacts.com/`)
**Scope:** How likely AI answer engines (ChatGPT search, Perplexity, Google AI Overviews, Claude, Copilot) are to find, trust and cite ActorFacts.

## Method and limits

- **Direct crawl: not possible.** The audit environment's network policy blocked outbound connections to `actorfacts.com`, so I could not read raw HTML, `robots.txt`, `llms.txt`, the sitemap, JSON-LD, response headers or page speed. Those checks are listed under [Still to verify](#still-to-verify-needs-direct-access).
- **What was done:** 17 web searches (one US search index), covering `site:` queries, brand queries, and the queries a real user would type for people ActorFacts covers. Each search returns roughly the top 9–10 results. These are point-in-time samples, not rank tracking.

## Summary

| Area | Status |
|---|---|
| Indexed by search engines | Yes. The homepage, category pages, profiles and biographies are all indexed. |
| Shows up for its own brand name ("ActorFacts") | No. Generic "actor facts" trivia pages (Britannica, Ranker, IMDb) come up instead. |
| Shows up for people it covers (7 tested) | 0 of 7 in the top results. |
| Entity/brand signals | Weak. No third-party mentions turned up, and the brand name is a generic phrase. |
| Content freshness | Risky. Pages are about 300–530 days old and give ages as fixed text. |
| Template consistency | Inconsistent title and slug patterns. Some include a redundant "-actorfacts". |
| Overall AI visibility | **Low.** The site is indexed but not cited. Competitors win every query tested. |

## Findings

### 1. The site is indexed, but on the apex domain, not `www`

Every indexed URL is `https://actorfacts.com/...`. The `www.` host you supplied never showed up in results. Confirm that `www.actorfacts.com` returns a **301** to `https://actorfacts.com/` (or the other way round), and that `<link rel="canonical">` uses the same host on every page. Inconsistent hosts split signals between two URLs and confuse citation de-duplication.

Indexed sections seen:
- `/` (title: "ActorFacts - Actor, Actress Biographies, Photos, Movie Cast and Crew, Cinema News")
- `/about/`, `/biography/`, `/photos/`, `/photos/kollywood/`
- `/category/uncategorized/`, the WordPress default category (should not be indexed)
- Profile/gallery pages: `/kushitha-kallapu/`, `/sonal-chauhan/`, `/trupti-ravindra/`
- Biography posts: `/prabhas-biography-pan-indian-star-baahubali-legend/`, `/mahesh-babu-biography-.../`, `/vennela-kishore-biography-.../`, `/niharika-nm-biography-.../`, `/kriti-sanon-biography-...-actorfacts/`, `/priyanka-chopra-biography-...-actorfacts/`

### 2. ActorFacts loses every person query tested

| Query | Who ranked instead | ActorFacts in top results? |
|---|---|---|
| Kushitha Kallapu biography age movies | thecityceleb.com, technosports.co.in (×7) | No |
| Sonal Chauhan biography age height movies | Wikipedia, tring.co.in, thecityceleb, wikibio.in, starsunfolded | No |
| Trupti Ravindra actress biography | Nobody. The engine said it "couldn't find" this person. | No (even though `/trupti-ravindra/` is indexed) |
| Vennela Kishore biography age height family | wikibio.in, thecityceleb, starsunfolded | No |
| Niharika NM biography age height family | starsunfolded, wikibio.in, scraper sites | No |
| Prabhas biography pan-Indian star Baahubali | Wikipedia, Outlook India, Moviebuff, AceShowbiz | No |
| Kriti Sanon biography age height weight… | thecityceleb, successcds, scraper sites | No |

Takeaways:
- **The Trupti Ravindra result matters most.** No other site competes for this name, yet the engine still answered "couldn't find any results". The page is indexed but carries too little text or too few signals to be retrieved. The site search summary described the profile pages as "short photo-gallery teasers rather than biographical detail." **Thin gallery pages do not get cited.**
- For mid-tier Telugu and Kannada names, the competition is beatable: wikibio.in, starsunfolded and thecityceleb are templated sites. The AI answers repeatedly flagged them as "low-quality" with "conflicting details". **A site that gives verified, sourced, dated facts can displace them.**
- For A-list names (Prabhas, Priyanka Chopra, Kriti Sanon, Mahesh Babu), Wikipedia, Outlook and IMDb hold the top results. Competing there is low ROI.

### 3. The brand has no entity footprint

A search for **"ActorFacts"** returned no ActorFacts pages. Results were Britannica "facts" pages, Ranker's "Fascinating Actor Facts", IMDb trivia and scraper sites. AI engines decide whom to cite partly by recognizing a named entity across sources, and no third-party mentions of ActorFacts showed up.

### 4. Ages are frozen in text and go stale

Search metadata showed ActorFacts biography pages last updated about 300–530 days ago. An age written as text ("age 26") is wrong a year later. While answering, the AI engines kept recalculating ages and pointing out stale figures on competing sites. Pages with stale facts get distrusted.

### 5. Titles and slugs follow two different templates

- Template A: `Niharika NM Biography: Age, Height, Weight, Body Measurements, Affairs, Family - ActorFacts`
- Template B: `Kriti Sanon Biography, Age, Height, Weight, Family, Career, Filmography, Controversies & More` (slug ends in `-actorfacts`, so the brand appears twice)
- Template C: `Prabhas Biography: Pan-Indian Star & Baahubali Legend - ActorFacts`
- Profile pages: `/sonal-chauhan/`, with the bare name and no "biography".

The long keyword-list titles ("Body Measurements, Affairs") look like the scraper sites, which have the least trust. Template C (a real description) is the strongest.

### 6. The contact email in structured data is a personal Gmail address

Search snippets show the homepage JSON-LD carries `{"name":"ActorFacts","email":"techroots91@gmail.com"}`. That is good because it exposes Organization data. But a free-mail address is a weak trust signal for a publisher, and it invites scraping. Use a domain address (e.g. `editor@actorfacts.com`).

### 7. Photo galleries are a weak, risky content type

The `/photos/` hub (Tollywood, Bollywood, Mollywood, Sandalwood, Kollywood, Hollywood) competes in a search space full of spam and explicit-content scraper domains. AI engines don't cite image galleries for factual answers. They may also discount a site sitting in that neighbourhood. Celebrity photos are often copyrighted, so check the licensing or source of each image.

## Recommendations (priority order)

### P0: this week
1. **Fix host consistency.** Make `www` → apex a 301 (or the reverse), set self-referencing canonicals, and use the same host in the sitemap and in Search Console.
2. **Check that AI crawlers aren't blocked.** In `robots.txt`, check for rules (from a security plugin, Cloudflare "Block AI bots", or a hosting default) that block `GPTBot`, `OAI-SearchBot`, `ChatGPT-User`, `PerplexityBot`, `ClaudeBot`, `Claude-SearchBot`, `Google-Extended`, `Bingbot` or `Applebot-Extended`. Allow them unless you have a reason not to. In Cloudflare, also check *Security → Bots → AI Scrapers and Crawlers*.
3. **Noindex `/category/uncategorized/`** and any tag or archive pages with fewer than ~3 posts.
4. **Submit the sitemap to Google Search Console and Bing Webmaster Tools.** ChatGPT search and Copilot draw on Bing's index, so Bing indexing matters directly for AI visibility.

### P1: next 30 days
5. **Merge the thin profile pages into biographies.** Each person should have one canonical URL with ≥600 words of original content. 301 the gallery-only version into it, or link the gallery as a section. Start with names where competition is weak: Trupti Ravindra, Kushitha Kallapu and other emerging Telugu/Kannada actors.
6. **Add a "Quick Facts" block at the top of every biography.** AI engines extract answer-shaped content, so give them a table like this:

   | Field | Value | Source |
   |---|---|---|
   | Full name | … | Interview / official handle |
   | Born | 19 Oct 2002, Hyderabad | … |
   | Debut film | … (2023) | … |
   | Height | 5′5″ (165 cm), as reported | … |

   Show a "Last verified: <date>" line, and cite a source for each claim (official Instagram, a press interview, the production house).
7. **Compute ages from birth date** (shortcode or template), never as fixed text.
8. **Add `Person` JSON-LD** to every biography: `name`, `alternateName`, `birthDate`, `birthPlace`, `jobTitle`, `image`, `sameAs` (Wikipedia, IMDb, Wikidata, official Instagram/X). Wrap it in `ProfilePage` with `dateModified`. Add `Article` with a named `author` (`Person`, with an author page).
9. **Standardize titles on one pattern:** `{Name}: Biography, Age, Movies & Family | ActorFacts`. Drop "Body Measurements" and "Affairs", and remove `-actorfacts` from slugs (with 301s).
10. **Add an FAQ section** answering real questions ("How old is X?", "What was X's first movie?", "Is X married?"). Keep the answers short and self-contained.

### P2: 60–90 days
11. **Build entity signals.** Fill out the About page (who writes it, editorial policy, how facts are verified, corrections policy). Add `Organization` schema with `logo`, `sameAs` to the site's social profiles, and a domain email. Create consistent social profiles under the "ActorFacts" name.
12. **Earn mentions.** Get coverage on Telugu/Kannada film news sites, and in Reddit or Quora answers where you cite your own verified fact sheets. AI engines weigh third-party corroboration.
13. **Publish `/llms.txt`** listing your best biography hubs and what the site covers. It's low effort, though its effect is still unproven.
14. **Add a corrections and update log** to each biography ("Updated Oct 2026: added *Indian Penal Law* (2025)"). This shows freshness to both crawlers and readers.
15. **Track progress monthly.** Re-run the seven queries above in ChatGPT search, Perplexity and Google, and record whether ActorFacts is cited.

## Still to verify (needs direct access)

These could not be checked from the audit environment:

- [ ] `robots.txt` contents and AI-bot rules
- [ ] `/llms.txt` exists
- [ ] `sitemap.xml` / `sitemap_index.xml`: coverage, `lastmod` accuracy
- [ ] `www` → apex redirect status and canonical tags
- [ ] JSON-LD present on biography pages (Person/Article/Breadcrumb)
- [ ] Whether content is in the server-rendered HTML (not injected by JS)
- [ ] Core Web Vitals / TTFB, especially on image-heavy gallery pages
- [ ] Cloudflare or a WAF challenging bots (403s for crawler user agents)
- [ ] Image alt text and file names on gallery pages

To run these, allow `actorfacts.com` and `www.actorfacts.com` in the cloud environment's network settings, then re-run the audit.
