# Experiment 3: Competitor Gap Test

**Status:** ⚪ Not Started
**Priority:** 🟡 HIGH
**Duration:** 3-5 days
**Owner:** [Your Name]

---

## Hypothesis

**Google Lens, ChatGPT, and Google Translate have significant gaps in UX, speed, or accuracy that we can exploit**

**If this fails:** No clear differentiation → Need to find alternative competitive advantage or STOP

---

## Objective

Validate that existing solutions have meaningful gaps that justify building VeggieScan.

**Key Insight:** We're NOT competing on AI power (commoditized). We're competing on UX + speed + purpose-built experience.

**Differentiation Thesis:**
- **Google Lens:** Good AI, clunky UX for dietary restrictions
- **ChatGPT:** Can classify, but slow (30+ seconds), manual, loses visual context
- **Google Translate:** Fast translation, zero dietary understanding

**Our Advantage:**
- Purpose-built for vegan/vegetarian menu scanning
- Fast (< 2 seconds)
- Visual context preserved (augmented view)
- iOS-native excellence
- Zero friction

---

## Competitors to Test

### 1. Google Lens
**What it does:**
- Point camera at text → instant translation
- Can identify objects, products, places
- Free, built into Google app

**Expected Gaps:**
- Generic translation (no dietary intelligence)
- Multiple steps to check each dish
- Loses visual context (shows text dump)
- No reasoning or hidden concerns
- Not vegan/vegetarian-focused

---

### 2. ChatGPT (Mobile App)
**What it does:**
- Text-based AI assistant
- Can classify menu items if you paste text
- Can explain ingredients

**Expected Gaps:**
- Slow (30+ seconds per menu)
- Manual copy-paste required
- Loses visual context (text only)
- No batch processing (one dish at a time)
- No saved history
- Requires switching apps

---

### 3. Google Translate Camera
**What it does:**
- Point camera → live translation overlay
- Works offline (some languages)
- Free, built into Google Translate app

**Expected Gaps:**
- Translation only (no dietary classification)
- No understanding of vegan/vegetarian
- No ingredient analysis
- Still requires user to interpret (is "oyster sauce" vegan?)

---

### 4. Happy Cow (Bonus: Vegan-Specific)
**What it does:**
- Vegan/vegetarian restaurant finder
- Restaurant reviews
- Some menu photos

**Expected Gaps:**
- Doesn't scan menus
- Only finds vegan restaurants (not dishes at non-vegan places)
- No instant classification
- Different use case (discovery, not menu scanning)

---

## Method

### 1. Test Menu Selection (Day 1)

**Use 20 menus from Experiment 1 (LLM Accuracy Test):**
- Diverse cuisines (Italian, Thai, Japanese, Chinese, Indian)
- Diverse languages
- Mix of simple and complex dishes
- Mix of obvious and hidden animal products

**Reuse existing dataset to save time**

---

### 2. Competitive Testing (Days 2-3)

**For each competitor, test all 20 menus and measure:**

#### A. Accuracy
- How many dishes correctly identified as vegan/vegetarian/meat?
- False positives (says safe, but contains animal products) - **CRITICAL ERROR**
- False negatives (says unsafe, but is vegan/vegetarian) - Less critical

#### B. Speed
- Time from "open app" to "get answer for full menu"
- Per-dish time vs batch time
- Include all steps (opening app, taking photo, copy-paste, waiting for response)

#### C. UX Quality (Subjective 1-5 Rating)
- **Ease of use:** How intuitive? How many steps?
- **Visual clarity:** Is it easy to understand results?
- **Context preservation:** Can I still see original menu?
- **Friction:** How many app switches, copy-pastes, manual steps?
- **Confidence:** Does it explain reasoning?

#### D. Feature Gaps
- What's missing?
- What's frustrating?
- What would make it better?

---

### 3. User Testing (Day 4)

**Recruit 3-5 vegan/vegetarian travelers (friends, Reddit, etc.)**

**Task:**
"You're at a Thai restaurant in Bangkok. Use [Competitor X] to find out which dishes you can safely order."

**Observe:**
- Do they succeed?
- How long does it take?
- What frustrations do they express?
- Do they trust the results?

**Conduct for:**
- Google Lens
- ChatGPT
- Google Translate

**Capture quotes and pain points**

---

### 4. Competitive Analysis Matrix (Day 5)

**Create comparison table:**

| Criteria | Google Lens | ChatGPT | Google Translate | Happy Cow | **VeggieScan (Planned)** |
|----------|-------------|---------|------------------|-----------|--------------------------|
| **Accuracy** | ? | ? | N/A | N/A | >90% (from Exp 1) |
| **Speed (full menu)** | ? | ? | ? | N/A | <2 seconds (target) |
| **UX Quality (1-5)** | ? | ? | ? | ? | 5 (goal) |
| **Vegan/Veg Focus** | ❌ | ⚠️ | ❌ | ✅ | ✅ |
| **Visual Context** | ⚠️ | ❌ | ✅ | N/A | ✅ |
| **Batch Processing** | ❌ | ❌ | ❌ | N/A | ✅ |
| **Reasoning Shown** | ❌ | ✅ | ❌ | N/A | ✅ |
| **Offline Mode** | ⚠️ | ❌ | ✅ | ❌ | ✅ (planned) |
| **Saved History** | ❌ | ✅ | ❌ | N/A | ✅ |
| **iOS Native** | ❌ | ❌ | ❌ | ⚠️ | ✅ |
| **Cost** | Free | Free/$20/mo | Free | Free | $X (TBD) |

**Legend:**
- ✅ = Yes / Excellent
- ⚠️ = Partial / OK
- ❌ = No / Poor
- N/A = Not applicable

---

## Gap Analysis

### Hypothesis: Key Differentiators

