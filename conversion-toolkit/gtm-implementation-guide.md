# GTM Implementation Guide

How to deploy the starting stack on kinsta.com through Google Tag Manager — safely, without Dev, and without wrecking Core Web Vitals. Written for a marketer with GTM edit access.

> **Ground rules**
> - One change at a time. Publish, verify in **GTM Preview**, then move on.
> - Prefer each vendor's **async loader**. Never paste a synchronous `<script>` that blocks rendering.
> - Fire heavy tags **after** the page is interactive, not before first paint.
> - Re-check Core Web Vitals after each publish (see §6).

---

## 0. Prerequisites (one-time)

1. Confirm the GTM container snippet is already on all kinsta.com templates (it is, since Crazy Egg-type tags run today). If a **custom-coded page** doesn't include the GTM snippet, that page is a blind spot — list those pages and treat them as out of reach until the snippet is added.
2. Turn on **GTM Preview/Debug** and keep it open while building.
3. Decide a naming convention, e.g. `HTML - Clarity`, `Custom - VWO`, `Trigger - Pageview /pricing`.

---

## 1. Conversion tracking first (do this before any tool)

Every A/B test needs a reliable "trial started" signal. Two options:

**Option A — Thank-you / dashboard URL trigger (simplest).**
If a completed signup lands on a distinct URL (e.g. `mykinsta.com/...` or `kinsta.com/signup/success`), create:
- **Trigger** → *Page View* → fires on *Page URL contains* `signup/success` (adjust to the real URL).
- Push a dataLayer event so every tool can consume it:

```html
<!-- Tag: HTML - Trial Started dataLayer push -->
<script>
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({ event: 'trial_started' });
</script>
```

**Option B — Custom event on the signup button (if signup is same-page / SPA).**
- **Trigger** → *Click - All Elements* → fires on the signup CTA (match by Click ID/Class/Text).
- Better: ask whoever owns the signup form to `dataLayer.push({event:'trial_started'})` on success. If that needs Dev, fall back to Option A.

Then define **`trial_started`** as the primary goal inside VWO, GA4, and HubSpot so all three read the same event.

> ⚠️ Cross-domain note: if signup completes on `mykinsta.com` (different domain), URL-based tracking won't fire from the kinsta.com container. Use GA4 cross-domain measurement, or count the *signup-page reach* + button click as the on-site proxy metric and reconcile true completions in HubSpot.

---

## 2. Microsoft Clarity (free — heatmaps + session replay)

1. Clarity → create project → copy the tracking code.
2. GTM → **New Tag** → *Custom HTML* → paste the Clarity snippet (it's already async).
3. **Trigger:** *Initialization - All Pages* (loads early but non-blocking).
4. Name `HTML - Clarity`. Preview → confirm Clarity dashboard shows a live session → Publish.
5. In Clarity, set up **funnels/filters** for `/pricing`, `/signup`, and `/wordpress-hosting/migration/`.

*Cost: free, unlimited. ~30-day retention.*

---

## 3. VWO (A/B testing + heatmaps)

1. VWO → get the **async SmartCode**.
2. GTM → **Custom HTML** tag → paste SmartCode.
3. **Trigger:** *Initialization - All Pages* (VWO must load early to avoid flicker/FOUC).
4. Enable VWO's **anti-flicker** setting so the original doesn't flash before the variation.
5. Import the `trial_started` event as a **goal** (Settings → Goals → Custom conversion → dataLayer `trial_started`).
6. Build tests in VWO's **visual editor** — no code. See `ab-test-backlog.md`.

> Flicker control matters on a performance-sensitive site: keep the anti-flicker timeout short (e.g. ≤1000ms) so a slow VWO load never blocks content for real users.

*Cost: from ~$314/mo (Growth). VWO's heatmaps can replace Crazy Egg if you consolidate.*

---

## 4. OptinMonster (exit-intent, sticky bar, slide-ins)

1. OptinMonster → build campaigns in their editor:
   - **Floating bar** (site-wide): "Get your first month free" → button to `/signup`.
   - **Exit-intent popup** on `/pricing` and `/signup`: reinforce the existing free-trial + free-migration offer.
   - **Slide-in** on migration page.
2. Deploy via GTM:
   - GTM → **Custom HTML** tag → OptinMonster's account embed (async).
   - **Trigger:** *Initialization - All Pages*.
3. Control *where* each campaign shows using OptinMonster's **page-level targeting** (URL rules) and **display rules** (exit-intent, scroll depth, time-on-page) — configured in OptinMonster, not GTM.
4. Set each campaign's success to route the click to `/signup` so it flows into `trial_started`.

*Cost: ~$9–49/mo. Copy is in `variant-copy.md` — all promotes the existing offer; no new offer.*

---

## 5. TrustPulse (social proof toasts) — optional, cheap

1. TrustPulse → create an **"on fire"** campaign (e.g. "N people started a trial this week") or an action campaign tied to signups.
2. GTM → **Custom HTML** → TrustPulse embed (async) → **Trigger:** *All Pages*.
3. Target it to the homepage, pricing, and migration pages.

*Cost: ~$50–100/mo. Keep frequency modest — over-firing reads as spammy and can hurt trust.*

---

## 6. Core Web Vitals guardrail (run after every publish)

Kinsta sells speed, so treat CWV as a release gate:

1. **Before** adding a tag: record baseline LCP / INP / CLS from **Search Console → Core Web Vitals** (field data) and **PageSpeed Insights** (lab) for homepage, `/pricing`, `/signup`.
2. **After** publishing: re-measure the same pages 48–72h later (field data lags).
3. Watch specifically for:
   - **CLS** jumps from injected bars/popups (reserve space; avoid layout shift on load).
   - **INP** regressions from heavy JS.
   - **LCP** delays if a tag loads render-blocking.
4. Mitigations: async/defer everything; fire non-critical tags on `DOM Ready` or first interaction; use OptinMonster/TrustPulse timing rules so overlays appear *after* content paints.
5. If a tool degrades CWV materially and can't be tuned, **pause the tag** — the sign-up lift isn't worth a slower performance-brand site.

---

## 7. Change log discipline

Keep a simple log (a shared sheet is fine): date, tag published, pages affected, CWV before/after, and the test/campaign it powers. Makes rollback and attribution trivial.
