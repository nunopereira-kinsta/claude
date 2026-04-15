# New Trial Outreach Initiative — Pre-Read & Call Agenda

**Date:** Q3 Kick-off Call (30 min)
**Attendees:** Rachel Devine, Lucas Prigge, Shahzeb Ali, Pedro, PJ, Nour Moudarres, Nuno Pereira
**Objective:** Align on how we identify, reach out to, and convert high-potential trial accounts (and recent purchasers) into expansion opportunities.

---

## Context

Following a conversation with Nathan before the GTM meetup, one of the Q3 priorities is to proactively reach out to new trial accounts — and accounts that have just purchased a plan — based on their expansion potential. A typical example: a large agency signs up for a WP 2 plan without ever speaking to Sales.

This is the first time we're running a structured initiative like this, so it requires cross-functional alignment across Sales, RevOps, Customer Success, Finance, and Marketing.

This document summarises what has already been discussed in the Slack thread and highlights what still needs to be decided during the call.

---

## What's Been Discussed So Far

### 1. Target Accounts

**Agreed starting scope (Nuno, Rachel):**
- Primary focus on **new trial users** to keep things manageable.
- **Agencies that signed up on a non-agency plan** should be routed to AMs.
- RevOps to pull data on which account profiles typically upgrade.

**Enrichment & filtering signals proposed (Shahzeb):**
- Company attributes: size, team structure, estimated number of client sites.
- Tech stack: WordPress usage, current hosting provider, plugins (eComm, LMS).
- Agency type: eCommerce, enterprise, SMB, performance-focused.
- Intent signals: recent hiring (DevOps, WordPress), migration-related content, hosting research activity.
- In-app behaviour: migration queries in Intercom, rapid product usage, performance concerns.
- Website insights: portfolio analysis, traffic/performance benchmarks, client tier.
- Reputation/partnership data: Clutch, G2, Google reviews, CMS/plugin partnerships.

**Additional signals (PJ):**
- **Employee count** — surfaces enterprise brands that signed up without talking to Sales.
- Website metrics and plugin data (eComm, LMS) for direct brands and single-site accounts.
- Migration timing as a qualifying signal.

