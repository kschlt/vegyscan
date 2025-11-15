# User Personas

> **Last Updated:** 2025-11-15

_This file is the Single Source of Truth for all user groups and their dietary preferences._

**Focus:** Personas are organized by **dietary type and strictness level** to test different classification requirements and features.

---

## Persona 1: Strict Vegan - Anna {#strict-vegan-anna}

### Dietary Profile
- **Type:** Vegan (ethical reasons)
- **Strictness:** Extremely strict
- **Rules:**
  - ❌ No animal products whatsoever
  - ❌ No honey
  - ❌ No animal-derived broths/stocks (Dashi, bone broth)
  - ❌ No gelatin, lard, animal fats
  - ❌ Even traces in sauces are unacceptable
  - ❌ Cross-contamination is a concern (fried in same oil as meat)

### Usage Requirements
- **Needs:** High confidence classification (⚫⚫⚫ only)
- **Expects:** Clear warning about hidden animal products
- **Values:** Detailed reasoning ("contains fish sauce in dressing")
- **Behavior:** Will NOT order if confidence is ⚫⚫◯ or ⚫◯◯
- **Feature needs:**
  - Symbol recognition (trusts 🌱 vegan symbol)
  - Cuisine context awareness (knows Belgian fries may use animal fat)
  - Detailed ingredient list

### Test Cases for Anna
- Tonkotsu ramen → Must classify as ❌ (pork bone broth)
- Vegetable tempura → Must warn about potential animal fat in batter/frying
- Miso soup → Must check if Dashi (fish stock) is used
- French fries in Belgium → Must warn about animal fat frying

---

## Persona 2: Flexible Vegan - Ben {#flexible-vegan-ben}

### Dietary Profile
- **Type:** Vegan (health + environmental reasons)
- **Strictness:** Moderate - pragmatic
- **Rules:**
  - ✅ Prefers vegan options always
  - ✅ Will choose vegetarian if no vegan available
  - ✅ Small traces in sauces acceptable if unavoidable
  - ❌ No direct meat/fish/eggs in dish
  - ✅ Ok with ⚫⚫◯ confidence if reasoning is provided

### Usage Requirements
- **Needs:** Quick overview of vegan AND vegetarian options
- **Expects:** Ranking (vegan > vegetarian > contains animal products)
- **Values:** Practical advice ("can request without fish sauce")
- **Behavior:** Uses app to find best available option, not just strict vegan
- **Feature needs:**
  - Overlay filters (show vegan, also show vegetarian as backup)
  - Adaptation suggestions ("order without fish sauce")
  - Comparative view (dish A is vegan, dish B is vegetarian)

### Test Cases for Ben
- Pad Thai → May accept if can remove fish sauce
- Vegetarian pizza with cheese → Acceptable fallback option
- Vegetable curry with ghee (clarified butter) → Wants to know, may accept

---

## Persona 3: Vegan + Allergies - Clara {#vegan-allergies-clara}

### Dietary Profile
- **Type:** Vegan + severe allergies
- **Strictness:** Very strict (safety-critical)
- **Rules:**
  - ❌ No animal products (vegan)
  - ❌ No nuts (severe allergy - life-threatening)
  - ❌ No soy (intolerance)
  - ❌ No gluten (celiac disease)
  - ⚠️ Cross-contamination is CRITICAL concern

### Usage Requirements
- **Needs:** Multi-filter capability (vegan AND nut-free AND soy-free AND gluten-free)
- **Expects:** Highest confidence only (⚫⚫⚫) or explicit warning
- **Values:** Complete ingredient transparency
- **Behavior:** Will NOT order unless absolutely certain - risk is too high
- **Feature needs:**
  - Multiple allergen detection (future feature)
  - Clear warnings for uncertain ingredients
  - Phrase generation to ask staff about allergens

### Test Cases for Clara
- Salad with "dressing" → Must identify if nut-based or soy-based dressing
- Gluten-free pasta → Must verify vegan (no egg) AND cross-contamination risk
- Rice noodles → Must check for fish sauce (animal) AND soy sauce (allergen)
- Vegetable stir-fry → Must identify if cooked in sesame/peanut oil

