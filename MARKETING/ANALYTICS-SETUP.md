# Analytics Setup — Goldy Brown

Implements the `analytics-tracking` skill. The point is to measure what matters and ignore what doesn't.

## What to install (in order)

### 1. Google Search Console (required, free)
The single most important tool. Tells you what queries actually surface goldybrown.com.

**Setup:**
1. Go to https://search.google.com/search-console
2. Add property → Domain → `goldybrown.com`
3. Verify via DNS TXT record (your registrar) or HTML file at root
4. Submit sitemap: `https://goldybrown.com/sitemap.xml`
5. Submit URL inspection requests for the top 10 commercial pages

**Check weekly:**
- Performance tab → Queries (sorted by impressions). Where are we showing up?
- Pages → Top pages. Which earn the clicks?
- Coverage → any errors?

### 2. Bing Webmaster Tools (free, 5 minutes)
Bing-and-DuckDuckGo combined are still ~10% of search. Often easier to rank in Bing.

**Setup:** https://www.bing.com/webmasters → Import from Search Console (one-click).

### 3. Plausible Analytics (paid, simple) OR Google Analytics 4 (free, complex)

**Plausible recommendation:**
- $9/mo for goldybrown.com
- Cookie-free, GDPR-friendly, no banner needed
- Shows you the 5 things that actually matter: visits, sources, top pages, top countries, conversions
- Add this snippet to `index.html` and every static page in the `<head>`:

```html
<script defer data-domain="goldybrown.com" src="https://plausible.io/js/script.js"></script>
```

**If you prefer GA4:**
- Free, more granular, more complex
- Setup: https://analytics.google.com → Create property → Data Stream → Web → goldybrown.com
- Get the Measurement ID (G-XXXXXXXXXX) and add this to every page:

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-XXXXXXXXXX', {anonymize_ip: true});
</script>
```

GDPR note: GA4 in the EU/UK requires a consent banner. Plausible doesn't.

### 4. Microsoft Clarity (free, optional)
Heatmaps + session recordings. Useful for the first few months to see how people actually use the site.
https://clarity.microsoft.com — free, no usage limits.

---

## Events to track

If using GA4 or Plausible, fire custom events on these clicks:

| Event | Where | Why |
|-------|-------|-----|
| `cta_holster_buy` | Holster purchase button on every page | Primary conversion |
| `cta_hotel_email` | Hotel Programme email links | B2B lead |
| `cta_corporate_email` | Corporate gift email links | B2B lead |
| `cta_wedding_email` | Wedding gift email links | High-intent retail |
| `cta_journal_subscribe` | RSS link | Engagement |
| `quiz_complete` | Find Your Piece result page | Engaged visitor |
| `outbound_instagram` | Instagram link clicks | Social funnel |

**Implementation example (works with both Plausible and GA4):**

```html
<a href="/" data-event="cta_holster_buy" onclick="trackEvent('cta_holster_buy')">Shop the Holster</a>

<script>
function trackEvent(name){
  if (window.plausible) plausible(name);
  if (window.gtag) gtag('event', name);
}
</script>
```

---

## What to measure (and what to ignore)

### Measure
- **Organic search clicks/week** (Search Console). The top of the funnel.
- **Top 20 ranking queries.** Where you're winning, where the gap is.
- **Hotel Programme email clicks/week.** The B2B pipeline.
- **Holster CTA clicks → cart adds → purchases** (conversion rate).
- **Top pages by entrances + bounce rate.** Pages with 80%+ bounce need work.
- **Time on /journal/ articles.** If under 30 seconds, the article isn't landing.

### Ignore
- Total pageviews. Vanity number.
- Bounce rate alone, without context. A glossary page bouncing is fine.
- Real-time visitors. A live counter is for theatre.
- "Average session duration" — heavily skewed by long tabs left open.

---

## Reports to build

### Weekly (15 minutes, every Monday)
- Search Console: top 10 new queries surfacing this week
- Plausible/GA4: total visits week-over-week, top entry pages
- Hotel + corporate inbox: any new programme leads

### Monthly (45 minutes)
- Top 50 keywords ranked, week-1 vs week-4 movement
- Pages added vs pages indexed (Search Console)
- Conversion rate: organic visits → email/CTA
- Geographic breakdown — which cities are warming up

### Quarterly (2 hours)
- Full content audit: which journal pieces drove the most search clicks
- Drop the bottom 10% of pages (no traffic, no purpose) or rewrite them
- Plan next quarter's content calendar based on what's working
- Backlink check via Ahrefs free tier or Search Console — who's linking?

---

## Goal-setting (concrete numbers)

A young brand's first 12 months on a content engine like this typically looks like:

| Month | Organic search visits/mo (target) |
|-------|-----------------------------------|
| 1 | 50 |
| 3 | 250 |
| 6 | 1,000 |
| 9 | 3,000 |
| 12 | 8,000-15,000 |

These are realistic ranges, not guarantees. Hotel Programme leads compound differently — one signed property is worth ~10K retail visits.

---

## What the analytics will tell you (honestly)

After 90 days you'll know:
1. Which 5-10 pages are doing the heavy lifting (concentrate further work here)
2. Which 10-20 pages should be deleted or merged
3. Which 3-5 keywords are 1 page away from the top 5 (build a topic cluster around them)
4. Whether the hotel programme is generating qualified leads or just GETs to the page

If after 90 days the analytics tell you something *different* — listen to that.
