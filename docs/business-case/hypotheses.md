# VeggieScan - Open Hypotheses & Questions

**Last Updated:** 2024-11-17
**Purpose:** Track all questions that need data-driven answers

**Principle:** No hard-coded assumptions. Every strategic decision validated with data.

---

## 🔴 Critical Questions (Must Answer in Phase 1)

### 1. LLM Classification Accuracy
**Question:** Can GPT-4, Claude, or Gemini achieve >90% accuracy on vegan/vegetarian classification?

**Current Status:** ❓ Unknown
**Validation Method:** [validation/llm-accuracy-test.md](./validation/llm-accuracy-test.md)
**Decision Criteria:**
- ✅ PASS: >90% accuracy, cost <€0.005/page
- ⚠️ CONDITIONAL: 85-90% accuracy
- ❌ FAIL: <85% accuracy

**Impact if FAIL:** Core value proposition fails → STOP or pivot to translation-only

---

### 2. Pricing Model
**Question:** Which monetization model maximizes user adoption AND revenue?

**Options:**
- A) One-time purchase at $X
- B) Monthly subscription at $Y/month
- C) Annual subscription at $Z/year
- D) Freemium (X free scans, then $Y/month)
- E) Hybrid (one-time unlock + optional add-ons)

**Current Status:** ⚠️ **Partial Evidence** (not validated)
**Evidence from Competitive Research (2025-11-17):**
- **Willingness to pay EXISTS**: HappyCow ($4-6 iOS one-time), Waygo ($6 one-time), Vegan Passport ($2 one-time) all have paying users
- **One-time purchase models work**: HappyCow users say "well worth it", Waygo users say "so worth the cost"
- **Freemium exists**: Menu Translator App uses freemium (unknown conversion rate)
- **⚠️ LIMITATION**: Research shows pain points, NOT which pricing model works best for VegyScan

**Validation Method:** [validation/willingness-to-pay-survey.md](./validation/willingness-to-pay-survey.md)
**Decision Criteria:**
- Test all options in survey (one-time vs. subscription vs. freemium)
- Choose option with:
  - Highest willingness to pay (60%+ say yes)
  - Best LTV potential
  - Simplest implementation for v1

**Impact if no clear winner:** May need hybrid model or regional pricing

---

### 3. Price Point
**Question:** What price maximizes revenue without hurting adoption?

**Current Status:** ⚠️ **Market Range Identified** (not validated for VegyScan)
**Evidence from Competitive Research (2025-11-17):**
- **$4-8 range exists in market**: HappyCow $4-6, Waygo $6, Vegan Passport $2
- **Users willing to pay mid-range**: "Well worth it" sentiment for $4-6 range
- **⚠️ LIMITATION**: Shows existing prices, NOT optimal price for VegyScan specifically

**Validation Method:** Van Westendorp pricing survey
**Test Range:** $2.99, $4.99, $7.99, $9.99 (bracket around competitive range)
**Decision Criteria:**
- "Too cheap" price point
- "Good value" price point
- "Too expensive" price point
- Optimal price = intersection of curves

**Impact if too low:** Business model not viable
**Impact if too high:** Low adoption, high CAC

---

### 4. Target Market
**Question:** Which market should we launch in first?

**Options:**
- A) US market (English, high WTP, 50%+ iOS penetration)
- B) UK market (English, high WTP, 50%+ iOS)
- C) Germany (familiar, but lower WTP, 30% iOS)
- D) Multi-market (English + German from Day 1)
- E) Other (data may reveal unexpected opportunity)

**Current Status:** ⚠️ **Signals Point to US/UK** (not validated)
**Evidence from Competitive Research (2025-11-17):**
- **Vegan communities are English-dominant**: Reddit (r/vegan, r/vegantravel), forums documented as English-first
- **HappyCow's iOS-first strategy worked**: $4-6 iOS model successful (100k+ reviews, >1M members)
- **Germany not mentioned** in competitive research as primary market
- **⚠️ LIMITATION**: Research shows where vegan travelers are active online, NOT validated market size or WTP by region

**Validation Method:** Market-specific WTP analysis + competitive research (needs CAC data per region)
**Decision Criteria:**
- Highest WTP
- Best iOS penetration in target demo
- Lowest competitive intensity
- Easiest organic acquisition (CAC potential)

**Selection:** Data-driven, not familiarity-driven

**Impact:** Affects localization, marketing, pricing strategy

---

### 5. Competitive Differentiation
**Question:** Do Google Lens, ChatGPT, and Google Translate have significant gaps we can exploit?