**Churn/activation signals (Csaba's research):**
- Trial accounts that convert typically: create a site on day 0, add a domain by day 1, point their domain by day 2 (medians).
- If a trial account hasn't pointed a domain by **day 6**, that's a strong churn signal.
- Median cancellation happens at **day 8** — outreach should happen before this.

> **DECISION NEEDED:** Which of these signals do we prioritise for v1? How much enrichment is realistic to implement before launch?

---

### 2. Ownership and Process

**What's been proposed:**
- **SDRs** own outreach to trial users (Rachel).
- **AMs** own outreach to already-paying customers and agencies on non-agency plans (Rachel).
- Current onboarding program only targets Sales-Led signups, so no conflict with PLG trials (Lucas, Nour).

**Timing considerations:**
- Csaba's data suggests intervening before day 6–8 for at-risk accounts.
- Csaba recommended building automation for a "soft churn alert" when trial accounts miss activation milestones.
- PJ flagged the need for migration timing data (time between account creation and first migration).

**Caution (PJ):** Signal must be tight — this should not turn into a welcome/onboarding call for the dev team.

> **DECISIONS NEEDED:**
> - Confirm SDR vs. AM ownership split.
> - Define when outreach happens (e.g., day 3? day 6? triggered by missed milestones?).
> - How does the handover from SDR to AE/AM work?
> - If a value-based onboarding trigger is introduced later, where is the line between CS and Sales? (Lucas, Nour)

---

### 3. Messaging and Value Proposition

**General approach (PJ):**
- Never a hard sell or forced upgrade.
- Outreach should **open with a question, not a pitch** — confirm the signal, start a real conversation.

**By segment:**

| Segment | Angle |
|---|---|
| **Agencies** | Partnership conversation. Understand who else they host with. Goal: consolidate all sites on Kinsta. |
| **Direct brands / single-site** | Infrastructure-fit conversation. If signals are there (eComm, LMS, high headcount), discuss fit before they hit a ceiling. |
| **At-risk trials** | Offer help with specific activation steps — creating/migrating a site, setting up a domain, pointing DNS. |

**Competitive reference (PJ):** WP Engine does this with self-signups, pushing isolated environments over shared plans.

> **DECISIONS NEEDED:**
> - Do we want a specific offer or incentive for any of these segments?
> - Should we draft outreach templates/sequences before launch?
> - Who owns messaging creation?

---

### 4. Tracking and Reporting

**Not yet discussed in detail.** The original brief proposed tracking:
- Number of accounts passed to Sales Dev
- SDR acceptance rates
- Reasons for not expanding
- Accounts handed to AMs
- Resulting expansion deals and MRR

**Available data inputs:**
- Csaba's trial conversion research (activation milestones, churn timing).
- The agency microsite campaign follows a similar identify-and-qualify model (Shahzeb) — could borrow its reporting framework.

> **DECISIONS NEEDED:**
> - What are the key metrics we report on?
> - How frequently do we review performance?
> - Who owns the reporting?

---

### 5. Incentives and Commissions

**What's clear (Rachel):**
- Trial users don't count as customers until they pay — no change to how SDR commissions fundamentally work.
- SDRs create a deal or handoff only if there's real potential, and get paid based on that.

**What needs follow-up:**
- If a trial user converts to paid **during** an active sales process with an AE, it needs to be flagged as new revenue for commission purposes. Rachel to connect with **Gelila** on this.
- Commission rules need alignment across Sales Management (lead assignment), Finance (commission processing), and Customer Success (conflict check) (Lucas).

> **DECISIONS NEEDED:**
> - Confirm commission treatment for the "trial converts to paid mid-sales-process" edge case.
> - Any special incentive structure for this initiative, or standard rules apply?

---

### 6. HubSpot Setup

**Framework proposed (Lucas):**
- **PLG trial signups** = MQLs and **New Revenue Deals** (they haven't paid yet).
- **Already paying customers** = **Expansion Deals**.
- This fits within existing GTM architecture.

**Deal logging rules (Lucas):**

| Scenario | Deal Type | Amount |
|---|---|---|
| Trial at risk, Sales saves it, converts at same level | NEW SLG | Full post-trial revenue |
| Trial not at risk, converts at same level without Sales influence | NEW SLG | Closed Lost ($0 gained) |
| Trial not at risk, Sales upsells during trial | NEW SLG | Difference between original and new MRR |
| Already paying, Sales upgrades | EXPANSION SLG | Upgrade amount |

> **DECISIONS NEEDED:**
> - Which pipeline do we use?
> - Do we need new deal stages or properties?
> - How do we mark/tag these accounts to distinguish them from standard inbound?

---

## Proposed Call Agenda (30 min)

| Time | Topic | Owner |
|---|---|---|
| 0–2 min | Context and goal for the call | Nuno |
| 2–8 min | **Target accounts:** Agree on v1 scope and priority signals | All (RevOps to lead) |
| 8–14 min | **Ownership and process:** Confirm who owns what, outreach timing, and handover | Rachel, Nuno |
| 14–18 min | **Messaging:** Align on angle per segment, decide who drafts templates | PJ |
| 18–22 min | **HubSpot setup:** Confirm pipeline, deal types, and tagging | Lucas |
| 22–26 min | **Commissions and tracking:** Flag open items, assign owners for follow-up | Rachel, Lucas |
| 26–30 min | **Next steps and owners** | Nuno |

---

## Open Items Requiring Follow-Up Outside This Call

- [ ] RevOps to pull data on which account profiles typically upgrade
- [ ] Rachel to connect with Gelila on commission edge case (trial converts mid-sales-process)
- [ ] Csaba's churn signal automation — who builds the "soft churn alert"?
- [ ] Outreach messaging/templates — who drafts, who reviews?
- [ ] Define reporting cadence and dashboard ownership
- [ ] Confirm no overlap with any planned value-based onboarding trigger (Lucas, Nour)
