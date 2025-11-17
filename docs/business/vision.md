# Product Vision

> **Status:** Draft
> **Last Updated:** 2025-11-15
> **Working Names:** VegyScan / Veggie Lens / Menu Vision / GreenScan

## Vision Statement

**Transform any foreign-language menu into an interactive, digitally-enriched, vegan/vegetarian-friendly super-menu that looks exactly like the original but explains, translates, and evaluates everything.**

Take a photo of a foreign menu → instantly get an interactive, augmented version that preserves the original layout but adds intelligent overlays, translations, hotspots, and vegan/vegetarian insights.

## Problem Statement

### Who
Travelers (especially vegans, vegetarians, and people with dietary restrictions) visiting foreign countries with unfamiliar languages and food cultures.

### What Problems

**1. Language Barriers**
- Unfamiliar writing systems (Japanese, Korean, Thai, Arabic, etc.)
- Mixed-language menus with poor translations
- Translations alone don't explain what the dish actually is
- Complex menu layouts with scattered information

**2. Dietary Uncertainty**
- Hidden animal ingredients in traditional dishes
- Cooking methods (e.g., Belgian fries fried in animal fat)
- Broths made with bones/fish (Dashi, Tonkotsu)
- Local standards and traditions unknown to travelers
- Symbols and allergen info not understood

**3. Current Tools Are Inadequate**

**Google Translate Camera:**
- Doesn't recognize which texts belong together
- No menu context understanding
- No dish explanations
- No vegan/vegetarian intelligence
- No country/cultural context
- No interactivity
- Can't handle multi-page menus

**ChatGPT with Photo:**
- Delivers unstructured text output
- Loses menu visual structure
- No interactive UX
- Often slow
- Uncertain classifications without context
- Hard to use for actual ordering (you still point at the original)

## Goals

1. **Enable confident ordering** for vegans/vegetarians in any foreign restaurant
2. **Preserve visual context** while adding digital intelligence (augmented, not replaced)
3. **Be faster and more accurate** than Google Translate or ChatGPT for menu understanding
4. **Provide transparent reasoning** for vegan/vegetarian classifications
5. **Create intuitive, instant UX** that feels native to mobile dining experiences

## Strategic Scope

_For detailed features, see [Functional Requirements](./requirements/functional.md) - the Single Source of Truth for all features._

### What We're Building (High-Level)

An iOS-native app that transforms foreign-language menus into interactive, augmented experiences through:
1. **Visual preservation** - the original menu remains the center of interaction
2. **Intelligent augmentation** - translations, classifications, and insights overlaid on the original
3. **Vegan/vegetarian intelligence** - diet-specific classification with transparent reasoning
4. **Instant UX** - perceived response time < 2 seconds (lazy loading, progressive disclosure)

### What We're NOT Building (Strategic Boundaries)

**Out of scope for v1:**
- **Community features** - community-shared scans, user feedback, ratings (v2+ consideration)
- **User accounts/sign-in** - no cloud authentication, local-only storage for v1
- **Allergen tracking** beyond vegan/vegetarian (future v2+ consideration - complexity and liability)
- **Nutritional information** (calories, macros) - different value proposition
- **Recipe suggestions** or cooking instructions - not menu-focused
- **Web version** - iOS-only focus for v1 (leverage native capabilities)
- **Android app** - iOS-only focus for v1 (resource constraints)

**Strategic reasons:**
- **Focus on core value:** Vegan/vegetarian travelers need menu understanding, not social features or nutritional tracking
- **Minimize complexity:** Community features require cloud storage, moderation, different architecture
- **Privacy-first:** Local-only storage, no account required, works offline
- **Leverage iOS-native:** VisionKit, Core ML, SwiftUI capabilities maximize quality and minimize development time
- **Manage complexity:** Allergen tracking adds legal liability and requires different accuracy standards
- **Resource constraints:** Single platform initially allows faster iteration and learning
- **Future-compatible:** v1 architecture designed to be extensible (not rebuildable) when adding community features later

### Strategic Decisions and Constraints

_These guide v1 implementation without specifying HOW._

**v1 Scope Constraints:**

- **Community features:** OUT of v1 scope
  - Community-shared scans, user feedback, social features deferred to v2+
  - Rationale: Requires cloud storage, different architecture, increased complexity
  - **Critical:** v1 architecture must be future-compatible (extensible, not rebuildable)
  - Design foundation that can be extended with cloud features later

- **User profiles/sign-in:** NOT required for v1
  - No account creation, no cloud authentication
  - User preferences stored locally on device only
  - Rationale: Keeps v1 simple, privacy-friendly, works offline
  - Note: May be needed later if business model requires subscription/billing

- **Language/Internationalization:**
  - v1 launches in English
  - UI designed with minimal text, maximum icons/colors (universal design)
  - i18n framework used everywhere (enables future translation)
  - Vegan/vegetarian icons language-independent
  - Future: Translate UI to German, French, etc. without redesign

**Cost Optimization Priority:**

- **LLM/API costs must be minimized** (drives architecture decisions)
  - Offline-first where possible (OCR on-device, aggressive caching)
  - Target: <€0.005 per page in LLM costs (see REQ-NF-013)
  - 70%+ cache hit rate required for business viability

**Deferred to Business Planning:**

- **Business model:** One-time purchase vs. subscription vs. freemium
  - Not relevant for v1 implementation
  - Constraint: Whatever model chosen, ongoing costs must stay minimal

