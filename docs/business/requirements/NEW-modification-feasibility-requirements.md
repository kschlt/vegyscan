# NEW Requirements: Modification Feasibility & Enhanced Cultural Intelligence

**Status:** DRAFT - Awaiting User Review
**Created:** 2025-11-18
**Based on:** Deep Research on Global Vegan Menu Scanning Challenges (31-page analysis)

---

## Overview

This document captures NEW requirements discovered through deep research on cuisine-specific challenges and modification patterns. These insights go beyond the existing REQ-F-042 (Cultural Context Database) and REQ-F-044 (Modification Questions).

**Key New Insights:**
1. Not all modifications are equally feasible - we need to classify difficulty
2. Country/cuisine-specific modification culture varies dramatically
3. We need to set user expectations based on what's actually possible

---

## REQ-F-054: Modification Feasibility Classification

**Description:** System must classify each potential dish modification by feasibility level (Easy/Moderate/Impossible/Unknown) based on cooking method, ingredient integration, and cultural modification norms.

**Rationale:** **CRITICAL NEW INSIGHT** from research: Suggesting impossible modifications frustrates users and wastes time. A soup cooked with bones for hours cannot be veganized. But cheese on top of pasta can easily be left off. We must communicate this distinction clearly.

**Priority:** Must Have (CRITICAL - directly impacts user experience and trust)

**Status:** NEW - Not Yet Implemented

**Research Foundation:**
> "Sometimes it might be easy to change a dish because you can only leave something out. In other ways it's impossible because some soup has been cooked the whole day with bones - there's no way to take the bones out. But if you make a sauce, maybe it's possible to don't do the sauce with cream, but do it with something else if they don't have pre-produced the sauce."

### Feasibility Levels

**🟢 EASY (High Success Probability)**
- **Definition:** Ingredient can be removed without affecting core dish
- **Examples:**
  - Cheese topping on pasta → "No cheese please"
  - Egg on fried rice → "Without egg"
  - Sauce served on the side → "Sauce on side" or "No sauce"
  - Garnishes (bonito flakes, dried shrimp on top)
- **User Message:** "✅ Easy to modify - just ask to leave it out"
- **Success Rate:** 85-95% (restaurants usually accommodate)