### Notes
Clara's needs partially drive **future allergy detection features** - v1 focuses on vegan/vegetarian, but her persona informs confidence level importance.

---

## Persona 4: Strict Vegetarian - David {#strict-vegetarian-david}

### Dietary Profile
- **Type:** Vegetarian (lacto-ovo - eggs and dairy OK)
- **Strictness:** Strict - no meat, no fish
- **Rules:**
  - ❌ No meat (beef, pork, chicken, lamb, etc.)
  - ❌ No fish or seafood
  - ❌ No meat/fish broths or stocks (bone broth, Dashi, fish sauce)
  - ❌ No gelatin, lard, rennet
  - ✅ Eggs OK
  - ✅ Dairy OK (milk, cheese, butter, yogurt)
  - ✅ Honey OK
  - ✅ Will happily eat vegan options too

### Usage Requirements
- **Needs:** Clear distinction between vegetarian and vegan
- **Expects:** Classification includes "vegetarian (contains dairy/eggs)"
- **Values:** Knowing WHY something isn't vegan (e.g., "contains eggs")
- **Behavior:** Scans for vegetarian, but also interested in vegan options
- **Feature needs:**
  - 🟢 Vegetarian badge distinct from ✅ Vegan badge
  - Ingredient transparency (eggs, dairy clearly marked)
  - Broader options than strict vegans

### Test Cases for David
- Margherita pizza → ✅ Vegetarian (cheese), ❌ not vegan
- Carbonara → ❌ (contains bacon/pancetta)
- Vegetable soup → Must check broth (if chicken/beef stock → ❌)
- Pad Thai → ❌ if contains fish sauce (even without meat pieces)
- Omelet → ✅ Vegetarian (eggs OK for David)

---

## Persona 5: Practical Vegetarian - Eric {#practical-vegetarian-eric}

### Dietary Profile
- **Type:** Vegetarian (practical, not strict)
- **Strictness:** Low to moderate
- **Rules:**
  - ❌ No visible meat (beef, pork, chicken, lamb, etc.)
  - ❌ No visible fish or seafood pieces
  - ✅ Meat/fish broths and stocks are OK (bone broth, chicken stock, Dashi, fish sauce)
  - ✅ Sauces cooked with meat are OK (as long as no meat pieces remain)
  - ✅ Eggs and dairy OK
  - ✅ Honey OK
  - ✅ Cross-contamination not a concern (fried in same oil as meat is fine)
  - ✅ Vegan options also fine

