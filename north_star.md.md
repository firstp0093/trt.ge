north_star.md

> GENERATED: 2026-01-09T17:05:45Z  
> OWNER: Product / Growth  
> STATUS: North Star Spec (source of truth)

# TRT Provider Matchmaking & Acquisition Platform
## Strategic Product Specification (North Star)

### One-line
Build the **world’s most structured, verified dataset on TRT providers** and use it to capture high-intent demand from **Google + AI search**, then route users to the **best-fit clinic** with measurable ROI.

---

## 0) Why users come back (and share)
People share healthcare “finders” when they feel:
- **Safe:** “This doesn’t feel sketchy; it’s verified and transparent.”
- **Confident:** “It explained *why* these clinics match me.”
- **Prepared:** “It gave me a clean summary I can bring to a consult.”
- **No surprises:** “Pricing and logistics were clear up front.”
- **Respectful:** “No creepy data collection; consent-first.”

**Design principle:** Every surface must increase trust *and* produce something worth sharing (a short, factual, timestamped artifact).

---

## 1) Executive Vision

### What we are building
A HIPAA-aware marketplace and SaaS platform that:
1) **Acquires** users via programmatic local intent + topical authority pages  
2) **Qualifies** users via interactive tools (symptoms, labs, cost, preferences)  
3) **Matches** users to verified providers based on compatibility + logistics + capacity  
4) **Closes** via provider CRM + analytics + attribution

### What we are not building (non-goals)
- Not a “general men’s health blog” without structured data outputs
- Not a “Yelp for TRT” with unverified profiles and noisy reviews
- Not a medical diagnostic tool (education + structured summaries only)

---

## 2) North Star Metric

### North Star
**Verified Matches → Booked Consults (VMB)**  
Count of consultations booked with *verified* providers where the match score ≥ threshold.

### Supporting metrics
- **Acquisition:** organic sessions, AI referral sessions, CTR, index coverage
- **Activation:** tool completion rate, lead capture rate, consent rate
- **Match quality:** match acceptance rate, time-to-book, refund/dispute rate
- **Provider ROI:** CAC, CPA, attributed revenue, LTV, churn

---

## 3) Core Loop (Intent-Based Architecture)

> Core philosophy: We are not “a directory.” We are an **authoritative dataset** that search engines and LLMs can reliably cite.