**🟡 MODERATE (Depends on Kitchen)**
- **Definition:** Requires ingredient substitution or kitchen has to prepare differently
- **Examples:**
  - Cream in pasta sauce → "Use plant milk instead" (if available)
  - Butter for cooking → "Use oil instead" (if they're willing)
  - Fish sauce in stir-fry → "Use soy sauce instead"
  - Meat broth in rice → "Cook in water" (if they cook to order)
- **User Message:** "⚠️ Moderate - depends on what the kitchen has available"
- **Success Rate:** 40-70% (varies by restaurant type and country)

**🔴 IMPOSSIBLE (Cannot Be Modified)**
- **Definition:** Ingredient is integral to the dish and cannot be removed or substituted
- **Examples:**
  - Soup/stew cooked with bones for hours → Broth is infused
  - Curry paste made with shrimp paste → Pre-made, can't remake
  - Lard used for frying → Food already cooked
  - Gelatin in dessert → Structural component
  - Cheese/egg in fresh pasta dough → Already mixed in
- **User Message:** "❌ Cannot be veganized - core ingredient cooked in"
- **Success Rate:** 0-10% (only if kitchen is willing to remake from scratch, rare)

**❓ UNKNOWN (Insufficient Information)**
- **Definition:** Not enough information to determine feasibility
- **User Message:** "❓ Ask the waiter - it depends on how they prepare it"
- **Success Rate:** Variable

### Classification Logic

The system must use these factors to determine feasibility:

**1. Cooking Method Context**
```
IF ingredient = "broth" AND dish_type = "soup/stew"
  → IMPOSSIBLE (broth is infused, can't be removed)

IF ingredient = "cheese" AND location = "topping"
  → EASY (can be left off)

IF ingredient = "cream" AND dish_type = "sauce"
  → MODERATE (depends if kitchen has plant alternative)

IF ingredient = "egg" AND dish_type = "pasta dough"
  → IMPOSSIBLE (baked/cooked into structure)
```

**2. Cuisine/Country Modification Norms**
```
IF cuisine = "Japanese" AND restaurant_type = "traditional"
  → Lower all feasibility by 1 level (modifications rarely accepted)

IF cuisine = "Thai" AND restaurant_type = "street food"
  → Higher success rates (vendors often flexible)

IF ingredient = "fish sauce" AND cuisine = "Vietnamese"
  → MODERATE-to-IMPOSSIBLE (so ubiquitous, kitchens may not have alternatives)
```

**3. Ingredient Integration Level**
```
Topping/Garnish → EASY
Sauce (separate) → EASY to MODERATE
Sauce (integrated) → MODERATE to IMPOSSIBLE
Core ingredient → IMPOSSIBLE
Cooking fat/method → IMPOSSIBLE (after cooking)
Pre-made component → IMPOSSIBLE (curry paste, broth)
```

### Acceptance Criteria

- [ ] Each dish analysis includes modification feasibility classification
- [ ] Feasibility displayed with color-coded icons: 🟢 🟡 🔴 ❓
- [ ] Clear explanation of WHY each feasibility level is assigned
- [ ] Examples of what to ask for each level:
  - EASY: "Just ask them to leave it out"
  - MODERATE: "Ask if they can substitute [X] with [Y]"
  - IMPOSSIBLE: "This dish cannot be veganized - choose a different dish"
- [ ] Caveat for cultural norms (e.g., "Note: In traditional Japanese restaurants, modifications are rarely accepted")
- [ ] User can tap to see detailed reasoning
- [ ] Success probability shown as percentage (e.g., "⚠️ ~50% success rate")

### UX Examples

**Example 1: Easy Modification**
```
🍝 Spaghetti Aglio e Olio

Classification: 🟢 VEGETARIAN (can be vegan)

✅ EASY TO VEGANIZE
└─ Remove: Parmesan cheese (topping)

💬 Ask: "Can I have this without the cheese?"
🇮🇹 Posso averlo senza formaggio?

Success Rate: ~95% ✅
```

**Example 2: Moderate Modification**
```
🍛 Pad Thai

Classification: 🔴 NOT VEGAN

⚠️ MODERATE - Depends on Kitchen
└─ Remove: Egg, Fish sauce
└─ Substitute: Soy sauce instead

💬 Ask: "Can you make this without egg and
         fish sauce, using soy sauce?"
🇹🇭 [Thai translation]

Success Rate: ~60% ⚠️
Note: Street vendors usually accommodate this
```

**Example 3: Impossible Modification**
```
🍜 Tonkotsu Ramen

Classification: 🔴 NOT VEGAN

❌ CANNOT BE VEGANIZED
└─ Reason: Pork bone broth cooked for 12+ hours
           Broth is infused throughout, cannot be removed

Recommendation: Choose a different dish
Alternative: Look for "Vegetable Ramen" or
            "Shoyu Ramen with vegetable broth"

Success Rate: ~5% ❌
```

**Example 4: Unknown (Need to Ask)**
```
🥘 Mushroom Risotto

Classification: 🟡 VEGETARIAN (unknown if vegan)

❓ ASK THE WAITER - Depends on Preparation
└─ Possible non-vegan ingredients:
   • Butter (for cooking)
   • Cream (in risotto)
   • Parmesan (stirred in or topping?)
   • Chicken/beef broth (instead of vegetable)

💬 Questions to ask:
1. "Is this made with butter or oil?"
2. "Does it have cream?"
3. "What broth is used - vegetable or chicken?"
4. "Can you make it without dairy?"

Feasibility: MODERATE if ingredients separate
            IMPOSSIBLE if pre-made
```

---

## REQ-F-055: Country-Specific Modification Culture Database

**Description:** System must maintain database of modification acceptance norms by country, cuisine type, and restaurant type, and use this to set user expectations.

**Rationale:** Research shows modification success rate varies dramatically by culture. In Japan, traditional restaurants rarely accommodate changes. In Thailand, street vendors are often flexible. Users need this context to avoid frustration and awkward interactions.

**Priority:** Must Have

**Status:** NEW - Not Yet Implemented

**Research Foundation:**
> "In Japan, modifications rarely accepted in traditional restaurants."
> "Thai street vendors often flexible with ingredients."
> "French cuisine: sauces often pre-made, can't modify."

### Database Structure

```yaml
Country: Japan
  Cuisine Types:
    - Traditional Japanese:
        Modification Acceptance: VERY LOW (15-25%)
        Cultural Notes: |
          Modifying dishes is considered disrespectful to the chef's
          intent. Traditional restaurants (izakaya, sushi, kaiseki)
          almost never accommodate modifications.
        Exceptions:
          - Temple restaurants (shojin ryori) - made for dietary restrictions
          - Modern vegan restaurants
        User Guidance: |
          "In traditional Japanese restaurants, modifications are rarely
          accepted. Look for dishes that are naturally vegan or visit
          specialized vegan restaurants."

    - Western-style/Casual:
        Modification Acceptance: MODERATE (50-60%)
        Cultural Notes: Western chains and casual restaurants more flexible

Country: Thailand
  Cuisine Types:
    - Street Food:
        Modification Acceptance: HIGH (70-85%)
        Cultural Notes: |
          Street vendors and casual restaurants often cook to order.
          "No fish sauce, no egg" is commonly understood.
        Exceptions:
          - Pre-made curry pastes (usually contain shrimp paste)
          - Sauces made in advance
        User Guidance: |
          "Thai street food is usually customizable. Most vendors
          understand 'gin jay' (vegan) and can adjust."

    - Fine Dining:
        Modification Acceptance: MODERATE (60-70%)
        Cultural Notes: More willing to accommodate than Japanese fine dining

Country: France
  Cuisine Types:
    - Traditional French:
        Modification Acceptance: LOW (30-45%)
        Cultural Notes: |
          French cuisine relies heavily on sauces and cooking techniques.
          Many sauces are pre-made. Modifications seen as interfering
          with chef's vision.
        Common Issues:
          - Butter used in most vegetable dishes
          - Meat stocks in "vegetable" soups
          - Sauces made in advance
        User Guidance: |
          "Traditional French restaurants rarely modify dishes.
          Ask if sauces/sides can be served separately."

Country: Mexico
  Cuisine Types:
    - Traditional/Street:
        Modification Acceptance: MODERATE-HIGH (60-75%)
        Cultural Notes: |
          Many dishes can be customized, but lard and chicken broth
          are often already in the beans/rice by the time you order.
        Common Issues:
          - Lard (manteca) in refried beans, tamales (cooked in)
          - Chicken stock in rice (cooked in)
        User Guidance: |
          "Ask 'sin manteca, sin caldo de pollo' (no lard, no chicken broth).
          Success depends on if it's already prepared."
```

### Acceptance Criteria

- [ ] Database covers top 20 vegan travel destinations
- [ ] Each country entry includes:
  - [ ] Overall modification acceptance (percentage/rating)
  - [ ] Breakdown by cuisine type (traditional vs. modern vs. street food)
  - [ ] Cultural context (why modifications accepted/rejected)
  - [ ] Common pre-made ingredients (can't be modified)
  - [ ] User guidance specific to that culture
- [ ] System applies this context when showing modification feasibility
- [ ] Adjust success rate estimates based on country
- [ ] Provide cultural tips in modification suggestions

Example UX:
```
🍛 Pad Thai (Thailand)

⚠️ MODERATE - Can Usually Be Modified

💡 In Thailand: Street vendors often cook to order
   and can leave out fish sauce and egg.

Success Rate: ~70% at street food stalls
             ~85% at casual restaurants
             ~60% at hotel restaurants

[Show Modification Questions]
```

---

## REQ-F-056: Cuisine Problem Intensity Ranking

**Description:** System must rank cuisines by "vegan problem intensity" (how frequently hidden animal ingredients appear) and use this to prioritize warnings, questions, and cultural tips.

**Rationale:** Research shows certain cuisines are far more problematic than others. Thai cuisine has fish sauce "in almost everything." Japanese cuisine has dashi in nearly all soups. Users need to know which cuisines require extra vigilance.

**Priority:** Should Have

**Status:** NEW - Not Yet Implemented

**Research Foundation:**
> Cuisine rankings by problem intensity:
> - 🔴 Very High: Thai, Japanese (hidden fish ingredients ubiquitous)
> - 🟡 High: Chinese, Vietnamese, Korean
> - 🟢 Lower: Indian, Middle Eastern, Mexican

### Problem Intensity Levels

**🔴 VERY HIGH - Extreme Vigilance Required**
- Thai Cuisine: Fish sauce, shrimp paste, oyster sauce in ~80%+ of dishes
- Japanese Cuisine: Dashi (fish stock) in ~70%+ of soups, sauces, rice dishes

**🟡 HIGH - Frequent Hidden Ingredients**
- Chinese: Oyster sauce in vegetables, meat broths, lard (50-70% of dishes)
- Vietnamese: Fish sauce (nước mắm) in sauces and soups (~60%)
- Korean: Anchovy broth, fish sauce in kimchi (~50-60%)
- Italian: Cheese with rennet, anchovies in sauces (~40-50%)
- French: Butter, stocks in vegetables (~40-50%)

**🟢 LOWER - Manageable with Care**
- Indian: Ghee, dairy common but disclosed (~30-40%)
- Middle Eastern: Ghee, broths occasional (~25-35%)
- Mexican: Lard, chicken broth but regional (~30-40%)

### How System Uses This

**1. Warning Priority**
```
IF cuisine_type = "Thai" OR "Japanese"
  → Show PROMINENT warning:
    "⚠️ Thai cuisine frequently uses fish sauce (nam pla)
     in almost all dishes. Always ask to confirm."

IF cuisine_type = "Indian"
  → Show MODERATE warning:
    "💡 Indian dishes often contain ghee (clarified butter).
     Ask if dishes can be made without it."
```

**2. Auto-Suggest Verification Questions**
```
IF cuisine_type = "Thai"
  → Auto-include verification even for "appears vegan" dishes:
    "This APPEARS vegan, but to be safe, ask:
     'ไม่ใส่น้ำปลาใช่ไหม?' (No fish sauce, correct?)"
```

**3. Confidence Level Adjustment**
```
IF cuisine = "Thai" AND dish_appears_vegan AND no_explicit_veg_symbol
  → Lower confidence from ⚫⚫⚫ to ⚫⚫◯
  → Add reasoning: "Thai dishes often contain fish sauce even
     if not listed. Verify before ordering."
```

**4. Educational Onboarding**
When user scans first menu of a cuisine type:
```
First Thai Menu Scan:
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ 🇹🇭 Thai Cuisine Tip       ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                            ┃
┃ Thai food is DELICIOUS but ┃
┃ challenging for vegans:    ┃
┃                            ┃
┃ ⚠️ Fish sauce (น้ำปลา) is  ┃
┃    used in ~80% of dishes  ┃
┃                            ┃
┃ Look for "เจ" (jay) symbol ┃
┃ = Buddhist vegan           ┃
┃                            ┃
┃ VegyScan will flag hidden  ┃
┃ ingredients, but ALWAYS    ┃
┃ double-check with staff.   ┃
┃                            ┃
┃ [Got it!]   [Learn More]   ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

### Acceptance Criteria

- [ ] Database ranks all major cuisines by problem intensity
- [ ] Each cuisine entry includes:
  - [ ] Problem intensity rating (Very High / High / Lower)
  - [ ] Most common hidden ingredients (ranked by frequency)
  - [ ] Percentage of dishes affected (e.g., "~80% contain fish sauce")
  - [ ] User guidance specific to that cuisine
- [ ] System adjusts warnings based on problem intensity
- [ ] First-scan educational tips for Very High cuisines
- [ ] Confidence levels adjusted for problematic cuisines
- [ ] Research citations for each rating (from user's research doc)

---

## REQ-F-057: Context-Aware Veganization Difficulty Indicator

**Description:** System must display overall "veganization difficulty" for each scanned menu based on cuisine type, dish types, and modification culture.

**Rationale:** Users need to know "how hard will this menu be?" BEFORE diving into individual dishes. A Thai street food menu vs. a French fine dining menu vs. an Indian vegetarian restaurant menu all have very different difficulty levels.

**Priority:** Should Have

**Status:** NEW - Not Yet Implemented

### Menu-Level Difficulty Assessment

After scanning a menu, show overall assessment:

**EASY Menu Example (Indian Vegetarian Restaurant)**
```
┏━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ 📋 MENU ANALYSIS          ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                           ┃
┃ 🟢 VEGAN-FRIENDLY MENU    ┃
┃                           ┃
┃ ✅ 12 vegan dishes found  ┃
┃ ⚠️  8 vegetarian (dairy)  ┃
┃                           ┃
┃ 💡 This is an Indian      ┃
┃    vegetarian restaurant  ┃
┃    Many dishes are        ┃
┃    naturally vegan or     ┃
┃    can easily be made     ┃
┃    without ghee/dairy.    ┃
┃                           ┃
┃ [View Vegan Options]      ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

**CHALLENGING Menu Example (Traditional Japanese)**
```
┏━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ 📋 MENU ANALYSIS          ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                           ┃
┃ 🔴 CHALLENGING MENU       ┃
┃                           ┃
┃ ⚠️ Japanese cuisine -     ┃
┃    most dishes contain    ┃
┃    dashi (fish stock)     ┃
┃                           ┃
┃ ❌ 0 clearly vegan dishes ┃
┃ ❓ 3 possibly vegan with  ┃
┃    modifications          ┃
┃    (ask about dashi)      ┃
┃                           ┃
┃ 💡 Traditional restaurants┃
┃    rarely modify dishes.  ┃
┃    Consider finding a     ┃
┃    vegan restaurant.      ┃
┃                           ┃
┃ [View Options Anyway]     ┃
┃ [Find Vegan Restaurant]   ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

### Difficulty Factors

```python
difficulty = calculate_difficulty(
    cuisine_problem_intensity,      # Thai/Japanese = HIGH
    modification_culture,             # Japan traditional = LOW acceptance
    vegan_dish_count,                # 0 = HIGH difficulty
    modifiable_dish_count,           # Low = HIGH difficulty
    confidence_levels                # Many LOW confidence = HIGH difficulty
)
```

**Result:**
- 🟢 VEGAN-FRIENDLY (many options, easy modifications)
- 🟡 MODERATE (some options, moderate modifications)
- 🔴 CHALLENGING (few/no options, difficult modifications)

### Acceptance Criteria

- [ ] Menu-level difficulty shown after initial scan
- [ ] Color-coded (green/yellow/red)
- [ ] Explains WHY difficult (cuisine type, modification culture, dish availability)
- [ ] Suggests action (view options / find different restaurant)
- [ ] Can be dismissed (user proceeds to dish-by-dish view)
- [ ] Reappears as banner at top while browsing dishes

---

## Enhanced REQ-F-042: Cultural Context Database - Additional Data Needed

The existing REQ-F-042 is good, but based on the new research, it needs these additions:

### Add to Each Cuisine Entry:

**1. Problem Intensity Rating**
```yaml
Cuisine: Thai
  Problem Intensity: VERY HIGH
  Problem Frequency: 80-90% of dishes contain fish sauce or shrimp paste
  Research Citation: "[Reddit user testimonials, travel blogs]"
```

**2. Modification Culture**
```yaml
  Modification Acceptance:
    Street Food: 70-85% (HIGH)
    Casual Restaurants: 60-75% (MODERATE-HIGH)
    Fine Dining: 50-60% (MODERATE)
  Cultural Notes: |
    Street vendors cook to order and often understand "gin jay" (เจ).
    Pre-made curry pastes usually contain shrimp paste (cannot modify).
```

**3. Modification Feasibility Patterns**
```yaml
  Common Modification Patterns:
    EASY:
      - "No egg on fried rice"
      - "No dried shrimp on papaya salad"
    MODERATE:
      - "No fish sauce" (if cooking to order)
      - "Use soy sauce instead"
    IMPOSSIBLE:
      - Pre-made curry paste (contains shrimp paste)
      - Pad Thai sauce (often pre-made with fish sauce)
```

**4. Language/Script OCR Difficulty**
```yaml
  Language: Thai
  Script: Thai script
  OCR Difficulty: MEDIUM
  OCR Accuracy: 80-90%
  Challenges:
    - No spaces between words (requires segmentation)
    - Tone marks must be recognized
    - Stylized fonts can be problematic
  Phase: Phase 2 (6-12 months after launch)
```

This should be added to the existing REQ-F-042 database structure.

---

## Summary of Changes

**New Requirements:**
1. **REQ-F-054:** Modification Feasibility Classification (Easy/Moderate/Impossible)
2. **REQ-F-055:** Country-Specific Modification Culture Database
3. **REQ-F-056:** Cuisine Problem Intensity Ranking
4. **REQ-F-057:** Context-Aware Veganization Difficulty Indicator

**Enhanced Requirements:**
- **REQ-F-042:** Add problem intensity, modification culture, OCR difficulty to cultural database

**Impact:**
- Users will have realistic expectations about what can/cannot be modified
- Reduces frustration from attempting impossible modifications
- Builds trust through honest, culturally-aware guidance
- Prioritizes high-value warnings for problematic cuisines

---

## Next Steps

1. **User Review:** Does this capture your research insights?
2. **Prioritization:** Which of these are Must Have vs. Should Have for v1?
3. **Integration:** Merge these into main functional requirements doc
4. **Data Collection:** Begin building the enhanced cultural database with your research data
5. **UX Design:** Create mockups for modification feasibility UI

---

**Questions for User:**
1. Does the Easy/Moderate/Impossible classification match your mental model?
2. Any additional modification patterns I missed?
3. Should we add "Country-Specific Modification Phrases" (how to politely ask in each culture)?
4. Priority: Which of REQ-F-054 through REQ-F-057 are critical for v1 vs. v1.5?
