# Product Vision

> **Status:** Draft (Research-Integrated 2025-11-17)
> **Last Updated:** 2025-11-17
> **Working Names:** VegyScan / Veggie Lens / Menu Vision / GreenScan

## Vision Statement

**Transform any foreign-language menu into an interactive, digitally-enriched, vegan/vegetarian-friendly super-menu that looks exactly like the original but explains, translates, and evaluates everything.**

Take a photo of a foreign menu → instantly get an interactive, augmented version that preserves the original layout but adds intelligent overlays, translations, hotspots, and vegan/vegetarian insights.

## Problem Statement (Research-Validated)

> **Research Basis:** Analysis of 50+ vegan/vegetarian traveler stories from Reddit, forums, and travel blogs (Nov 2025)
>
> **Key Finding:** "Meals are the biggest source of travel stress" for vegan/vegetarian travelers. User research recommends: **"Should VegyScan Be Built? Answer: YES, with high confidence."**

### Who
Vegan and vegetarian travelers dining at foreign restaurants with unfamiliar languages and food cultures.

**Target User Validation:**
- **Primary:** Strict ethical vegans (Anna persona), health-oriented vegans (Ben), strict vegetarians (David)
- **Secondary:** Practical vegetarians (Eric), pescatarians (Emma), allergy-constrained users (Clara)
- **Market Size Evidence:** HappyCow has >1M members (4.8★, 100k+ reviews), proving substantial user base exists and pays

---

### Critical Pain Points (Research-Validated)

Through deep user research, we identified **5 critical pain points** with severity and frequency ratings:

#### Pain Point #1: Hidden Non-Obvious Ingredients ⚠️ CRITICAL
**Severity:** Critical | **Frequency:** Very High | **Affects:** ALL vegan/vegetarian travelers

**Research Evidence:**
- **User Quotes:**
  - *"Several times I would order the tofu dish to find it came with unadvertised pork, fish or crab"*
  - *"Strictly 'vegetable' soups usually had egg throughout them"*
  - *"They often make both rice and beans with lard or chicken broth, so that's something to check"*

**Hidden Ingredients Documented:**
- Fish sauce in "vegetable" dishes (Thai, Vietnamese cuisine)
- Dashi (fish stock) in Japanese miso soup, ramen
- Lard in Chinese pastries, Latin American refried beans
- Gelatin in desserts, marshmallows
- Rennet in traditional cheeses
- Butter in "vegan" dishes (miscommunication)

**Current Inadequate Workarounds:**
- Granular questioning ("Does this have fish sauce? Chicken stock? Butter?")
- Researching hidden ingredients by country manually
- Avoiding complex dishes entirely
- Sticking to obviously safe foods (fries, fruit)

**Emotional Impact:** Causes betrayal, guilt, distress. For ethical vegans, accidental consumption is traumatic.

---

#### Pain Point #2: Language Barrier + Cultural Gaps ⚠️ CRITICAL
**Severity:** Critical | **Frequency:** Nearly Universal | **Affects:** ALL travelers in foreign countries

**Research Evidence:**
- **User Quotes:**
  - *"If you say you're vegetarian, you may get served fish... If you say you're vegan, lots of people won't understand"*
  - *"The fact that English was his second language made it difficult to convey what I was trying to avoid... I wondered if he actually understood me"*
  - *"Lots of people don't realize fish isn't vegetarian"*

**Cultural Knowledge Gaps:**
- Local concept of "vegetarian" varies by culture (fish may be included)
- Technical terms invisible to generic translators (Dashi, ghee, rennet)
- Cooking methods not apparent from translation (Belgian fries in animal fat)

**Current Inadequate Workarounds:**
- Using multiple translation tools simultaneously (Google Translate + phrasebooks)
- Carrying Vegan Passport (multilingual explanation cards)
- Listing every forbidden item individually
- Using local terminology ("strict vegetarian" in India)

---

#### Pain Point #3: Trust & Verification Anxiety ⚠️ HIGH
**Severity:** High | **Frequency:** Constant | **Affects:** Safety-conscious users, ethical vegans

**Research Evidence:**
- **User Quotes:**
  - *"I'm having a hard time trusting that things... will actually be vegan, or if something will get lost in translation"*
  - *"I feel nervous/embarrassed/scared asking servers... I wonder if the owner actually understood me"*
  - *"Is anyone else paranoid eating out?"*