## Success Criteria

**User Experience:**
- Feels "instant" (< 2 seconds perceived response time)
- User can confidently order vegan/vegetarian food in foreign restaurant
- Original menu remains center of interaction (not replaced)
- No information overload (progressive disclosure)

**Technical:**
- High accuracy symbol recognition (>95%)
- Correct meta-info bundling (all dish components grouped)
- Reliable vegan/vegetarian classification with transparent reasoning
- Cost-efficient LLM usage (maximize on-device processing)

**Business:**
- Users willing to pay for app (validates value proposition)
- Better than free alternatives (Google Translate, ChatGPT)
- Positive reviews highlighting speed, accuracy, and trust

## Post-Launch Success Metrics

**Product Metrics (First 3 Months):**
- **Downloads:** 10,000 total downloads
- **Active Users:** 60% retention after 1 week, 40% retention after 1 month
- **Engagement:** Average 5+ menus scanned per active user per trip
- **Feature Adoption:**
  - 70%+ of users scan at least one menu
  - 40%+ of users use history feature
  - 20%+ of users try iOS Share Extension (UC-007)
  - 30%+ of users favorite at least one dish

**User Experience Metrics:**
- **Onboarding:** 90% of users complete first scan within 2 minutes of opening app
- **Success Rate:** <5% error rate on scans (OCR failures, network errors combined)
- **Performance:** 95% of scans complete in <2 seconds (perceived response time)
- **Satisfaction:** 4.5+ stars average rating on App Store
- **Customer Support:** <2% of users contact support (indicates good UX)

**Business Metrics:**
- **LLM Cost Efficiency:** <€0.005 per page in LLM API costs (CRITICAL for viability)
- **Cache Hit Rate:** 70%+ cache hit rate for returning users
- **Revenue per User:** €8 net revenue per sale (before API costs, after App Store fees)
- **Refund Rate:** <2% refund rate (indicates product-market fit)
- **Customer Acquisition Cost (CAC):** <€3 per user (must be profitable at €8 price)

**Technical Health Metrics:**
- **Crash Rate:** <0.5% sessions (industry standard: <1%)
- **API Uptime:** 99.5%+ availability (dependent on LLM provider)
- **OCR Success Rate:** 85%+ of photos successfully extract text
- **Classification Accuracy:** 90%+ accuracy on vegan/vegetarian classification (measured via user feedback in v2)

**Growth Metrics (3-6 Months):**
- **Organic Growth:** 60%+ of downloads from organic (App Store search, word-of-mouth, Share Extension)
- **Viral Coefficient:** >1.2 (each user brings 1.2 new users via sharing)
- **Geographic Expansion:** Users in 10+ countries
- **Month-over-Month Growth:** 20%+ growth in monthly active users

**Analytics Implementation (REQ-NF-024):**
- **Privacy-First:** No third-party analytics, custom implementation or TelemetryDeck
- **User Opt-In:** Analytics opt-in required (GDPR compliance)
- **Metrics Tracked:**
  - Scans per session, scans per user, scans per trip
  - Feature usage: Upload vs Camera, Share Extension usage, History views
  - Error rates: OCR failures, network failures, LLM errors
  - Cache hit rates: Menu-level, dish-level, perceptual hash
  - Performance: Time to first scan, scan processing time, UI responsiveness
- **NO Tracking:**
  - No personally identifiable information (PII)
  - No location data (respect privacy)
  - No menu content (privacy-sensitive)
  - No cross-session user tracking

**Success Thresholds:**

**Green (Exceeding Expectations):**
- 10,000+ downloads in first 3 months
- 4.7+ star rating
- <€0.003 per page LLM costs
- CAC <€2

**Yellow (Meeting Expectations):**
- 5,000-10,000 downloads
- 4.3-4.7 star rating
- €0.003-0.005 per page costs
- CAC €2-3

**Red (Below Expectations - Action Required):**
- <5,000 downloads in 3 months → Increase marketing, improve ASO
- <4.0 star rating → Critical UX issues, fix immediately
- >€0.005 per page costs → Business model unsustainable, pivot pricing or caching
- CAC >€3 → Cannot scale profitably, focus on organic growth

**Break-Even Analysis:**
- **Revenue per sale:** €8
- **App Store fee (30%):** €2.40
- **Net revenue:** €5.60
- **Target LLM cost (10 scans/user):** €0.05
- **Available margin:** €5.55 per user
- **Break-even (covering development):** Depends on development costs (TBD)
- **Example:** If development costs €20,000, need 3,600 sales to break even

**Long-Term Success Indicators (6-12 Months):**
- Sustainable growth without paid advertising (organic CAC <€3)
- Strong App Store ratings (4.5+) indicating product-market fit
- Low churn (users return app on subsequent trips)
- Feature requests indicate engagement (users care enough to suggest improvements)
- Competitor validation (others enter space = market confirmed)

## Target Users

_[Detailed personas in [personas.md](./personas.md)]_

**Primary:**
- Vegans and vegetarians traveling abroad
- Travelers in countries with unfamiliar writing systems
- Digital nomads and backpackers

**Secondary:**
- Flexitarians
- People with food allergies
- Anyone seeking to understand foreign menus better

**Context:**
- Active travelers (not daily use)
- Likely use case: 1-3 weeks per trip, several trips per year
- High willingness to pay during travel (part of trip budget)