```mermaid
flowchart TD
  A[User Intent Query\n“TRT clinic Austin Aetna telehealth”] --> B{Traffic Source}
  B --> C[Traditional Search\nGoogle/Bing]
  B --> D[AI Search\nChatGPT/Perplexity/AI Overviews]

  subgraph S[Platform Engine: The Data Source]
    E[Knowledge Graph\nClinics, Doctors, Locations, Pricing, Insurance] --> F[Structured Output\nJSON-LD / Schema.org / Tables]
    E --> G[LLM-Ready Content\nFactual, attributed, timestamped]
    E --> H[Tools Output\nScores + summaries as portable artifacts]
  end

  C --> I[Programmatic Landing Page\nCity/Insurance/Modality]
  D --> J[Citation/Reference\nEntity + Data Hub pages]

  I --> K[Interactive Engagement\nAssessment + Estimator + Matcher]
  J --> K
  K --> L[Lead Capture\nConsent-first]
  L --> M[Provider Match\nRanked + explainable]
  M --> N[Consult Booked]
  N --> O[Conversion + ROI\nAttribution + Analytics]
4) Product Surfaces
A) Patient Acquisition Layer (SEO + AI Visibility)
A1) Programmatic SEO Pages (Static-first / SSG)
Templates

/trt-clinics/[state]/[city]

/trt-clinics/[state]/[city]/[modality]

/trt-clinics/[state]/[city]/[modality]/[insurance]

Page requirements

Unique intro + FAQs + “how we rank” snippet (avoid thin/duplicate pages)

Filtered clinic listings backed by structured data

Internal links to relevant education (hub/spoke)

Fast, crawlable HTML (SSG preferred; SSR only when needed)

Index quality guardrails

Auto-noindex pages with < N results or low uniqueness

Canonicals for near-duplicate filter permutations

Sitemaps segmented (programmatic / entities / data hubs)

A2) Entity Homepages (Clinic & Provider Profiles)
Each clinic gets a strict, fact-based “entity homepage” optimized for citation:

Identity: legal name, NPI/credentials (where applicable), founding year, ownership model

Coverage: states served, modalities, insurance accepted, telehealth availability

Pricing: starting price, membership model, what’s included (structured fields)

Medical oversight: medical director name + credentials (if verified)

Reviews: verified + sourced (with provenance labels)

Last verified timestamp + verification badge

FAQ schema embedded (only factual Qs)

A3) Data Hubs (Citation Engine)
Purpose-built pages easy to parse for humans and machines:

/data/trt-pricing-by-city

/data/trt-telehealth-states-served

/data/insurance-acceptance-by-market

Rules

Clean tables + methodology + “last updated”

Export links: .json / .csv / .jsonld

Every statistic has definitions + provenance

A4) AI / LLM Readability Layer
Schema.org JSON-LD on every entity + listing page

“About this data” blocks (definitions, cadence, methodology)

Optional llms.txt / llm.txt (experimental): point agents to canonical hubs and entity endpoints
Treat as additive, not a dependency.

B) Patient Engagement Suite (Conversion Tools)
Tools are educational + summarization. They do not diagnose or provide medical advice.

B1) Symptom Severity Assessment (“ADAM-style” tool)
Inputs

Structured responses (no free-text required; free-text optional)

Outputs

Symptom score + category bands

“Discussion guide” for provider visit

Downloadable summary artifact (PDF/JSON) with timestamps

Lead capture

Show partial results → email/phone + consent to reveal full report

Always provide a non-gated “basic summary” for trust

B2) Labs Decoder (“Bloodwork Interpreter”)
Inputs

TT, FT (optional), SHBG, E2 (optional), HCT/HGB (optional), age

Outputs

Normalized ranges (with source + lab variability disclaimer)

Flags: “ask your clinician about…” prompts

Structured JSON summary for portability

Safety

No dosing advice

No treatment recommendation

“Seek medical care” triggers for dangerous ranges

B3) Protocol Preference Matcher
Inputs

Modality preference, injection frequency tolerance, needle comfort, travel, budget

Optional: fertility goals, adherence style

Outputs

Ranked preferences + “what to ask clinics” checklist

Portable “Treatment Preference Profile” JSON artifact

B4) Cost of Therapy Estimator
Inputs

City/state, modality, insurance/cash, visit frequency assumptions

Outputs

Monthly + annual ranges

Line-item breakdown (labs, consults, meds, supplies)

Model comparison (telehealth subscription vs in-person)

Also feeds aggregated, non-PHI market averages into Data Hub pages.

C) Provider SaaS Layer (Monetization + Outcomes)
C1) Provider Onboarding + Verification
Identity and licensing verification workflow (levels: see §11).

Required structured fields

Modalities, states served, insurance accepted

Pricing components (base + included items + optional add-ons)

Capacity / lead volume limits

C2) Lead Management CRM
Pipeline:
New → Contacted → Qualified → Booked → Converted → Retained

Enriched leads:

Tool artifacts attached (symptoms/labs/preferences/cost assumptions)

Match rationale: “why this lead fits you”

Consent and data access controls visible in-line

Integrations:

Webhooks/Zapier + import/export

Optional native integrations later

C3) Analytics + Attribution
Provider dashboard:

CPL / CPA / close rate / time-to-first-contact

Cohort retention (lead quality by source & landing page)

“Answer Share” (AI visibility proxies):

Visits from AI referrers + bot fetches to data hubs

Engagement with “citation-ready” pages (scroll, copy events, export hits)

Do not claim direct “LLM cited us” unless provable; use proxies and verifiable referrers.

5) Data Architecture (The Moat)
Data types
Public Citation Data (indexable)

Clinics, locations, modalities, pricing ranges, insurance acceptance

Reviews (with provenance), educational content, aggregated market stats

Sensitive / Regulated Data (restricted)

Lead contact info, tool inputs/outputs tied to a person, communications, appointment metadata

Separation principle
Public dataset must be fast, cacheable, globally readable

Sensitive data must be access-controlled, auditable, minimally retained

mermaid
Copy code
flowchart LR
  U[User] --> P[Public Site\nProgrammatic + Entity + Data Hubs]
  U --> T[Tools\nAssessment / Labs / Cost / Matcher]
  T -->|Consent| S[Secure Lead Store\nPII/PHI boundary]
  S --> R[Routing + Match Engine]
  R --> V[Provider Portal\nCRM + Analytics]

  P --> KG[Public Knowledge Graph\nStructured citation data]
  KG --> EX[Exports\nJSON/CSV/JSON-LD]
Core entities (minimum viable schema)
Clinic

id, name, legal_name, locations[], telehealth, states_served[], modalities[], pricing_model, starting_price_range, insurances[], verification_level, last_verified_at

Provider

id, name, credentials, role, associated_clinics[], license_states[], verified_at

Location

id, clinic_id, address, geo(lat,lng), service_radius, appointment_types[]

ListingPage

id, params(city/modality/insurance), canonical_url, content_hash, index_policy, last_generated_at

Review

id, clinic_id, source, rating, text, verified_flag, created_at, provenance_label

Lead

id, contact, consent, tool_artifacts[], created_at, source_attribution

Match

id, lead_id, clinic_id, score, explanation[], status, booked_at

6) SEO + LLM Optimization System (Integrated)
A) Indexing & page quality rules
Every landing page must provide:

Unique content (intro + FAQs + local context)

Structured listings (consistent fields)

Freshness (regeneration when clinic data changes)

Avoid:

Infinite filter combinations

Thin pages with repeated boilerplate

Unbounded pagination without a canonical strategy

B) Structured data strategy (Schema.org)
Listing pages: ItemList + MedicalClinic entries

Clinic pages: MedicalClinic + Physician (when verified) + FAQPage

Reviews: Review with provenance

Data hubs: tabular data + downloadable exports

C) “Citation-ready” content format
Prefer:

Short fact blocks (Founded, States served, Starting price, Insurance, Verification)

Clean comparison tables

Methodology sections (“How we calculate averages”)

Explicit timestamps (“Last verified”)

Provide machine endpoints:

/api/public/clinics/[id].json

/exports/trt-pricing-by-city.csv

/exports/clinic-index.jsonl (future)

D) Topical Authority Map (Hub/Spoke)
Goal: look like an encyclopedia with a knowledge graph, not a blog.

mermaid
Copy code
mindmap
  root((TRT Topical Authority))
    (Treatment Options)
      [Injections]
      [Gels & Creams]
      [Pellets]
      [Clomiphene / SERMs]
    (Side Effects & Management)
      [Estradiol discussion]
      [Polycythemia awareness]
      [Fertility preservation]
    (Diagnostics & Labs)
      [Total vs Free T]
      [SHBG]
      [LH/FSH]
      [Prolactin]
    (Legal & Access)
      [Telehealth by state]
      [Insurance & cash-pay]
      [Clinic selection criteria]
    (Comparisons)
      [Telehealth vs in-person]
      [Cypionate vs enanthate]
      [HCG vs alternatives]
    (Local Intent)
      [TRT clinics in City]
      [Labs in City]
      [Men's health specialists in City]
Automation requirements:

Internal links from listings → relevant hubs/spokes

Hubs/spokes → “find clinics” CTAs

Entity pages link to relevant education based on modalities offered

7) Compliance, Safety, and Trust
Mandatory user-facing disclaimers
Tools are educational; not diagnosis; consult a licensed clinician

Emergency guidance for critical lab flags (seek immediate care)

Clear data provenance and “how we verify”

HIPAA-aware design requirements
Data minimization (collect only what’s needed)

Consent gating before storing tool outputs tied to identity

Encryption in transit + at rest

Audit logs for sensitive record access

Role-based access control (provider sees only assigned/accepted leads)

Retention policy (auto-delete stale leads and tool inputs)

Content & advertising policy hygiene
Clinic claims must be structured + verifiable

Prohibit prohibited medical advertising claims in provider-submitted content

Moderation workflow + provenance tracking for reviews

8) Technical Architecture (Pragmatic, Performance-First)
Architecture split (recommended)
Public Acquisition Layer (SEO/AI)

Static-first framework + SSG for programmatic pages

Extremely fast HTML + JSON-LD + exports

Secure App Layer (Tools, Leads, Provider Portal)

Auth, consent, lead storage, CRM, analytics

Data Pipeline

Verification jobs, review ingestion, dedupe, quality scoring, page regeneration

Stack constraints (non-negotiables)
Must support:

High-volume page generation

Geo search (radius, city/state)

Structured data exports

Strong access control + auditability for sensitive data

Background jobs with retries + idempotency

Compliance procurement gate: choose vendors based on BAA/compliance requirements.

9) Roadmap (Phased Delivery)
mermaid
Copy code
timeline
  title TRT Platform Roadmap
  section Phase 1 — Foundation (0–8 weeks)
    Data model + verification levels : clinic/provider schema, provenance
    Directory MVP : city pages + entity pages + basic filters
    Basic lead capture : consent + contact + routing v1
  section Phase 2 — Conversion Tools (8–16 weeks)
    ADAM-style assessment : scoring + shareable artifact
    Labs decoder : structured summary + safety flags
    Cost estimator : region + modality cost model
  section Phase 3 — Programmatic Scale (16–28 weeks)
    Programmatic page expansion : state/city/modality/insurance
    Data hubs + exports : pricing by city + methodology
    Internal linking automation : hub/spoke engine
  section Phase 4 — Provider SaaS (28–44 weeks)
    CRM pipeline : kanban + lead enrichment
    Attribution + ROI : CPL/CPA + cohort reporting
    Match engine v2 : capacity-aware + explainable ranking
  section Phase 5 — Moat (44+ weeks)
    Continuous verification : monitoring + alerts
    Answer-share proxies : AI referrer + export usage analytics
    Public dataset APIs : structured endpoints for partners
10) Quality Bar (“100% Optimal” Definition)
This spec is “done” when:

We can generate thousands of high-quality pages without index bloat

Every clinic page is citation-ready (facts + provenance + timestamps)

Tools produce portable structured artifacts that improve match quality

Providers can measure ROI end-to-end (source → consult → conversion)

Compliance posture is credible: minimization, consent, auditability, separation

11) Policy Decisions (Resolved “Open Questions”)
These policies optimize for end-user trust + shareability.

11.1 Verification scope: Level 2 vs Level 3 (and what badges mean)
Goal: Verification badges must mean something obvious to a user: “I can trust this is real and current.”

Levels

Level 0 — Self-claimed

Provider/clinic submitted, no verification

Display: “Unverified” label; limited distribution

Level 1 — Credential verified

Verify license/NPI (where applicable), clinic identity, contact channels

Verify states served + telehealth availability (basic)

Display: “Verified credentials” badge

Level 2 — Operational verified

Everything in Level 1, plus:

Medical oversight verified (medical director identity/credentials where required)

Pricing model verified (base price + what’s included + add-ons structure)

Insurance acceptance verified (see insurance verification methods below)

Display: “Verified clinic details” badge + “last verified” timestamp

Level 3 — Continuously verified (preferred)

Everything in Level 2, plus:

Continuous monitoring / re-check cadence (see §11.5)

Change-detection + rapid re-verification SLAs

Verified capacity signals (accepting new patients, lead limits) with expiry

Display: “Continuously verified” badge + freshness indicator

How to verify insurance acceptance (practical)

Accepted: written confirmation from clinic + periodically re-confirmed

Optional stronger: screenshots/portal evidence or insurer directory cross-check where feasible

Always disclose verification method in “About this data” on the profile

11.2 Reviews policy: allowed sources + what “verified” means
Goal: Reviews must be believable enough that users will rely on them and share them.

Allowed review types

Verified reviews (first-party): only from users who booked or confirmed a consult through the platform (or otherwise verified via a documented process)

Partner verified reviews (optional): from trusted survey partners with clear provenance labels

Public web reviews (default: off): only if a source is consistent, attributable, and doesn’t degrade trust—if included, label clearly as “Public source (unverified by us)”

Definitions

Verified review: we can tie the reviewer to a real appointment/engagement or verified survey source

Unverified review: anything else (should be hidden or de-emphasized)

Moderation

Remove profanity, hate, impersonation, PHI leakage, personal attacks

No incentives for positive reviews; disclose if incentives exist (prefer none)

UX rule

Always show a provenance label: Verified Patient, Partner Survey, Public Source

Never merge review types into one indistinguishable score without labels

11.3 Pricing schema: inclusive vs add-on fees (no surprises)
Goal: A user should never feel tricked after clicking or calling.

Schema

Primary price shown: the minimum all-in base a typical patient must pay to start, with what’s included

Included items (structured): consults, labs, medication, supplies, follow-ups, messaging

Optional add-ons (structured): fertility add-ons, extra labs, delivery fees, additional consults

Ranges over false precision: show ranges when variability is real

Display rules

If a fee is effectively mandatory for the advertised plan, it must be included in the primary price

If a price can’t be verified, display “self-reported” label and reduce ranking weight (see §11.4)

11.4 Match ranking: hard filters vs soft preferences (trust-first)
Goal: Search must feel like it listens. Breaking filters breaks trust.

Hard filters (never violate silently)

State coverage / telehealth eligibility

Distance / service radius

Modality availability (if explicitly selected)

Insurance acceptance (if explicitly selected and verified)

Capacity constraints (if clinic not accepting new patients / lead cap reached)

Soft preferences (rank boosters)

Price fit (within budget range)

Appointment speed (time-to-book)

User preference profile (frequency tolerance, travel tolerance, etc.)

Review quality (weighted by verification)

Freshness/verification level

Fallback behavior

If strict filters yield too few results, show an explicit section:

“No exact matches—here are close alternatives,” and state which constraint was relaxed.

Explainability requirement

Every match must have a short “Why this fits you” panel:

3–6 bullet reasons + 1 caveat (if any)

11.5 Data freshness: cadence + triggers (reliability is shareable)
Baseline cadence (minimum)

Re-verify core clinic facts every 90 days (or faster for Level 3)

Off-cycle triggers

Provider-initiated changes (publish only after verification)

User reports incorrect info (fast-track re-check)

License status changes (immediate)

“Capacity/accepting patients” fields expire automatically unless reconfirmed

Pricing changes trigger page regen + timestamp update

User-facing freshness

Always show Last verified: YYYY-MM-DD

If stale beyond a threshold: downgrade badge visibility and ranking weight

11.6 Risk posture: clinical phrasing without implied medical advice
Goal: Be helpful, factual, and safe—users trust what feels responsible.

Language rules

Describe options; do not recommend treatment or dosing

Use neutral language: “may,” “can,” “some patients,” “talk to your clinician”

Avoid directives: replace “you should” with “a clinician may consider”

Tool output rules

Summaries are discussion guides, not medical guidance

Safety flags must say: “Seek medical care” / “Contact a clinician urgently”

Never provide dosing, protocols, or individualized treatment recommendations

Disclosure

Prominent disclaimers near outputs + in exports (PDF/JSON)

Appendix A — Example: Clinic “Fact Block” (Human + LLM Friendly)
Founded: 2018

Modality: Telehealth + In-person

States served: TX, FL, CA

Insurance: Aetna (verified), BCBS (pending), Cash-pay

Starting price: $199/mo (membership)

Medical director: Dr. Jane Smith, MD (verified)

Verification: Level 3 (continuously verified)

Last verified: 2026-01-01

Source notes: pricing verified via clinic attestation; insurance verified via clinic confirmation

Appendix B — Example: llms.txt (Experimental, optional)
Place at /llms.txt (or /llm.txt) and keep it short + canonical.

Site: TRT Provider Matchmaking & Verified Clinic Dataset

Canonical entity index: /data/clinic-index

Data hubs:

/data/trt-pricing-by-city (updated monthly)

/data/trt-telehealth-states-served (updated weekly)

Entity pages: /clinics/{slug}

Machine exports:

/exports/clinic-index.json

/exports/trt-pricing-by-city.csv

Update policy: clinic verification every 90 days (or on change request)

Contact: support@domain.com

css
Copy code