**1. UX Excellence**
- **Their gap:** Clunky, multi-step, loses context
- **Our advantage:** Purpose-built, single tap, augmented view

**2. Speed**
- **Their gap:** 30+ seconds (ChatGPT), multiple manual steps
- **Our advantage:** < 2 seconds, instant batch results

**3. Purpose-Built for Dietary Restrictions**
- **Their gap:** Generic translation or generic AI (not vegan-focused)
- **Our advantage:** Understands hidden animal products (fish sauce, dashi, ghee, rennet)

**4. Visual Context Preservation**
- **Their gap:** Text dump (Lens, ChatGPT) or no classification (Translate)
- **Our advantage:** Augmented view (original menu + color-coded overlay)

**5. iOS-Native Integration**
- **Their gap:** Web apps or cross-platform (not optimized for iOS)
- **Our advantage:** Share Extension, VisionKit, native SwiftUI, iOS gestures

**6. Trust & Transparency**
- **Their gap:** No reasoning (Lens, Translate) or too verbose (ChatGPT)
- **Our advantage:** Clear reasoning in 1-2 sentences, tap to expand

---

## Success Criteria

### ✅ PASS (Clear Differentiation Exists)

**Criteria:**
- At least 2 significant gaps identified across competitors
- Users express frustration with current tools in user testing
- Our planned solution demonstrably better on UX, speed, or focus
- False positive rate in competitors >5% (accuracy gap)

**Example PASS scenario:**
- Google Lens takes 30+ seconds per menu (vs our <2 seconds)
- ChatGPT has 10% false positive rate (misses fish sauce, dashi)
- All competitors lose visual context (text dump vs augmented view)
- Users say "I wish there was a single app that just worked for this"

**Action:** Proceed with confidence in differentiation strategy

---

### ⚠️ CONDITIONAL (Marginal Differentiation)

**Criteria:**
- Only 1 clear gap identified
- Competitors are "good enough" but not excellent
- Our advantage is incremental, not transformational

**Example CONDITIONAL scenario:**
- Google Lens is actually pretty good (85% accuracy)
- Speed difference is marginal (5 seconds vs 2 seconds)
- Users are "somewhat frustrated" but not "very frustrated"

**Action:**
- Find stronger differentiation (e.g., social features, restaurant reviews)
- Consider if incremental improvement justifies building
- May need to pivot feature set

---

### ❌ FAIL (No Clear Gap)

**Criteria:**
- Competitors already solve problem well
- Users satisfied with current tools
- No meaningful gap in accuracy, speed, or UX
- Our planned solution not significantly better

**Example FAIL scenario:**
- Google Lens has >90% accuracy and fast UX
- Users say "Google Lens works great, I don't need another app"
- No clear UX or speed advantage

**Action:**
- STOP development OR
- Find entirely different angle (e.g., community features, gamification, B2B)

---

## Differentiation Strategy: UX as Moat

**Key Principle:**
> "LLM power is commoditized. Anyone can call GPT-4. We win on UX: speed, simplicity, visual context preservation, iOS-native integration, zero friction."

**Positioning:**
- **NOT:** "AI-powered menu translator" (commoditized)
- **INSTEAD:** "The best app for vegan/vegetarian travelers to scan menus"

**Why UX is defensible:**
- Requires deep user research (we're doing this)
- Requires iOS expertise (native development)
- Requires taste and design sense (not just engineering)
- Hard to copy (anyone can copy AI, hard to copy great UX)

**Examples of UX moats:**
- Instagram (photos existed, but Instagram made it delightful)
- Stripe (payments existed, but Stripe made it developer-friendly)
- Superhuman (email existed, but Superhuman made it fast)

**Our version:**
- Menu scanning exists (Google Lens, ChatGPT)
- VeggieScan makes it delightful for vegan/vegetarian travelers

---

## User Pain Points to Document

**From user testing, capture quotes like:**
- "I have to look up each dish individually on ChatGPT - takes forever"
- "Google Lens translates, but I still don't know if fish sauce is vegan"
- "I lose the menu context - just see a wall of translated text"
- "I'm anxious I'll miss hidden ingredients and accidentally eat meat"
- "I wish there was one app that just worked for this specific problem"

**Use these quotes in:**
- Marketing copy
- Product positioning
- Investor pitch (if applicable)

---

## Tools & Budget

**Required:**
- Test devices: iPhone with Google Lens, ChatGPT, Google Translate apps
- Stopwatch or screen recording for timing
- Spreadsheet for tracking results
- 3-5 vegan/vegetarian travelers for user testing

**Estimated Budget:**
- $0 (using free tools and friends for testing)

**Time:**
- Setup: 2 hours
- Competitive testing: 8 hours (20 menus × 3 competitors)
- User testing: 6 hours (3 users × 2 hours each)
- Analysis: 4 hours

**Total Effort:** ~20 hours over 3-5 days

---

## Deliverables

1. ✅ Competitive analysis matrix (accuracy, speed, UX)
2. ✅ Gap analysis (where competitors fall short)
3. ✅ User testing quotes and pain points
4. ✅ Differentiation strategy (why we're better)
5. ✅ Decision: GO / CONDITIONAL / NO-GO

**Document findings in:** [DECISIONS.md](./DECISIONS.md)

---

## Next Steps

**If PASS:**
- Use differentiation insights in product design
- Use user quotes in marketing copy
- Proceed to Phase 2 with confidence

**If CONDITIONAL:**
- Explore additional differentiation (features, community, B2B)
- Consider if incremental improvement is enough
- Reassess product strategy

**If FAIL:**
- Stop development OR
- Major pivot (different use case, different audience)

---

**Last Updated:** 2024-11-17
**Status:** ⚪ Not Started
**Owner:** [Your Name]
