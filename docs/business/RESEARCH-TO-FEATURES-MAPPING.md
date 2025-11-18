# Research Insights → Product Features Mapping

**Date:** 2025-11-18
**Research Source:** "Global Vegan Menu Scanning Challenges: Geography, Cuisine, and Language Insights" (31 pages)
**Purpose:** Map deep research findings to concrete product features and vision elements

---

## Executive Summary

Your research provides **exceptional depth** on:
1. ✅ Which cuisines are most problematic (Thai, Japanese = Very High)
2. ✅ Which countries have which hidden ingredients (detailed database)
3. ✅ OCR/language difficulty by script (Thai, Japanese, Arabic challenges)
4. ✅ Market prioritization (US/UK primary, Germany secondary)
5. ⭐ **NEW:** Modification feasibility patterns (easy/moderate/impossible)
6. ⭐ **NEW:** Country-specific modification culture (Japan rarely accepts, Thailand flexible)

**Status:**
- ~70% of research insights ALREADY captured in existing requirements
- ~30% are NEW insights requiring new features (modification feasibility, country culture)

---

## Mapping Table: Research → Existing Features

| Research Insight | Status | Location in Specs | Notes |
|-----------------|--------|-------------------|-------|
| **Cuisine Problem Intensity Rankings** | 🟡 Partial | REQ-F-042 mentions cuisines but not intensity ranking | Need to add: REQ-F-056 (Problem Intensity Ranking) |
| **Hidden Ingredients by Cuisine** | ✅ Captured | REQ-F-042: Cultural Context Database | Thai fish sauce, Japanese dashi, Chinese oyster sauce all documented |
| **Language/Script OCR Difficulty** | ❌ Missing | Not in functional requirements | Should be in technical/architecture specs (Phase 1/2/3 rollout) |
| **Market Prioritization (US/UK/Germany)** | ✅ Captured | Business Case (hypotheses.md, market-analysis.md) | Well documented in business layer, not in product layer |
| **Cultural Dietary Concept Variations** | ✅ Captured | REQ-F-042: Cultural Notes section | "Vegetarian in Japan may include fish" documented |
| **Local Language Phrases** | ✅ Captured | REQ-F-043: Smart Vegan Passport, REQ-F-044: Modification Questions | "เจ" (jay) in Thailand, specific phrases per culture |
| **⭐ Modification Feasibility Levels** | ⭐ NEW | → REQ-F-054 (NEW) | Easy (leave out) / Moderate (substitute) / Impossible (cooked in) |
| **⭐ Country Modification Culture** | ⭐ NEW | → REQ-F-055 (NEW) | Japan traditional = rarely accepts, Thailand street = flexible |
| **⭐ Cuisine-Specific Modification Patterns** | ⭐ NEW | → REQ-F-054, REQ-F-055 (NEW) | "Curry paste pre-made = impossible, cheese topping = easy" |
| **Menu-Level Difficulty Assessment** | ⭐ NEW | → REQ-F-057 (NEW) | Show users "This menu is CHALLENGING" vs. "VEGAN-FRIENDLY" |
| **Community Dish Recognition** | ✅ Captured | REQ-F-053: Community Dish Confirmation (v1.5) | "Same restaurant, different branches vary" documented |
| **Local Safe Dishes** | ✅ Captured | REQ-F-042: Safe local dishes section | Example: Edamame in Japan, Hummus in Middle East |
| **Watch-Out Dishes** | ✅ Captured | REQ-F-042: Watch-out dishes section | Belgian fries (animal fat), Chinese vegetable dishes (oyster sauce) |

**Legend:**
- ✅ Captured = Already in requirements
- 🟡 Partial = Mentioned but not detailed
- ⭐ NEW = New insight, requires new feature
- ❌ Missing = Not captured anywhere

---

## Detailed Mapping: Research Sections → Features

### 1. Problem Intensity by Cuisine

**Research Insight:**
> Ranking of cuisines by how frequently hidden animal ingredients appear:
> - 🔴 Very High: Thai (fish sauce), Japanese (dashi)
> - 🟡 High: Chinese (oyster sauce), Vietnamese, Korean
> - 🟢 Lower: Indian (ghee but disclosed), Middle Eastern, Mexican

**How This Maps to Product:**

✅ **ALREADY CAPTURED:**
- REQ-F-042: Cultural Context Database includes hidden ingredients per cuisine
- REQ-F-012: Cuisine Context Awareness applies cuisine-specific rules

