# Referral Program — Goldy Brown

Implements the `referral-program` skill. A working spec for a friend-refers-friend programme that respects the brand's quiet-luxury voice.

## The brief

Most luxury referral programmes fail because they read as discount marketing. The Goldy Brown referral programme is built to read as a personal handoff between two clients — closer to a private members club introduction than a "$10 off your next order."

## The structure

### For the existing client (the referrer)
- Personal referral link (e.g. `goldybrown.com/?ref=AC9F`)
- For every successful referral that buys a piece $200+:
  - Free hand-tattooed personalisation on their next piece (normally $50)
  - OR hot-stamping on a second piece they already own
- After 3 successful referrals: invitation to a private atelier visit (in person or video) and an early-access drop list before public release

### For the friend (the referred)
- 10% off their first order, sent via personalised email from the friend (not a generic discount code)
- A handwritten card included with the first shipment that mentions the referrer

### What we don't do
- Bare cash discounts ("$25 off")
- Stackable discount codes
- Public leaderboards
- Pop-up "refer a friend" overlays

The structure says: <em>your friend thought of you specifically, and the atelier is treating you well because of that</em>. Not: <em>here's an affiliate link for a $25 commission</em>.

---

## Implementation (technical)

### Phase 1 — manual, immediate
Run it as a manual programme to start. Costs nothing, validates the unit economics.

1. Add a "Refer a friend" link in the post-purchase email and in the warranty card
2. Mailto link: `mailto:?subject=A%20brand%20I%20use&body=...` with pre-written text the client can edit
3. When a referred order comes in, attribution is by note ("Referred by [name]") in the order notes
4. Quarterly, count successful referrals and send the personalised thank-you to the referrer

**Pros:** Zero infrastructure. Personal feel matches the brand.
**Cons:** Doesn't scale past ~50 referrals/month without manual overhead.

### Phase 2 — light tech, after 100+ orders
1. Add a unique referral code to each customer record (in Shopify or whatever the order system is)
2. Generate a personal link: `goldybrown.com/?ref=CODE`
3. JavaScript reads `?ref=` on landing, stores it in `localStorage` as a 90-day cookie
4. At checkout, the code is attached to the order automatically
5. Reward eligibility automated; thank-you email automated

Tools that handle this for Shopify: Friendbuy, Yotpo Loyalty, Smile.io. Pick one. They all do the same job.

### Phase 3 — full programme, after $500K ARR
- Tiered rewards (3/6/12 successful referrals)
- Exclusive drops only available to clients with active referrals
- Private members atelier event (annual, Vancouver)

---

## The math (back-of-envelope)

| Metric | Target Year 1 |
|--------|---------------|
| Existing clients participating | 30% (industry avg ~10%; quiet-luxury brands skew higher) |
| Successful referrals per participating client | 1.5/year |
| Conversion rate of referred visitors | 15-25% (vs ~2-4% cold) |
| Per-referral cost to brand | $50 (free hand-tattoo) |
| Per-referral revenue to brand | $249-$1,000+ |
| Programme ROI | 5-20× |

The 5-20× ROI assumes you already have product-market fit. If retention is bad, fix that before referrals.

---

## The referrer-side script

What the existing client sees in a personalised email or shareable link:

> Subject: I think you'd actually use this
>
> Hi [friend],
>
> Got a new Holster from Goldy Brown a few months back — body-worn leather travel bag, made in Vancouver — and I'm using it on every flight now. Pouch sized for passport, phone, AirPods, and a slim wallet. Figured you'd appreciate it.
>
> If you want to take a look, here's a 10%-off link they set up: [goldybrown.com/?ref=AC9F]
>
> No pressure either way.
>
> [name]

The script is editable. The voice is the friend's, not ours.

---

## What kills referral programmes (avoid)

- **Pop-up cards immediately on site visit.** Trust isn't built yet. Wait until post-purchase.
- **Asking too soon.** Send the referral ask 30 days post-delivery, not day 1. The client needs to actually use the piece first.
- **Tiered cash rewards.** "Earn $50 for every friend" reads as MLM. Use brand experiences instead (atelier visit, early access, free personalisation).
- **Forcing the share format.** Some clients want a link, some want to physically tell a friend, some want to send a piece as a gift. All three should work.
- **Public thank-you walls.** Naming names without explicit consent destroys trust. If a client wants to be credited publicly, they can opt in.

---

## Adjacent: gift card pseudo-referrals

A simpler near-equivalent: physical Goldy Brown gift cards (paper, signed, sealed) that an existing client can buy at a 15% discount and gift to a friend. The friend redeems for any piece. The card itself becomes the referral mechanism — the friend physically holds the brand before they buy anything.

Print run: 100 cards/year. Cost: ~$2 each printed nicely. Revenue per redeemed card: $200-$500. The card can also be sold via the website at face value (no discount) for a generic gifting use case.

---

## Launch sequence

- **Month 0 (now):** Add the refer-a-friend mailto in the post-purchase email and the warranty card. Run manual attribution.
- **Month 3:** Look at attribution data. If 5+ referrals/month, justify the $50/mo Friendbuy or similar tool.
- **Month 6:** Add the gift card programme.
- **Month 12:** Run the first private atelier event for top referrers.

The whole programme should feel like an extension of the lifetime warranty — quiet, personal, and felt only by the people who deserve it.
