# A/B Test Backlog

Prioritized, on-site A/B tests for kinsta.com, all buildable in VWO's visual editor (no Dev). Every test's success metric is **`trial_started`** (see GTM guide §1); watch a secondary guardrail so a "win" on clicks that tanks real signups gets caught.

## How it's scored

- **Impact** (1–5): expected effect on trial sign-ups, weighted by page traffic/intent.
- **Effort** (1–5): build complexity in VWO (1 = copy swap, 5 = multi-element layout).
- **Priority = Impact ÷ Effort.** Do high-priority first. Run each to statistical significance before rolling to 100%.

> Ship order rule of thumb: start where **high intent meets high traffic** — the pricing page and the signup entry — then homepage, then migration.

---

## Pricing page (`/pricing`) — highest intent

| # | Hypothesis | Variant | Impact | Effort | Priority |
|---|---|---|---|---|---|
| P1 | Primary CTA copy is generic; a value-led CTA lifts clicks | "Try for free" → "Start my free month" / "Start free — no card" | 4 | 1 | **4.0** |
| P2 | Free-trial risk-reversal is buried; surfacing it near the CTA reduces hesitation | Add microcopy under CTA: "First month free · No credit card · Free migration" | 4 | 1 | **4.0** |
| P3 | Plan choice overwhelms; pre-selecting/《most popular》badge guides the eye | Add "Most popular" highlight + default toggle to annual | 4 | 2 | 2.0 |
| P4 | Monthly price framing feels high; annual-first framing anchors better | Toggle defaults to annual (show "/mo billed yearly") | 3 | 2 | 1.5 |
| P5 | Trust is thin at decision point; social proof lifts conversion | Add G2/Trustpilot rating + customer-count line above plans | 3 | 2 | 1.5 |
| P6 | FAQ objections aren't addressed inline | Add a 3-item objection FAQ near CTA (migration, cancel, support) | 3 | 2 | 1.5 |

## Signup entry (`/signup` and the CTA that leads there)

| # | Hypothesis | Variant | Impact | Effort | Priority |
|---|---|---|---|---|---|
| S1 | Signup page lacks reassurance; visitors bail at the form | Add trust strip above form: "No credit card · Cancel anytime · Free migration" | 5 | 1 | **5.0** |
| S2 | Hero CTAs across site → test which destination CTA text pulls most to signup | "Try Kinsta Now" vs "Start free month" vs "Get started free" | 4 | 1 | **4.0** |
| S3 | Perceived length/friction; adding a progress or "takes 2 min" cue helps | Add "Set up in ~2 minutes" cue near form start | 3 | 1 | 3.0 |
| S4 | Social proof on the form page reduces abandonment | Add logo strip / "230,000+ businesses" line beside form | 3 | 2 | 1.5 |

## Homepage (`/`) — highest traffic

| # | Hypothesis | Variant | Impact | Effort | Priority |
|---|---|---|---|---|---|
| H1 | Hero headline is feature-led; outcome-led headline converts better | Test outcome framing (speed/uptime) vs current | 4 | 2 | 2.0 |
| H2 | Hero CTA emphasis; single strong CTA vs dual CTA | Make "Try for free" primary, demote secondary | 4 | 1 | **4.0** |
| H3 | Free-migration differentiator under-used in hero | Add "Free managed migration" as a hero sub-benefit | 3 | 1 | 3.0 |
| H4 | Sticky CTA on scroll keeps the offer present | Persistent header CTA / OptinMonster bar (coordinate w/ tools) | 3 | 1 | 3.0 |

## Migration page (`/wordpress-hosting/migration/`) — lowest-friction switchers

| # | Hypothesis | Variant | Impact | Effort | Priority |
|---|---|---|---|---|---|
| M1 | "Get started" is vague; a switch-specific CTA converts intent | "Get started" → "Migrate free — start now" | 4 | 1 | **4.0** |
| M2 | Proof points exist but aren't near the CTA | Move "1.1k+ monthly migrations · 96% satisfaction" beside CTA | 3 | 1 | 3.0 |
| M3 | Effort objection ("migration is painful") persists | Add "We do 100% of the work" reassurance block above CTA | 3 | 2 | 1.5 |

---

## Suggested first sprint (do these five)

1. **S1** — signup trust strip (Impact 5, Effort 1)
2. **P1** — pricing CTA copy
3. **P2** — pricing risk-reversal microcopy
4. **H2** — homepage single strong CTA
5. **M1** — migration switch-specific CTA

All five are copy/element swaps (Effort 1), touch your highest-intent surfaces, and can run in parallel as separate VWO campaigns. Draft copy for each is in `variant-copy.md`.

## Running discipline

- **One variable per test** where possible, so a win is attributable.
- **Sample size:** use VWO's built-in significance calc; don't call a test before it reaches significance (rough rule: ≥ a few hundred conversions per arm, or 2–4 weeks).
- **Guardrail metric:** watch downstream trial→paid and bounce, not just the click, so a "louder CTA" that attracts low-fit clicks gets caught.
- **Log every result** (win/loss/flat + lift %) in the change log so the backlog re-prioritizes off real data.