⭐ **NEW FEATURE NEEDED:**
- **REQ-F-056: Cuisine Problem Intensity Ranking**
  - Assign intensity levels (Very High/High/Lower) to each cuisine
  - Use this to prioritize warnings ("⚠️ Thai cuisine uses fish sauce in 80%+ of dishes")
  - Show first-scan educational tips for Very High cuisines
  - Adjust confidence levels (Thai dish "appears vegan" → lower confidence, ask to verify)

**Example UX:**
```
First Thai Menu Scan:
┏━━━━━━━━━━━━━━━━━━━━━━┓
┃ 🇹🇭 Thai Cuisine Tip   ┃
┣━━━━━━━━━━━━━━━━━━━━━━┫
┃ ⚠️ HIGH DIFFICULTY     ┃
┃                        ┃
┃ Fish sauce (น้ำปลา) is ┃
┃ in ~80% of Thai dishes ┃
┃                        ┃
┃ VegyScan will help you ┃
┃ identify it, but always┃
┃ confirm with staff.    ┃
┃                        ┃
┃ Look for "เจ" symbol   ┃
┃ (Buddhist vegan) ✅    ┃
┗━━━━━━━━━━━━━━━━━━━━━━┛
```

---

### 2. Hidden Ingredients by Cuisine (Detailed)

**Research Insight:**
Your research provides extensive tables of hidden ingredients:
- Thai: น้ำปลา (nam pla), กะปิ (kapi shrimp paste), oyster sauce
- Japanese: だし (dashi), 鰹節 (katsuobushi), うなぎエキス (unagi extract)
- Chinese: 蚝油 (oyster sauce), 鸡精 (chicken bouillon), 猪油 (lard)
- Italian: Acciughe (anchovies), Parmesan (animal rennet), strutto (lard)
- And detailed lists for Vietnamese, Korean, French, Indian, Mexican, Middle Eastern...

**How This Maps to Product:**

✅ **ALREADY CAPTURED:**
- REQ-F-042: Cultural Context Database has this EXACT structure
- Each cuisine should have:
  ```yaml
  Hidden Ingredients:
    - Fish sauce (น้ำปลา / nam pla) - in 80% of dishes
    - Shrimp paste (กะปิ / kapi) - in curry pastes, stir-fries
    - Oyster sauce - in vegetable dishes
  ```

**What You Need to Do:**
- **Populate REQ-F-042 database with your research data** ← This is ready to go!
- Your research IS the database source
- For each cuisine, copy your "Key Hidden Ingredients" and "Common Oversights" into the Cultural Context DB

**No new feature needed - just data population.** ✅

---

### 3. Modification Feasibility (⭐ NEW INSIGHT)

**Research Insight:**
> "Sometimes it's easy to change a dish - just leave something out. Other times it's impossible because soup has been cooked with bones the whole day. If you make a sauce, maybe it's possible if they haven't pre-produced it."

**This is a MAJOR new insight not previously captured.**

**How This Maps to Product:**

⭐ **NEW FEATURE:**
- **REQ-F-054: Modification Feasibility Classification**
  - Easy (🟢): Toppings, garnishes, sauce on side
  - Moderate (🟡): Substitutions if kitchen has alternatives
  - Impossible (🔴): Cooked into dish, pre-made components

**Example UX:**
```
🍜 Tonkotsu Ramen

❌ CANNOT BE VEGANIZED

🔴 IMPOSSIBLE to modify
└─ Pork bone broth cooked 12+ hours
   Flavor is infused throughout
   Cannot be removed

💡 Recommendation:
   Choose a different dish or ask for
   "Vegetable Ramen" instead
```

```
🍝 Spaghetti Pomodoro w/ Parmesan

🟡 VEGETARIAN → Can be Vegan

🟢 EASY to modify
└─ Parmesan is a topping
   Just ask them to leave it off

💬 Ask: "Senza formaggio, per favore"
Success Rate: ~95% ✅
```

