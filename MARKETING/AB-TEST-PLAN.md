# A/B Test Plan — Goldy Brown

Implements the `ab-test-setup` skill. The first 8 tests to run, in priority order.

## The framework

A test only matters if it can change a real-money decision. For each test below, the expected outcome is in dollars or in a credible % lift.

**Tools:**
- Static-page tests: Vercel Edge Config, Cloudflare Workers, or just-roll-out-2-versions on alternating days
- Shopify product page: built-in Shopify A/B (or Intelligems for serious testing)
- Email: built into Klaviyo / Customer.io
- For honest stats: 95% confidence threshold, 7-day minimum run

**Sample size:** with traffic of <1,000 visitors/week, most A/B tests are inconclusive. Don't over-test until traffic justifies it. For now, run sequential tests (week 1 = version A, week 2 = version B) and compare cohort metrics.

---

## Test 1 — The Hotel Programme hero CTA wording

**Hypothesis:** "Request a sample kit" converts better than "See the tiers" because it commits the visitor to a clear next action.

**Variant A (current):** Two CTAs side by side — "Request a sample kit" + "See the tiers"
**Variant B:** Single CTA — "Request a sample kit (no cost)"

**Metric:** Click-through rate from hero → email
**Expected lift:** 15-25%
**Run:** 4 weeks (low traffic page)

---

## Test 2 — Holster homepage price display

**Hypothesis:** Showing the price next to the lifetime warranty (instead of standalone) reframes the price as "$249 forever" rather than "$249 today."

**Variant A:** "$249 USD" alone in the buy box
**Variant B:** "$249 USD · Backed for life. Free worldwide shipping."

**Metric:** Add-to-cart rate
**Expected lift:** 10-20%
**Run:** 2 weeks

---

## Test 3 — City landing page hero structure

**Hypothesis:** Leading with delivery speed converts better than leading with brand story.

**Variant A (current):** Brand-first lead — "Goldy Brown is a Vancouver-based leather atelier..."
**Variant B:** Delivery-first lead — "Free DHL/FedEx delivery to [city] in 3–5 business days. Full grain leather holsters from $249."

**Metric:** Scroll depth + outbound click to /
**Expected lift:** 20-30%
**Run:** 2 weeks per city, rotate through 7 cities

---

## Test 4 — Find Your Piece quiz placement

**Hypothesis:** Quiz placement on the homepage above the fold drives more conversions than buried in the footer.

**Variant A:** Quiz link only in nav and footer
**Variant B:** Inline "Not sure where to start? Take the 30-second recommender →" placed after the hero

**Metric:** Quiz starts + quiz completion rate + post-quiz CTA clicks
**Expected lift:** Quiz starts +200%, downstream conversions +5-10%

---

## Test 5 — Hotel Programme tier card CTA

**Hypothesis:** A direct-action CTA on each tier card converts better than the page-level CTA at the bottom.

**Variant A (current):** Tier cards are static; conversion CTA only at top and bottom of page
**Variant B:** Each tier card has its own "Request this tier sample" button

**Metric:** Hotel email enquiries with tier specified
**Expected lift:** 30-50% lift in qualified enquiries (filtered by tier specificity)
**Run:** 3 weeks

---

## Test 6 — Wedding gifts page recipient grid order

**Hypothesis:** "Groomsmen" first (the most-searched query) converts better than the current alphabetical/conventional ordering.

**Variant A:** Bride and groom → groomsmen → bridesmaids → ...
**Variant B:** Groomsmen → bridesmaids → bride and groom → parents → ...

**Metric:** Page time + email clicks to weddings@
**Expected lift:** 10-15%
**Run:** 4 weeks

---

## Test 7 — Email subject line: post-purchase referral ask

**Hypothesis:** "A favour, only if you're using it" beats a generic "Refer a friend" subject by a significant margin.

**Variant A:** "Refer a friend, get $50 off"
**Variant B:** "A favour, only if you're using it"

**Metric:** Open rate + click-to-referral-link rate
**Expected lift:** Open rate +25-40%, click rate +15-25%
**Run:** Send to 50% of post-30-day cohort each, 4-week sample

---

## Test 8 — Homepage above-the-fold copy density

**Hypothesis:** Less hero copy converts better at the luxury price point.

**Variant A (current):** Long-form descriptive lead with multiple sub-points
**Variant B:** Single-line lead — "A leather travel bag worn, not carried."

**Metric:** Scroll depth past hero, add-to-cart from hero CTA
**Expected lift:** 5-15%
**Run:** 4 weeks (homepage = highest traffic)

---

## What we're NOT testing (and why)

- **Pricing.** $249 is the floor for the unit economics. Don't test below it.
- **The lifetime warranty.** It's a brand commitment, not a marketing variable.
- **Made-in claims.** They're factual. We don't soften "made in South India" to test conversion.
- **Hot-stamp pricing.** "Free hot-stamp on every order" is a baseline; testing pulling it back damages the brand more than any conversion lift would justify.

---

## Sample-size reality check

To detect a 10% lift on a baseline 3% conversion rate at 95% confidence, you need roughly 10,000 visitors per variant. That's 20,000 visitors total per test.

If goldybrown.com is at 1,000 visits/week today:
- Test 1 (Hotel hero): 4 weeks × ~50 visits = 200 visitors per variant. Not enough for stats; treat as directional.
- Test 8 (Homepage): 4 weeks × ~500 visits = 2,000 per variant. Still under-powered, but useful for big lifts.

**Implication:** for the first 6-12 months, run **sequential tests** (week 1 = A, week 2 = B) instead of parallel splits. Compare full-week cohorts. Less rigorous statistically but actionable. Switch to proper A/B once traffic > 5,000/week.

---

## What to do with results

After each test:

1. **Document the result** in this file (add a "Results" section below the test).
2. **If winner is statistically meaningful (or directionally strong + traffic too low for stats):** ship the winning variant as the new baseline.
3. **If inconclusive after 4 weeks:** kill the test. Don't keep running indefinitely.
4. **If loser was the "obvious" choice:** that's the most valuable result. Document why your intuition was wrong.

## Test backlog (when the first 8 are done)

- Holster colour ordering on the swatch
- Hotel programme tier names ("Programme One/Two/Three" vs "Welcome/Suite/Signature")
- Free-tool quiz length (3 vs 5 vs 7 questions)
- "Designed in Vancouver" vs "Made in South India" headline emphasis
- Holster vs accessory featured on city pages
- Footer subscribe form copy ("Get the journal" vs "Two emails a month")
- Pop-up exit intent on Hotel Programme page (offer sample kit)
- Trust strip variants ("Lifetime warranty" alone vs "Lifetime warranty · Free shipping · Made to order")