**Emotional Impact:** Chronic anxiety, inability to relax during meals, exhaustion from constant vigilance.

**Current Inadequate Workarounds:**
- Double and triple-checking with staff
- Inspecting food closely before eating
- Having backup snacks in case meal is unsafe
- Only eating at explicitly vegan restaurants (limits options)

---

#### Pain Point #4: Time-Intensive Multi-Tool Workflow ⚠️ HIGH
**Severity:** High | **Frequency:** Every Meal | **Affects:** ALL users

**Research Evidence:**
- **User Quotes:**
  - *"I feel like I spend more time translating menus than enjoying my meal"*
  - *"By the time I explained my needs, my friends had often finished their first drink"*
  - *"First I use Google Lens to translate, then I show the waiter my phone with the translated phrase"*

**Current Fragmented Workflow:**
Users employ multiple apps/tools in succession:
1. HappyCow (find restaurant)
2. Google Translate (translate menu)
3. Vegan Passport (explain dietary restrictions)
4. Google Images (research dish names)
5. Reddit (verify hidden ingredients)

**Impact:** 5-10 minutes to decipher menu vs 2 minutes for others. Drawing unwanted attention, analysis paralysis, battery drain, social pressure.

---

#### Pain Point #5: Limited/Boring Food Options ⚠️ MEDIUM-HIGH
**Severity:** Medium-High | **Frequency:** Very Common | **Affects:** Users who avoid complexity

**Research Evidence:**
- **User Quotes:**
  - *"I survived on nuts, french fries, and raw vegetables... apples and bananas when there seemed to be nothing else"*
  - *"I ate rice & beans many days... sometimes even that had pork fat... other nights it was junk food for dinner"*

**Impact:** Missing out on local cuisine, nutritional deficiencies, food fatigue, reduced enjoyment of travel.

---

### Why Current Tools Fail (Competitive Gap Validation)

**Research Finding:** Users combine 2-4 tools because **no single solution addresses the full workflow**. Competitive analysis validates 5 high-priority gaps:

