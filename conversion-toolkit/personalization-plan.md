# Personalization Plan

On-site message swaps by visitor segment — the Mutiny lane. This **changes existing pages** (headline, sub-head, CTA, a hero benefit, sometimes a testimonial); it does **not** create new pages, change the product, or touch the offer. Built in **Mutiny** or **VWO Personalize**, deployed via GTM.

> Sequencing: don't personalize blind. Run it **after** Clarity + VWO are live and a couple of baseline A/B tests have shown what generally converts. Personalization multiplies a good baseline; it can't fix a bad one.

## Targeting signals available with no Dev

All readable client-side by Mutiny/VWO from the request, referrer, or UTM params:

- **Traffic source / campaign** — `utm_source` / `utm_campaign`, referrer domain (Google, Reddit, YouTube, review sites).
- **Geo / language** — country + browser language (Japan is a top market).
- **New vs returning** — cookie/visit count.
- **Landing context** — which page they entered on (pricing vs migration vs a guide).
- **Search intent proxy** — referring query isn't reliably available, but the **landing URL** is a strong proxy.

## Segment → message map

| Segment (signal) | Insight | On-site swap | Priority |
|---|---|---|---|
| **Returning, hasn't signed up** (visit count > 1, no trial cookie) | Already interested; needs a nudge, not a pitch | Hero → "Ready when you are — first month's free." Surface sticky "Start free" bar more assertively | High |
| **From a review site / comparison referrer** (G2, Trustpilot, "vs" pages) | Actively comparing hosts | Hero sub-head → lead with the differentiator: "Free managed migration + first month free." Add rating badge | High |
| **Japan / JP language** | Top non-English market; English pages likely underperform | Swap hero headline/CTA to localized copy on money pages (reuse existing dashboard localization strings; **no new content team work** if strings already exist — otherwise skip until they do) | High |
| **Paid campaign visitors** (`utm_medium=cpc`) | Expect message match to the ad | Mirror the ad's promise in the hero (e.g. ad said "free migration" → hero leads with migration) | Medium |
| **New, top-of-funnel referrer** (Reddit/YouTube/social) | Curious, not yet in buying mode | Softer hero + "first month free, no card" to lower the entry bar | Medium |
| **Agency-intent** (landed on/【from agency URLs or agency campaign UTMs) | Different value drivers (scale, white-label, recurring) | Hero swap → agency angle + route to the agency CTA (still self-serve trial where applicable) | Medium |
| **High-intent page entrants** (`/pricing`, `/signup`, `/migration`) | Decision stage | Reinforce risk-reversal near CTA (no card, free migration, cancel anytime) | Medium |

## Rules of the road

- **One swap per segment to start.** Headline + CTA is enough; don't rebuild the page.
- **Always keep a holdout/control** in the personalization tool so you can prove lift vs the default page — same discipline as A/B testing.
- **Fewer, sharper segments beat many fuzzy ones.** Start with the two "High" rows (returning-not-signed-up, review-site referrers); add others once they prove out.
- **Message match is the whole game:** the swap should echo *why that visitor is here*. A comparison-shopper wants the differentiator; a returning visitor wants a nudge; a JP visitor wants their language.
- **Respect CWV:** personalization JS must load with anti-flicker; a swap that flashes the default first (FOUC) or shifts layout hurts both UX and Core Web Vitals.

## Measurement

- Primary metric per segment: **`trial_started`** vs the segment's own holdout.
- Watch for **negative** personalization (a swap that underperforms the default) — kill it fast.
- Roll winners into the default page copy once proven, then free the slot for the next segment.

## Tool note

- **VWO Personalize** keeps testing + personalization in one tool (simplest if you're already on VWO for A/B).
- **Mutiny** is stronger for firmographic/account-level targeting (company, industry) — more relevant if/when the priority shifts toward ABM and "Talk to sales." For self-serve trial sign-ups, source/geo/returning signals in VWO cover most of the value at lower cost.