**Current Status:** ✅ **VALIDATED** (5 high-priority gaps documented)
**Evidence from Competitive Research (2025-11-17):**

**GAP 1: Hidden Ingredient Detection (#1 Pain Point)**
- User quotes: "Fish sauce is EVERYWHERE", "Dashi not listed on Japanese menus", "Google gives words not ingredients"
- NO competitor has systematic cultural food knowledge
- Menu Translator App uses "educated guess" disclaimers

**GAP 2: Offline Functionality**
- Menu Translator App: NO offline mode
- AnyMenu: NO offline mode
- Users: "Mountain hut with no signal", "expensive roaming"

**GAP 3: Speed (In-Restaurant UX)**
- Menu Translator: "usually within 10 seconds"
- ChatGPT: 30+ seconds
- Users: "Holding up the line", "feeling rushed"

**GAP 4: Trust Through Transparency**
- All competitors: Black-box AI or disclaimers
- Users: "Still ask waiter even after translating", "wouldn't trust when it really mattered"

**GAP 5: Pre-Visit Planning (Share Extension)**
- NO competitor has iOS Share Extension
- Users research on Google Maps but must manually screenshot/upload

**Validation Method:** Competitive analysis complete. See [competitor-analysis.md](./competitor-analysis.md)
**Decision Criteria:** ✅ PASSED
- Clear gaps documented with user quotes
- Users frustrated with current tools (trust, speed, offline, hidden ingredients)
- VegyScan solution addresses all 5 gaps

**Impact:** Clear differentiation strategy validated. Proceed with build.

**Key Differentiator (Hypothesis):** UX excellence, not AI power
- LLM power is commoditized (anyone can call GPT-4)
- We win on: purpose-built UX, speed, visual context, iOS integration
- "Same AI, 10x better experience"

---

### 6. User Pain Points Exist & Are Severe
**Question:** Do vegan/vegetarian travelers experience severe, frequent pain points when ordering abroad that justify building this product?

**Current Status:** ✅ **VALIDATED** (Research-backed evidence)
**Evidence from User Research (2025-11-17):**

**Critical Validation from [User Research Report](../business/user-research-report.md):**
- **50+ user stories analyzed** from Reddit, forums, travel blogs
- **5 critical pain points identified** with severity and frequency ratings
- **Emotional impact documented**: "Meals are the biggest source of travel stress" for this user group
- **Strong recommendation**: "Should VegyScan Be Built? Answer: YES, with high confidence"

**Pain Point #1: Hidden Non-Obvious Ingredients** (⚠️ CRITICAL Severity, Very High Frequency)
- User quotes: "Several times I would order tofu to find it came with unadvertised pork", "Strictly 'vegetable' soups usually had egg throughout them"
- Affects: ALL vegan/vegetarian travelers, especially in Asia
- Current solution: Granular questioning, avoiding complex dishes entirely (inadequate)

**Pain Point #2: Language Barrier + Cultural Gaps** (⚠️ CRITICAL Severity, Nearly Universal)
- User quotes: "If you say you're vegetarian, you may get served fish", "Lots of people don't realize fish isn't vegetarian"
- Affects: ALL travelers in foreign countries
- Current solution: Multiple translation tools + phrasebooks (inadequate)

**Pain Point #3: Trust & Verification Anxiety** (⚠️ HIGH Severity, Constant Frequency)
- User quotes: "I'm having a hard time trusting... if something will get lost in translation", "Is anyone else paranoid eating out?"
- Affects: Safety-conscious vegans, ethical vegans
- Emotional impact: Chronic anxiety, inability to relax during meals

**Pain Point #4: Time-Intensive Multi-Tool Workflow** (⚠️ HIGH Severity, Every Meal)
- User quotes: "I feel like I spend more time translating menus than enjoying my meal", "By the time I explained my needs, my friends had often finished their first drink"
- Workflow: HappyCow + Google Translate + Vegan Passport + research (5-10 minutes per meal)
- Affects: ALL users, social pressure, battery drain

**Pain Point #5: Limited/Boring Food Options** (⚠️ MEDIUM-HIGH Severity, Very Common)
- User quotes: "I survived on nuts, french fries, and raw vegetables", "I ate rice & beans many days... sometimes even that had pork fat"
- Affects: Users who avoid complexity due to uncertainty
- Impact: Nutritional deficiencies, reduced enjoyment of travel

**Validation Method:** Deep user research complete. See [user-research-report.md](../business/user-research-report.md)

**Decision Criteria:** ✅ PASSED
- Pain points are **severe** (CRITICAL to HIGH severity ratings)
- Pain points are **frequent** (Very High to Constant frequency)
- Pain points are **underserved** (current tools inadequate)
- Users **explicitly wish for this solution**: "Users explicitly wish for this solution" documented in research

**Impact:** Market need validated. Problem severity justifies dedicated solution.

---

### 7. Features Align with User Needs
**Question:** Do our planned features directly address the documented user pain points?

**Current Status:** ✅ **VALIDATED** (Research-mapped to requirements)
**Evidence from User Research + Requirements Mapping (2025-11-17):**

**Pain Point → Feature Mapping:**

| Pain Point | Severity | Planned Feature | Requirement | Validation |
|------------|----------|----------------|-------------|------------|
| **Hidden Ingredients** | CRITICAL | Cultural Intelligence Database | REQ-F-012 | ✅ Direct match |
| **Language + Cultural Gaps** | CRITICAL | Multi-language translation + Context | REQ-F-006, REQ-F-012 | ✅ Direct match |
| **Trust & Verification Anxiety** | HIGH | Confidence Scoring + Reasoning | REQ-F-009, REQ-F-010 | ✅ Direct match |
| **Time-Intensive Workflow** | HIGH | Speed <2s + Offline Caching | REQ-NF-001, REQ-F-029-031 | ✅ Direct match |
| **Limited Food Options** | MEDIUM-HIGH | Menu scanning + Symbol recognition | REQ-F-001, REQ-F-004 | ✅ Direct match |

**Feature Validation Examples:**

**REQ-F-012 (Cuisine Context Awareness) → Addresses Pain Point #1**
- User need: Detect fish sauce, Dashi, lard, gelatin (hidden ingredients)
- User quote: "They often make rice and beans with lard or chicken broth"
- Our solution: Systematic cultural food trap database by cuisine
- Research validation: "KILLER DIFFERENTIATOR" - no competitor has this

**REQ-F-009 + REQ-F-010 (Confidence + Reasoning) → Addresses Pain Point #3**
- User need: Trust in classification results
- User quote: "I'd pay good money for something I knew I could trust 100%"
- Our solution: Transparent confidence levels (⚫⚫⚫/⚫⚫◯/⚫◯◯) + reasoning
- Research validation: Competitive gap - all competitors use black-box AI or disclaimers

**REQ-NF-001 (Speed <2s) → Addresses Pain Point #4**
- User need: Fast results without social pressure
- User quote: "I felt awkward taking forever to order while everyone waited"
- Our solution: <2 second response time (5x faster than Menu Translator's 10s)
- Research validation: Competitive gap - Menu Translator 10s, ChatGPT 30s+

**REQ-F-029-031 (Offline Caching) → Addresses Pain Point #4**
- User need: Works without internet connection
- User quote: "Mountain hut with no signal", "expensive roaming charges"
- Our solution: Smart caching with 70%+ hit rate target
- Research validation: Competitive gap - Menu Translator & AnyMenu have NO offline mode

**Validation Method:** Requirements mapped to research. See [user-research-report.md](../business/user-research-report.md#must-have-features-mvp)

**Decision Criteria:** ✅ PASSED
- All 5 critical pain points have corresponding features
- Features are research-validated, not assumed
- Competitive gaps confirm features are differentiated
- User research explicitly recommends these features

**Impact:** Feature set validated. Confidence to build.

---

## 🟡 High-Priority Questions (Answer in Phase 2)

### 8. iOS VisionKit OCR Reliability
**Question:** Can iOS VisionKit extract text from 80%+ of real-world menus?

**Current Status:** ❓ Unknown
**Validation Method:** Test 100 menus with VisionKit
**Decision Criteria:**
- ✅ PASS: >80% success rate
- ⚠️ CONDITIONAL: 70-80% (need better UX guidance)
- ❌ FAIL: <70% (need alternative OCR)

---

### 9. LLM Cost Management
**Question:** Can we achieve <€0.005 per page through caching?

**Current Status:** ❓ Unknown (target: 70%+ cache hit rate)
**Validation Method:** Simulate with 100 menus + user behavior model
**Decision Criteria:**
- ✅ PASS: 70%+ cache hit rate simulated
- ⚠️ CONDITIONAL: 60-70% (adjust pricing)
- ❌ FAIL: <60% (business model at risk)

---

### 10. Development Timeline
**Question:** Can solo dev with AI assistance build MVP in 6-12 months?

**Current Status:** ❓ Unknown
**Validation Method:** Feature breakdown + time estimation
**Decision Criteria:**
- Realistic timeline based on scope
- Can build MVP before market opportunity closes
- Can sustain effort for duration (side hustle)

---

### 11. Break-Even Analysis
**Question:** How many paying users needed to cover costs and generate sustainable side income?

**Current Status:** ❓ Unknown (depends on pricing, costs)
**Validation Method:** Financial modeling (Phase 3)
**Decision Criteria:**
- Break-even achievable within 18-24 months
- Reasonable user count (not 100K+ users needed)

---

## 🟢 Medium-Priority Questions (Answer in Phase 3+)

### 12. Customer Acquisition Strategy
**Question:** Which channels can acquire users at <€3 CAC?

**Current Status:** ❓ Unknown (hypothesis: organic via Reddit, Share Extension)
**Validation Method:** Channel experiments (post-MVP)

---

### 13. User Retention
**Question:** What retention rate can we expect (D7, D30)?

**Current Status:** ❓ Unknown (seasonal usage pattern expected)
**Validation Method:** Beta testing + post-launch analytics

---

### 14. LTV Optimization
**Question:** Which features drive long-term value and reduce churn?

**Current Status:** ❓ Unknown
**Validation Method:** Post-launch user behavior analysis

---

## ❌ Removed Assumptions (Previously Hard-Coded)

**These were assumptions that have been REMOVED:**

### Pricing Model: One-Time Purchase
**Previous Assumption:** €8 one-time purchase
**Removed:** 2024-11-17
**Reason:** Solo dev bias toward one-time purchase (personal preference), but subscription may have better LTV. Must validate with users, not assume.
**Now:** Question #2 (to be validated in Phase 1)

### Target Market: Germany First
**Previous Assumption:** Launch in Germany (familiar market)
**Removed:** 2024-11-17
**Reason:** Familiarity bias. Business logic suggests US/UK may be better (higher WTP, more iOS users). Personal comfort shouldn't override data.
**Now:** Question #4 (to be validated in Phase 1)

### Price Point: €8
**Previous Assumption:** €8 is the right price
**Removed:** 2024-11-17
**Reason:** Developer intuition, not user research. Must validate optimal price point.
**Now:** Question #3 (to be validated with Van Westendorp survey)

### English UI with German Localization
**Previous Assumption:** English-first, German later
**Removed:** 2024-11-17
**Reason:** Depends on market selection (Question #4). If DE market wins, German-first makes more sense.
**Now:** Conditional on Question #4 answer

---

## 📋 Validation Tracker

| # | Question | Phase | Status | Method | Decision | Date |
|---|----------|-------|--------|--------|----------|------|
| 1 | LLM accuracy >90%? | 1 | ⚪ | Exp 1 | TBD | TBD |
| 2 | Which pricing model? | 1 | ⚪ | Exp 2 | TBD | TBD |
| 3 | What price point? | 1 | ⚪ | Exp 2 | TBD | TBD |
| 4 | Which market? | 1 | ⚪ | Exp 2+4 | TBD | TBD |
| 5 | Competitive gap? | 1 | ✅ | Competitive Research | PASS | 2025-11-17 |
| 6 | User pain points severe? | 0 | ✅ | User Research | PASS | 2025-11-17 |
| 7 | Features align with needs? | 0 | ✅ | Requirements Mapping | PASS | 2025-11-17 |
| 8 | VisionKit reliable? | 2 | ⚪ | Testing | TBD | TBD |
| 9 | LLM costs viable? | 2 | ⚪ | Simulation | TBD | TBD |
| 10 | Timeline realistic? | 2 | ⚪ | Estimation | TBD | TBD |
| 11 | Break-even users? | 3 | ⚪ | Financial model | TBD | TBD |

---

## 🎯 Decision-Making Principles

**How we make decisions:**
1. **Data-driven, not assumption-driven** - Validate every hypothesis
2. **User research over developer intuition** - What users want, not what we think
3. **Business logic over personal comfort** - Best market, not familiar market
4. **Optimize for LTV, not just price** - Long-term value, not one-time extraction
5. **UX as differentiator** - Win on experience, not technology

**When to challenge assumptions:**
- Developer says "I prefer X" → Ask "What do users prefer?"
- Feeling says "X is easier" → Ask "What does data say?"
- Intuition says "X will work" → Ask "How do we validate?"

---

**Last Updated:** 2025-11-17
**Owner:** [Your Name]
**Next Review:** After each experiment completes
