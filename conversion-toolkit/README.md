# Kinsta.com On-Site Conversion Toolkit

A marketer-run program to lift **free-trial sign-ups** on kinsta.com using on-site tools deployed via **Google Tag Manager** — no Dev, no Design, no Content team, and **no changes to the product or the "first month free" offer**.

This is the Mutiny / Crazy Egg lane: snippets you drop in through GTM and configure yourself.

## What's in here

| File | What it is |
|---|---|
| `README.md` | This overview — tool shortlist, starting stack, roadmap (start here) |
| `gtm-implementation-guide.md` | How to deploy each tool through GTM safely (tags, triggers, async loading, conversion tracking) |
| `ab-test-backlog.md` | Prioritized A/B test ideas for pricing / signup / migration / homepage |
| `variant-copy.md` | Ready-to-use draft copy for the sticky bar, exit-intent offers, and test headlines/CTAs |
| `personalization-plan.md` | Which visitor segments get which on-site message swaps |

## The starting stack (recommended — ~a few hundred $/mo, all via GTM)

**Microsoft Clarity + VWO + OptinMonster** covers the core loop — **diagnose → test → capture** — on your money pages (pricing, `/signup`, migration, homepage). Add personalization and social proof once you have data.

## 1-page tool shortlist

| # | Category | Tool | What it does on-site | Deploy | Approx price | Trial |
|---|---|---|---|---|---|---|
| 1 | Session replay + heatmaps | **Microsoft Clarity** | See where visitors stall/rage-click on pricing & signup | GTM snippet | **Free** (unlimited) | clarity.microsoft.com |
| 2 | A/B testing + heatmaps | **VWO** | Visual-editor A/B tests on headlines, CTAs, layout, forms | GTM snippet | from ~$314/mo (Growth) | vwo.com/free-trial |
| 3 | Exit-intent / sticky bars | **OptinMonster** | Catch abandoners, site-wide "first month free" bar, slide-ins | GTM snippet | ~$9–49/mo | optinmonster.com |
| 4 | Personalization (Mutiny lane) | **Mutiny** *or* **VWO Personalize** | Swap headlines/CTAs by source/geo/returning on existing pages | GTM snippet | Mutiny ~$5–20K+/yr; VWO incl. above | mutinyhq.com / vwo.com |
| 5 | Social proof / FOMO | **TrustPulse** | Live "someone just started a trial" toasts; trust badges near CTAs | GTM snippet | ~$50–100/mo | trustpulse.com |
| 6 | Interactive widget *(optional)* | **Outgrow** | Embedded migration-savings / hosting-cost calculator | GTM/embed | ~$14–100/mo | outgrow.co |

**Complements, not replacements:** Clarity/VWO sit alongside your existing **Crazy Egg**. VWO can consolidate heatmaps + A/B if you'd rather not run two.

**Deliberately excluded** (out of scope for self-serve on-site):
- Chat / demo-booking (Chili Piper, Qualified) and visitor de-anonymization (RB2B, Warmly) → sales-led lane, revisit only if "Talk to sales" becomes the priority.
- Externally-hosted landing pages (Unbounce, etc.) → keeps everything on kinsta.com.
- Anything requiring content/blog work, CRM/email programs, or new offers/pricing.

## Roadmap

**Week 1 — Instrument**
- Install **Clarity** + **VWO** via GTM.
- Fire a **trial-start conversion event** (on `/signup` completion) so every test has a real success metric.
- Record a **Core Web Vitals baseline** (PageSpeed Insights / Search Console) before adding more scripts.

**Weeks 2–4 — Capture + first tests**
- **OptinMonster**: site-wide "first month free" sticky bar + exit-intent on `/pricing` and `/signup`.
- First **VWO A/B tests** on the pricing and signup pages (see `ab-test-backlog.md`).
- **TrustPulse** trial-activity toasts.

**Ongoing — Optimize + personalize**
- More A/B tests informed by Clarity replays.
- Turn on **personalization** by source/geo/returning-visitor (see `personalization-plan.md`).
- Optional: embed the **Outgrow** calculator on homepage/pricing.

## Guardrail — Core Web Vitals

Every GTM script adds client-side weight, and Kinsta sells *performance*. After each tool goes live:
- Re-check **LCP / INP / CLS** (field data in Search Console; lab in PageSpeed Insights).
- Load tags **async / deferred**; fire heavy tags on interaction or after DOM-ready, not on every pageview where avoidable.
- **Roll back** anything that materially degrades speed. A faster page usually converts better anyway.

## Measuring success

- **Primary metric:** free-trial starts (GTM event on `/signup` completion → HubSpot).
- **Secondary:** high-intent form fills (talk-to-sales, contact).
- **Discipline:** every tactic runs against a real control; roll a winner to 100% only after statistically meaningful lift.

## Which Claude model to use for this work

- **Opus 4.8 @ `high`** — analyze heatmap/replay data, design the test plan, decide what to personalize (`xhigh` for a full money-page teardown).
- **Sonnet 5 @ `medium`** — generate A/B copy variants at volume (headlines, CTAs, offers).
- **Haiku 4.5 @ default** — cheap classification (tagging replay notes, bucketing segments).

*Opus to decide, Sonnet to produce variants, Haiku to sort.*