**Google Translate Camera:**
- ✅ Fast, free, ubiquitous (billions of installs)
- ❌ **Zero dietary intelligence** - literal translation only, no hidden ingredient detection
- ❌ No cultural context awareness (doesn't understand Dashi, fish sauce, lard)
- ❌ No order assistance
- **User Quote:** *"Google Translate gives you the words but not the ingredients"*

**ChatGPT with Photo:**
- ✅ Can classify vegan/vegetarian (when prompted)
- ❌ **Slow** (30+ seconds) - causes social pressure at restaurant
- ❌ Loses menu visual structure (unstructured text output)
- ❌ Requires internet, typing, copy-paste workflow
- **User Quote:** *"I still ask the waiter even after translating just to be safe"* (trust gap)

**Menu Translator App (Direct Competitor, 2024):**
- ✅ Menu scanning with dietary icons
- ❌ **Slow** (10 seconds) vs our <2s target
- ❌ **No offline mode** (critical gap for travelers)
- ❌ Uses "educated guess" disclaimers instead of confidence levels (trust gap)
- ❌ No systematic cultural food knowledge

**AnyMenu (Direct Competitor, 2025):**
- ✅ Order builder feature (closes scan→ORDER workflow)
- ❌ **No offline mode** (critical gap)
- ❌ Generic dietary approach, lacks vegan-specific intelligence
- ❌ Very new (no established trust, community)

**HappyCow:**
- ✅ Established brand (>1M members, 4.8★, $4-6 iOS validates WTP)
- ❌ **Different use case** - restaurant discovery, not menu scanning
- ❌ Only finds vegan restaurants, doesn't help at non-vegan establishments

**Validated Opportunity:** NO competitor combines menu translation + dietary filtering + cultural intelligence + offline capability in one purpose-built, iOS-native solution.

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
  - **UI language:** TO BE VALIDATED (Phase 1 market selection)
    - If US/UK market selected: English-first
    - If Germany market selected: German-first
    - If multi-market: English + German from Day 1
  - UI designed with minimal text, maximum icons/colors (universal design)
  - i18n framework used everywhere (enables future translation)
  - Vegan/vegetarian icons language-independent
  - Future: Translate UI to additional languages based on market expansion
  - **Decision driver:** Market selection from Phase 1 survey, not developer familiarity

**Cost Optimization Priority:**

- **LLM/API costs must be minimized** (drives architecture decisions)
  - Offline-first where possible (OCR on-device, aggressive caching)
  - Target: <€0.005 per page in LLM costs (see REQ-NF-013)
  - 70%+ cache hit rate required for business viability

**Deferred to Business Planning:**

- **Business model:** TO BE VALIDATED (Phase 1 survey)
  - Options: One-time purchase, subscription, freemium, hybrid, pay-per-use
  - Not relevant for v1 implementation
  - Constraint: Whatever model chosen, ongoing costs must stay minimal
  - See: [business-case/validation/willingness-to-pay-survey.md](../business-case/validation/willingness-to-pay-survey.md)

- **Target market:** TO BE VALIDATED (Phase 1 survey)
  - Options: US/UK (English), Germany, or multi-market
  - Decision driven by WTP data, iOS penetration, and CAC potential
  - See: [business-case/hypotheses.md](../business-case/hypotheses.md)

- **Price point:** TO BE VALIDATED (Phase 1 Van Westendorp survey)
  - Will be determined by user research, not developer intuition
  - See: [business-case/validation/willingness-to-pay-survey.md](../business-case/validation/willingness-to-pay-survey.md)

---

## Differentiation Strategy

**Core Insight:** LLM power is commoditized. Anyone can call GPT-4/Claude. We don't win on AI - we win on UX.

### Why UX is Our Moat

**The Problem with Competitors:**
- **Google Lens:** Has good AI, but clunky UX for dietary restrictions (generic translation, no dietary intelligence, multiple steps)
- **ChatGPT:** Can classify menus, but slow (30+ seconds), manual (copy-paste), loses visual context
- **Google Translate Camera:** Fast translation, but zero dietary understanding

**Our Advantage:**
- **Purpose-built** for vegan/vegetarian menu scanning (not generic translation)
- **Fast** < 2 seconds scan-to-result (vs 30+ seconds manual ChatGPT)
- **Visual context preserved** (augmented view, not text dump)
- **iOS-native excellence** (one-handed use, Share Extension, VisionKit integration)
- **Zero friction** (point camera, instant results - no copy-paste, no app switching)

**Strategy:** Nail the experience for ONE specific problem (menu scanning), not build features.

### What "Best UX" Means
1. **Speed:** Instant results (< 2 second perceived latency)
2. **Simplicity:** One-handed use in restaurant, no learning curve
3. **Visual context:** Original menu remains center of interaction (augmented, not replaced)
4. **Transparency:** Show reasoning ("Why is this flagged?"), not black box
5. **iOS-native:** Leverage platform (Share Extension, VisionKit, SwiftUI)
6. **Zero leaving app:** All info needed in-app (no Google searches, no asking staff for English menu)

### Positioning
**Tagline:** "The best app for vegan/vegetarian travelers to scan menus"

**Not:** "AI-powered menu translator" (commoditized)
**Instead:** "Purpose-built experience for finding safe dishes abroad" (differentiated)

**Key Messaging:**
- "Same AI power as ChatGPT, but 10x faster and easier"
- "Google Lens translates. We understand."
- "Built for vegans/vegetarians, not everyone"

---

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
- **Revenue per User:** [TO BE VALIDATED - depends on pricing model & price point from Phase 1 survey]
- **Refund Rate:** <2% refund rate (indicates product-market fit)
- **Customer Acquisition Cost (CAC):** <€3 per user (must be profitable at validated price point)

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
- **IMPORTANT:** All pricing assumptions TO BE VALIDATED in Phase 1 survey
- **Revenue per sale:** [TBD - from Van Westendorp survey]
- **App Store fee (30%):** [TBD - depends on final price]
- **Net revenue:** [TBD - 70% of sale price minus App Store fee]
- **Target LLM cost (10 scans/user):** €0.05
- **Available margin:** [TBD - net revenue minus LLM costs]
- **Break-even (covering development):** Depends on development costs and validated price point
- **Example:** Will be calculated in Phase 3 (Business Model Definition) using validated pricing data
- **See:** [business-case/financial-projections.md](../business-case/financial-projections.md) for full analysis

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