**Why This Matters:**
- Sets realistic expectations (don't waste time asking for impossible modifications)
- Builds trust (we're honest about what's possible)
- Guides users to better choices (pick easily-modifiable dishes)

---

### 4. Country-Specific Modification Culture (⭐ NEW INSIGHT)

**Research Insight:**
> - Japan: "Modifications rarely accepted in traditional restaurants"
> - Thailand: "Street vendors often flexible, can adjust"
> - France: "Sauces often pre-made, can't modify"
> - Mexico: "Lard already in beans, can't remove after cooking"

**This cultural context around modification ACCEPTANCE is new.**

**How This Maps to Product:**

⭐ **NEW FEATURE:**
- **REQ-F-055: Country-Specific Modification Culture Database**
  - Japan Traditional: 15-25% acceptance rate
  - Thailand Street Food: 70-85% acceptance rate
  - France Traditional: 30-45% acceptance rate

**Example UX:**
```
🍛 Pad Thai (Thailand)

⚠️ MODERATE - Can Usually Modify

💡 Cultural Context:
   Thai street vendors cook to order
   and often understand "gin jay" (เจ).

   Success Rate: ~70-85% ✅

[Show Modification Questions]
```

```
🍣 Miso Soup (Japan)

❌ Contains Dashi (Fish Stock)

⚠️ Cultural Note:
   Traditional Japanese restaurants
   rarely modify dishes. Requesting
   changes may be seen as disrespectful
   to the chef.

   Success Rate: ~15% (Very Low)

💡 Better Option:
   Look for "Vegetable Soup" or
   visit a vegan-friendly restaurant.
```

**Why This Matters:**
- Prevents awkward/unsuccessful interactions
- Respects local culture (don't push for modifications where not accepted)
- Guides users to more effective strategies

---

### 5. OCR/Language Difficulty

**Research Insight:**
Your research has detailed OCR difficulty table:
- Latin scripts: 95%+ accuracy (Easy)
- Thai: 80-90% (Medium) - no word spaces, segmentation hard
- Chinese: 85-95% (Medium) - thousands of characters
- Japanese: 80-90% (Hard) - 3 scripts, vertical text, complex
- Arabic: 80-85% (Medium) - RTL, cursive

**How This Maps to Product:**

❌ **MISSING FROM FUNCTIONAL REQUIREMENTS**
✅ **Should be in Architecture/Technical Specs**

**Where This Belongs:**
- **Architecture:** Tech stack decisions (which OCR library for which language?)
- **Business Case:** Phase 1/2/3 language rollout prioritization
- **Non-Functional Requirements:** Performance/accuracy targets per language

**Current Status:**
- Your research already informed the business case phased rollout:
  - Phase 1: Latin scripts (easy, fast to market)
  - Phase 2: Japanese, Chinese, Thai (high value despite difficulty)
  - Phase 3: Arabic, Hebrew, Korean

**Action Needed:**
- Add this table to Architecture specs (when you start technical architecture)
- Create ADR: "Language Rollout Priority" referencing this research
- No functional requirement needed (it's a technical constraint, not a user-facing feature)

---

### 6. Market Prioritization (US/UK Primary, Germany Secondary)

**Research Insight:**
Detailed market analysis scoring each region on:
- User base size
- iOS adoption
- Willingness to pay
- Problem intensity
- Competitor landscape

Results:
- 🟢 **Primary:** US, UK (large vegan travelers, high iOS, high WTP)
- 🟡 **Secondary:** Germany (large vegan pop, lower iOS ~20-30%)
- 🟢 **Tertiary:** Canada, Australia, Northern Europe

**How This Maps to Product:**

✅ **ALREADY CAPTURED:**
- **Business Case (hypotheses.md):**
  - Hypothesis #4: "Target Market - US/UK first, Germany secondary" ⚠️ Partial evidence
  - Market research validates this
- **Business Case (market-analysis.md):**
  - Should include your detailed market scoring

**Where This Belongs:**
- Business case (strategy layer) ✅ Already there
- Go-to-market plan (when you create it)
- Localization roadmap (which languages to prioritize)

**NOT a functional requirement** - it's a business strategy decision that informs WHICH features to build WHEN, but not WHAT features exist.

**Action Needed:**
- Ensure market-analysis.md has your detailed country scoring
- Use this to prioritize localization (English → German → French/Spanish)
- Use this to prioritize cultural databases (Thai/Japanese high priority for US/UK travelers)

---

### 7. Cultural Dietary Concept Variations

**Research Insight:**
> - Japan: "Vegetarian" may include fish (fish not seen as "meat")
> - India: "Vegetarian" includes dairy (lacto-vegetarian standard)
> - France/Spain: Concept of veganism less understood
> - Middle East: "Fasting food" may be better term than "vegan"

**How This Maps to Product:**

✅ **ALREADY CAPTURED:**
- **REQ-F-042: Cultural Context Database** - has "Cultural Notes" section
- **REQ-F-043: Smart Vegan Passport** - adapts terminology by culture
  - India: "Strict vegetarian (शुद्ध शाकाहारी)"
  - Japan: Full explanation (not just "vegan")
  - Thailand: "เจ" (Jay - Buddhist vegan)

**What You Need to Do:**
- Populate REQ-F-042 cultural notes with your research
- For each country, add:
  - How "vegetarian" is understood locally
  - Whether "vegan" is a familiar concept
  - Alternative terms that work better (e.g., "fasting food," "strict vegetarian")

**No new feature needed - data population.** ✅

---

### 8. Local Safe Dishes & Watch-Out Dishes

**Research Insight:**
Your research includes:
- **Safe dishes** by cuisine (e.g., Edamame in Japan, Hummus in Middle East)
- **Watch-out dishes** (Belgian fries in animal fat, Chinese "vegetarian" with broth)

**How This Maps to Product:**

✅ **ALREADY CAPTURED:**
- REQ-F-042: Cultural Context Database includes:
  ```yaml
  Safe Local Dishes:
    - Edamame (枝豆) - 95% vegan
    - Natto (納豆) - fermented soybeans

  Watch-Out Dishes:
    - Miso soup - usually contains dashi (fish stock)
    - Tempura - may be fried in animal fat
  ```

- REQ-F-048: Local Dish Highlighting
  - Badges local dishes: "🌍 LOCAL SPECIALTY"
  - Shows vegan status or how to veganize

**What You Need to Do:**
- Populate database with your lists for each cuisine
- Your research is the perfect source

**No new feature needed - data population.** ✅

---

## Vision Implications

Your research should also update the **Product Vision** to emphasize:

### 1. Realistic Modification Guidance (Not False Hope)

**Current Vision Statement:**
> "Transform any foreign-language menu into an interactive verification tool"

**Should Emphasize:**
> "Help users identify WHICH dishes can realistically be modified, and HOW to ask for those modifications effectively in each culture."

**Add to Vision Goals:**
- **Goal #6:** Set realistic expectations about modification feasibility
  - Not all modifications are possible (soup with bones cooked 12 hours = impossible)
  - Cultural norms vary (Japan rarely accepts changes, Thailand often does)
  - Empower users to make informed choices, not false hope

### 2. Culture-Aware, Not Just Language-Aware

**Current Vision Scope:**
- Translation ✅
- Hidden ingredient detection ✅
- Cuisine context ✅

**Should Add:**
- Modification culture awareness ⭐ NEW
- Success rate estimates ⭐ NEW
- Cultural dining etiquette ⭐ NEW

### 3. Problem Intensity Differentiation

**Vision Should Highlight:**
> "We prioritize the HARDEST cuisines (Thai, Japanese) where generic translators fail most often, providing deep cultural intelligence that goes beyond literal translation."

This positions you as solving the MOST PAINFUL problems (not just any translation problem).

---

## Feature Priority for v1 vs. v1.5

Based on your research, here's my recommendation:

### Must Have for v1 (Killer Features)

**From Your Research:**
1. ✅ REQ-F-042: Cultural Context Database (Thai, Japanese, Chinese hidden ingredients)
   - This is your CORE differentiator
   - Your research IS this database
2. ⭐ REQ-F-054: Modification Feasibility Classification (Easy/Moderate/Impossible)
   - Unique insight, massive value
   - Prevents wasted time and frustration
3. ✅ REQ-F-044: Modification Question Generator
   - Already captured, needs your cultural phrases
4. ✅ REQ-F-012: Cuisine Context Awareness
   - Apply hidden ingredient knowledge

### Should Have for v1.5 (High Value, But Can Wait)

**From Your Research:**
5. ⭐ REQ-F-055: Country Modification Culture Database
   - Adds success rate estimates
   - Cultural etiquette guidance
   - Can be added incrementally (start with top 5 countries)
6. ⭐ REQ-F-056: Cuisine Problem Intensity Ranking
   - Educational first-scan tips
   - Nice-to-have, but not blocker
7. ⭐ REQ-F-057: Menu-Level Difficulty Assessment
   - "This menu is CHALLENGING" summary
   - Good UX, but not critical for core flow

### Nice to Have for v2

8. REQ-F-048: Local Dish Highlighting
   - Helps users find cultural experiences
   - Lower priority than safety/veganization

---

## Data Population Checklist

Your research provides ready-to-use data for:

### Immediate (Can Populate Now)

- [ ] **REQ-F-042: Cultural Context Database**
  - [ ] Thai Cuisine: Copy hidden ingredients, phrases, safe dishes from research
  - [ ] Japanese Cuisine: Copy dashi variants, cultural notes from research
  - [ ] Chinese Cuisine: Copy oyster sauce warnings, regional variations
  - [ ] Vietnamese, Korean, Italian, French, Indian, Mexican, Middle Eastern
  - [ ] For EACH cuisine, add your:
    - Key Hidden Ingredients (with local names)
    - Common Oversights (what travelers miss)
    - Safe Local Dishes
    - Watch-Out Dishes
    - Cultural eating customs
    - Local terminology

- [ ] **REQ-F-054: Modification Feasibility Patterns**
  - [ ] Populate per cuisine:
    - Easy modifications (what can be left out)
    - Moderate modifications (what can be substituted)
    - Impossible modifications (what's cooked in)
  - Your research gives examples:
    - Thai curry paste → Impossible (pre-made with shrimp paste)
    - Pad Thai egg → Easy (cooked separately, can omit)
    - Mexican beans → Impossible (lard already cooked in)

### After Feature Design (v1.5)

- [ ] **REQ-F-055: Country Modification Culture**
  - [ ] Create entries for:
    - Japan (traditional vs. modern acceptance rates)
    - Thailand (street food vs. fine dining)
    - France (sauce culture, pre-made challenges)
    - Mexico (lard in beans, chicken stock in rice)
    - USA/UK (high acceptance, "allergy" framing works)

- [ ] **REQ-F-056: Problem Intensity Rankings**
  - [ ] Assign intensity levels:
    - Very High: Thai, Japanese
    - High: Chinese, Vietnamese, Korean, Italian, French
    - Lower: Indian, Middle Eastern, Mexican
  - [ ] Add percentages from your research ("~80% Thai dishes contain fish sauce")

---

## Summary: How Your Research Maps to Product

### ✅ Already Captured (70%)

Your research validates and enriches EXISTING requirements:
- Cultural database structure (REQ-F-042) ← YOUR RESEARCH IS THE CONTENT
- Modification questions (REQ-F-044) ← YOUR RESEARCH HAS THE PHRASES
- Cuisine context (REQ-F-012) ← YOUR RESEARCH HAS THE RULES
- Market prioritization (Business Case) ← YOUR RESEARCH HAS THE SCORING
- Language phasing (Business Case) ← YOUR RESEARCH HAS THE OCR DIFFICULTY

**Action:** Populate databases with your data (copy-paste from research)

### ⭐ New Features Needed (30%)

Your research uncovered NEW insights requiring NEW features:
- **REQ-F-054:** Modification Feasibility (Easy/Moderate/Impossible) ⭐ CRITICAL
- **REQ-F-055:** Country Modification Culture (acceptance rates) ⭐ HIGH VALUE
- **REQ-F-056:** Cuisine Problem Intensity Ranking ⭐ NICE TO HAVE
- **REQ-F-057:** Menu Difficulty Assessment ⭐ NICE TO HAVE

**Action:** Review new requirements doc, prioritize for v1 vs. v1.5

### 📋 Vision Updates Needed

- Emphasize realistic modification guidance (not false hope)
- Highlight culture-aware (not just language-aware)
- Position as solving HARDEST cuisines (Thai/Japanese differentiator)

---

## Next Steps

1. **Review NEW Requirements:**
   - Read `NEW-modification-feasibility-requirements.md`
   - Decide which are v1 vs. v1.5
   - Provide feedback on Easy/Moderate/Impossible classification

2. **Populate Cultural Database:**
   - Use your research to fill REQ-F-042 database
   - Start with Thai, Japanese, Chinese (highest priority)
   - I can help convert your research into YAML database format

3. **Update Vision Document:**
   - Add modification feasibility as core value prop
   - Emphasize cultural intelligence differentiator

4. **Prioritize Language Rollout:**
   - Confirm Phase 1: Latin scripts (Spanish, French, Italian, German)
   - Confirm Phase 2: Thai, Japanese, Chinese (high value despite difficulty)
   - Document this in Architecture specs (when you create them)

---

**Great work on this research!** It's incredibly thorough and provides exactly the kind of real-world intelligence that will differentiate VegyScan from generic translators. The modification feasibility insight is particularly valuable - no one else is doing this.

Let me know:
1. Do the new requirements (REQ-F-054 through REQ-F-057) capture your vision?
2. Which should be v1 vs. v1.5?
3. Should I help you populate the cultural database with your research data?