### Usage Requirements
- **Needs:** Clear visibility into whether dish contains actual meat/fish pieces
- **Expects:** Classification distinguishes "contains meat pieces" from "cooked in meat broth"
- **Values:** Practical information ("vegetable ramen, but broth contains pork stock")
- **Behavior:** Scans to avoid meat pieces, not concerned about hidden animal products in sauces
- **Feature needs:**
  - Nuanced classification: "Vegetarian (but contains fish sauce)" vs. "Contains fish pieces"
  - Main ingredient focus (what's IN the dish visibly)
  - Less concerned with confidence levels (⚫⚫◯ or ⚫◯◯ is fine)

### Test Cases for Eric
- Vegetable ramen with pork bone broth → ✅ OK (no visible meat, broth is fine)
- Pad Thai with fish sauce → ✅ OK (fish sauce in cooking, no fish pieces)
- Vegetable soup with chicken stock → ✅ OK (vegetables are main, stock is fine)
- Caesar salad with bacon bits → ❌ NOT OK (visible bacon pieces)
- French fries fried in animal fat → ✅ OK (not concerned about cross-contamination)
- Margherita pizza → ✅ OK (cheese, dairy fine)

### Contrast with Other Personas
- **vs. David (Strict Vegetarian):** David rejects fish sauce/bone broth; Eric is OK with them
- **vs. Fabian (Flexitarian):** Fabian still eats meat; Eric avoids all visible meat
- **vs. Ben (Flexible Vegan):** Ben wants vegan but accepts vegetarian; Eric is OK with animal products in sauces

---

## Persona 6: Pescatarian - Emma {#pescatarian-emma}

### Dietary Profile
- **Type:** Pescatarian (no meat, but fish/seafood OK)
- **Strictness:** Moderate
- **Rules:**
  - ❌ No land animal meat (beef, pork, chicken, lamb)
  - ❌ No meat broths (bone broth, chicken stock)
  - ✅ Fish and seafood OK
  - ✅ Fish-based broths OK (Dashi is fine)
  - ✅ Eggs and dairy OK
  - ✅ Vegan and vegetarian options also fine

### Usage Requirements
- **Needs:** Classification should distinguish "contains fish" from "contains meat"
- **Expects:** Fish sauce is OK, chicken stock is NOT OK
- **Values:** Knowing ingredient source (fish vs. land animal)
- **Behavior:** Looks for seafood, vegetarian, and vegan options - avoids meat
- **Feature needs:**
  - Classification: Vegan / Vegetarian / Pescatarian-OK / Contains Meat
  - Context-aware reasoning (Dashi is fish-based → OK for Emma)

### Test Cases for Emma
- Tonkotsu ramen → ❌ (pork bone broth)
- Miso soup with Dashi → ✅ (fish-based broth is OK)
- Paella with seafood → ✅ (seafood OK)
- Vegetable fried rice with fish sauce → ✅ (fish sauce OK)
- Chicken broth noodle soup → ❌ (chicken is land animal)

---

## Persona 7: Flexitarian - Fabian {#flexitarian-fabian}

### Dietary Profile
- **Type:** Flexitarian (reducing meat, not eliminating)
- **Strictness:** Low - pragmatic and flexible
- **Rules:**
  - ✅ Prefers plant-based or vegetarian options
  - ✅ OK with meat in sauces/broths (hidden meat)
  - ✅ OK with small amounts of meat (garnish, flavoring)
  - ❌ Avoids large meat portions (steak, whole chicken)
  - ✅ Fish OK
  - ✅ Interested in "least meat" options

### Usage Requirements
- **Needs:** Ranking by meat content (vegan > vegetarian > light meat > heavy meat)
- **Expects:** Transparency about how much/where meat is
- **Values:** Practical options ("mostly plants, some fish sauce OK")
- **Behavior:** Uses app to find lighter options, not strict filtering
- **Feature needs:**
  - Gradient classification (not binary vegan/not vegan)
  - "Contains small amount of meat in broth" vs. "Main ingredient is meat"
  - Suggestions for reducing meat (e.g., "can request no bacon topping")

### Test Cases for Fabian
- Vegetable ramen with pork broth → ⚠️ "Contains meat in broth" (acceptable for Fabian)
- Caesar salad with bacon bits → ⚠️ "Contains bacon garnish" (maybe acceptable)
- Grilled steak → ❌ "Main dish is meat" (avoid)
- Pasta with clam sauce → ✅ "Seafood-based, no meat" (good option)
- Vegetable stir-fry with oyster sauce → ⚠️ "Oyster sauce contains seafood extract" (OK)

---

## Persona 8: Allergy-Focused (No Dietary Preference) - Grace {#allergy-focused-grace}

### Dietary Profile
- **Type:** No dietary preference (eats everything), but severe allergies
- **Strictness:** Very strict about allergens only
- **Rules:**
  - ❌ No nuts (anaphylaxis risk)
  - ❌ No shellfish (severe allergy)
  - ❌ No sesame (intolerance)
  - ✅ Meat, fish, dairy, eggs all OK
  - ✅ Not concerned about vegan/vegetarian

### Usage Requirements
- **Needs:** Allergen detection (future feature)
- **Expects:** Clear warnings about nuts, shellfish, sesame
- **Values:** Ingredient transparency for safety
- **Behavior:** Uses app primarily for safety, not dietary preference
- **Feature needs:**
  - Allergen filters (nut-free, shellfish-free, etc.) - **future feature**
  - High confidence allergen detection
  - Warning if ingredients are unclear

### Test Cases for Grace
- Thai curry → Must check for peanuts in sauce
- Pad Thai → Must check for peanuts/cashews garnish
- Sushi → Must identify shellfish (shrimp, crab) vs. fish
- Hummus → ⚠️ May contain sesame (tahini)
- Salad → Must check for nut-based dressing or sesame seeds

### Notes
Grace's needs are **out of scope for v1** (allergen tracking beyond vegan/vegetarian), but her persona informs the importance of:
- High-confidence classification
- Detailed ingredient lists
- Transparent reasoning
- Future allergen detection features

---

## Summary: Persona Classification Needs

| Persona | Vegan | Vegetarian | Visible Meat OK? | Pescatarian | Allergen | Strictness | Confidence Needed |
|---------|-------|------------|------------------|-------------|----------|------------|-------------------|
| Anna (Strict Vegan) | ✅ Only | ❌ | ❌ | ❌ | - | Very High | ⚫⚫⚫ |
| Ben (Flexible Vegan) | ✅ Preferred | ✅ Fallback | ❌ | ❌ | - | Medium | ⚫⚫◯ OK |
| Clara (Vegan + Allergies) | ✅ | ❌ | ❌ | ❌ | Nuts, Soy, Gluten | Extreme | ⚫⚫⚫ Only |
| David (Strict Vegetarian) | ✅ OK | ✅ Main | ❌ | ❌ | - | High | ⚫⚫⚫ |
| Eric (Practical Vegetarian) | ✅ OK | ✅ Main | ❌ (but broth OK) | ❌ | - | Low-Medium | ⚫⚫◯ OK |
| Emma (Pescatarian) | ✅ OK | ✅ OK | ❌ (fish OK) | ✅ Main | - | Medium | ⚫⚫◯ OK |
| Fabian (Flexitarian) | ✅ Preferred | ✅ OK | ⚠️ (avoid large portions) | ✅ OK | - | Low | ⚫◯◯ OK |
| Grace (Allergy-Only) | N/A | N/A | ✅ | N/A | Nuts, Shellfish, Sesame | Extreme | ⚫⚫⚫ Only |

---

## Feature Testing Matrix

### Symbol Recognition (CRITICAL)
- Anna: Trusts 🌱 vegan symbol completely
- David: Needs 🟢 vegetarian symbol distinct from vegan
- All: Symbol overrides LLM classification

### Confidence Levels
- Anna, Clara, Grace: Only trust ⚫⚫⚫ (high confidence)
- David, Emma: Accept ⚫⚫◯ (moderate) with good reasoning
- Ben, Eric, Fabian: Accept ⚫◯◯ (low) if reasoning explains uncertainty

### Cuisine Context Awareness
- Anna, David: Need to know about Belgian fries (animal fat), Dashi (fish stock)
- Ben: Wants to know, but may accept if no alternative
- Eric: Information is nice, but not critical (broths/sauces are OK)
- Emma, Fabian: Fish sauce is OK (pescatarian/flexitarian), Dashi is OK

### Adaptation Suggestions
- Ben: "Can request without fish sauce" (flexible, willing to customize)
- Fabian: "Can request no bacon topping" (reduce meat)
- Anna: Unlikely to customize - needs guaranteed vegan options

### Nuanced Classification Needs
- **Eric (Practical Vegetarian):** Needs distinction between:
  - "Contains meat pieces" (NOT OK)
  - "Cooked in meat broth" (OK)
  - "Contains fish sauce" (OK, if no fish pieces)
- This drives requirement for **ingredient type transparency** (visible vs. hidden)

### Future Features (Out of Scope v1)
- Clara, Grace: Allergen detection beyond vegan/vegetarian
- Fabian: Meat-level gradient (not just binary vegan/not vegan)
- Eric: Nuanced "visible meat" vs. "hidden in broth/sauce" classification
- All: Community reviews, phrase generation
