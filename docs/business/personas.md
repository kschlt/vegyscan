# User Personas

> **Last Updated:** 2025-11-15

_This file is the Single Source of Truth for all user groups and their dietary preferences._

**Focus:** Personas are organized by **dietary type and strictness level** to test different classification requirements, information layers, and UX patterns. Each persona defines **what they test in the product**.

---

## Persona 1: Strict Ethical Vegan - Anna {#strict-vegan-anna}

### Purpose in Design
**Tests:** Upper bound of accuracy, worst-case detection, strictness in NFRs, edge case handling.
**If Anna trusts the output, everyone else will too.**

### Profile
- **Dietary Type:** Vegan (ethical + environmental reasons)
- **Strictness:** Extremely strict - zero tolerance for uncertainty
- **Food Literacy:** Expert-level - deep knowledge of hidden animal products
- **Motivation:** Ethics (animal welfare), environment, health
- **Confidence Threshold:** ⚫⚫⚫ only (high confidence) - will NOT order at ⚫⚫◯ or ⚫◯◯
- **Demographics:** Long-term vegan (5+ years), well-traveled, educated on food systems

### Dietary Rules
- ❌ No animal products whatsoever (meat, fish, dairy, eggs)
- ❌ No honey
- ❌ No animal-derived broths/stocks (Dashi, bone broth, chicken stock)
- ❌ No gelatin, lard, animal fats, rennet
- ❌ Even traces in sauces are unacceptable
- ❌ Cross-contamination is a concern (shared fryers, grills)

### Domain Knowledge (What Anna Knows)
**High awareness of hidden animal products:**
- **Gelatin** (from animal bones/connective tissue) in gummy bears, marshmallows, gelato, some yogurts
- **Rennet** (from calf stomach lining) in most traditional cheeses (Parmesan, Gruyère, etc.)
- **Albumin** (egg protein) used in wine clarification
- **Carmine/Cochineal** (crushed insects) in red food coloring (E120)
- **L-cysteine** (from animal hair/feathers) in bread dough conditioners
- **Isinglass** (fish bladder) in beer/wine filtration
- **Lard** (pig fat) vs. vegetable shortening in pastries
- **Dashi** (fish stock) as default base in Japanese cuisine
- **Oyster sauce, fish sauce** as common Asian condiments
- **Whey** (dairy by-product) in many processed foods
- **Bone char** used in sugar refining (some refined white sugar)
- **Cross-contamination:** shared fryers (fries in same oil as meat), grills, cutting boards

**This knowledge informs her expectations:**
- She expects the app to catch these hidden ingredients (not just obvious meat/fish)
- She looks for symbols first (🌱 vegan symbol most authoritative)
- She reads ingredient lists carefully even when symbol present
- She asks staff about preparation methods (frying oil, stock base, grill cleaning)
- She researches cuisine-specific risks (Belgian fries in animal fat, Japanese Dashi)

### Implications for Requirements

#### Functional Requirements
- **REQ-F-004:** Symbol recognition must be >95% accurate (she trusts symbols)
- **REQ-F-008:** Classification must detect hidden animal products (gelatin, rennet, Dashi, etc.)
- **REQ-F-010:** Classification reasoning must explain WHY something is flagged
- **REQ-F-011:** Warning messages must be clear and specific ("Contains fish stock in broth")
- **REQ-F-012:** Cuisine context awareness (Dashi in Japanese, lard in Chinese, etc.)
- **REQ-F-014:** Dish detail panel must show complete ingredient analysis
- **REQ-F-031:** Smart caching must maintain same strictness (no false positives from cache)

#### Non-Functional Requirements
- **REQ-NF-002:** High precision + extremely high recall for animal-derived ingredients
- **REQ-NF-003:** Traceability - surfaced evidence (OCR excerpt, reasoning chain)
- **REQ-NF-004:** Ability to inspect all data (detailed view, not hidden)

### UX Needs
- **Default view:** Detailed information visible (not collapsed)
- **Warning style:** Clear, specific ("Contains gelatin from animal bones")
- **Confidence display:** Always show confidence level (⚫⚫⚫ / ⚫⚫◯ / ⚫◯◯)
- **Reasoning:** Must always provide "Why?" explanation
- **Symbol trust:** If 🌱 vegan symbol detected, highlight prominently
- **Progressive disclosure:** Not needed - Anna wants to see everything upfront
- **Tolerance for uncertainty:** ZERO - if uncertain, app must warn clearly

### Test Cases for Anna
- ✅ **Tonkotsu ramen** → Must classify as ❌ (pork bone broth)
- ✅ **Vegetable tempura** → Must warn about potential animal fat in batter/frying oil
- ✅ **Miso soup** → Must detect if Dashi (fish stock) is used
- ✅ **French fries in Belgium** → Must warn about animal fat frying (cuisine context)
- ✅ **Gummy bears** → Must detect gelatin if ingredients listed
- ✅ **Caesar dressing** → Must detect anchovy paste if present
- ✅ **Parmesan cheese** → Must detect rennet (animal-derived)
- ✅ **Wine** → Should detect if albumin/isinglass used in filtration (if stated)

---

## Persona 2: Health-Oriented Vegan - Ben {#health-vegan-ben}

### Purpose in Design
**Tests:** Information layering, "don't overwhelm" constraints, simplified views, health-focused metadata, secondary tags.

### Profile
- **Dietary Type:** Vegan (primarily health reasons)
- **Strictness:** Moderate - pragmatic and flexible
- **Food Literacy:** Intermediate - knows obvious issues, not hidden edge cases
- **Motivation:** Health (weight, cholesterol, longevity), some environmental concern
- **Confidence Threshold:** ⚫⚫◯ OK with good reasoning - will accept moderate confidence
- **Demographics:** Newer vegan (1-2 years), health-conscious, less dogmatic

### Dietary Rules
- ✅ Prefers vegan options always
- ✅ Will choose vegetarian if no vegan available (pragmatic)
- ✅ Small traces in sauces acceptable if unavoidable (fish sauce in Pad Thai)
- ❌ No direct meat/fish/eggs in main dish
- ✅ OK with cross-contamination (shared fryers not a concern)
- ✅ Interested in health signals (fried vs. fresh, processed vs. whole foods)

### Domain Knowledge (What Ben Knows)
**Moderate awareness - knows common issues:**
- Obvious animal products (meat, fish, eggs visible in dish)
- Common sauces: fish sauce, oyster sauce
- Dairy products (cheese, milk, cream, butter)
- Basic nutrition (calories, fat, protein)

**Limited knowledge of edge cases:**
- ❌ May not know about gelatin, rennet, carmine, L-cysteine
- ❌ May not think about wine/beer filtration
- ❌ May not ask about frying oil or stock base
- ❌ Doesn't research every ingredient deeply
- ❌ Doesn't know about bone char in sugar

**Health knowledge (unique to Ben):**
- Understands macros (protein, fat, carbs)
- Knows "ultra-processed" vs. "whole foods"
- Cares about cooking methods (fried, grilled, steamed)
- Interested in nutritional density

**This affects his needs:**
- Relies on app to catch hidden ingredients he doesn't know about
- Trusts app more than strict vegans (who double-check everything)
- Values practical guidance over technical perfection
- Wants health-related metadata beyond just vegan/not vegan

### Implications for Requirements

#### Functional Requirements
- **REQ-F-008:** Classification should flag obvious animal products (Ben will accept moderate confidence)
- **REQ-F-010:** Reasoning should be clear but concise (not overwhelming)
- **REQ-F-015:** Overlay system - Ben wants to toggle details (show/hide)
- **REQ-F-026 (Future):** Adaptation suggestions ("can request without fish sauce")
- **Future:** Health tags (fried, processed, fresh, high-protein)

#### Non-Functional Requirements
- **REQ-NF-004:** Progressive disclosure - show essentials first, details on demand
- **REQ-NF-005:** Clean UI with ability to drill deeper (not cluttered)

### UX Needs
- **Default view:** Collapsed/simplified - show overview (green ✅ / yellow ⚠️ / red ❌)
- **Warning style:** Friendly nudges, not scary ("Contains fish sauce - request without?")
- **Confidence display:** Show but don't emphasize (⚫⚫◯ is acceptable)
- **Reasoning:** Concise summary, expandable for details
- **Health metadata:** Visual tags (🔥 fried, 🥗 fresh, ⚙️ processed) - nice to have
- **Progressive disclosure:** Essential - avoid information overload
- **Tolerance for uncertainty:** Moderate - "likely contains X" is acceptable

### Test Cases for Ben
- ✅ **Pad Thai** → May accept if can remove/reduce fish sauce (adaptation suggestion)
- ✅ **Vegetarian pizza with cheese** → Acceptable fallback (vegetarian, not vegan)
- ✅ **Vegetable curry with ghee** → Wants to know it's not vegan, may accept
- ✅ **Gummy bears** → Unlikely to know about gelatin (app must catch and inform)
- ✅ **French fries** → Wants to know if fried (health signal), less concerned about oil type

---

## Persona 3: Strict Vegetarian - David {#strict-vegetarian-david}

### Purpose in Design
**Tests:** Vegetarian vs. vegan distinction, fish/seafood detection, hidden broths/stocks, lacto-ovo classification.

### Profile
- **Dietary Type:** Vegetarian - lacto-ovo (eggs and dairy OK)
- **Strictness:** Strict - no meat, no fish, no hidden animal flesh
- **Food Literacy:** High - knows about hidden fish/meat in broths, sauces, gelatin
- **Motivation:** Ethics (animal welfare), religious/cultural, health
- **Confidence Threshold:** ⚫⚫⚫ preferred - wants high confidence for animal flesh
- **Demographics:** Long-term vegetarian (10+ years), culturally/religiously motivated

### Dietary Rules
- ❌ No meat (beef, pork, chicken, lamb, game)
- ❌ No fish or seafood (including shellfish)
- ❌ No meat/fish broths or stocks (bone broth, Dashi, fish sauce, oyster sauce)
- ❌ No gelatin (made from animal bones), lard, rennet (some cheeses)
- ✅ Eggs OK (lacto-ovo vegetarian)
- ✅ Dairy OK (milk, cheese with vegetarian rennet, butter, yogurt)
- ✅ Honey OK
- ✅ Will happily eat vegan options too

### Domain Knowledge (What David Knows)
**High awareness of hidden animal flesh:**
- **Fish sauce** (fermented fish) in Southeast Asian cuisine (Thai, Vietnamese)
- **Oyster sauce** (oyster extract) in Chinese cooking
- **Dashi** (fish stock) in Japanese cuisine (miso soup, ramen broth)
- **Bone broth** (animal bones) in soups, sauces, risotto
- **Chicken/beef stock** in "vegetable" soups, rice dishes
- **Gelatin** (animal bones) in desserts, marshmallows, gummy candies
- **Lard** (pig fat) in pastries, refried beans (Mexican)
- **Anchovies** in Caesar dressing, Worcestershire sauce
- **Rennet** (calf stomach) in traditional cheese (Parmesan, Gruyère, Pecorino)

**This knowledge informs his expectations:**
- He expects app to catch fish sauce/Dashi/bone broth (critical for vegetarians)
- He needs clear distinction: "vegetarian" vs. "vegan"
- He wants to know WHY something isn't vegan (e.g., "contains eggs" → still OK for him)
- He looks for vegetarian-specific symbols (🟢 vegetarian)

### Implications for Requirements

#### Functional Requirements
- **REQ-F-008:** Classification must detect fish-based ingredients (Dashi, fish sauce, oyster sauce)
- **REQ-F-011:** Must distinguish "vegetarian (contains dairy/eggs)" from "vegan"
- **REQ-F-012:** Cuisine context critical (Dashi in Japanese, fish sauce in Thai)
- **REQ-F-014:** Detail panel must show ingredient source (fish vs. dairy/egg)
- **Symbol distinction:** 🌱 Vegan vs. 🟢 Vegetarian (separate symbols)

#### Non-Functional Requirements
- **REQ-NF-002:** High recall for fish/meat products (can't miss fish sauce)
- **REQ-NF-003:** Clear traceability for "why vegetarian, not vegan" reasoning

### UX Needs
- **Default view:** Show both vegan AND vegetarian options (David eats both)
- **Warning style:** Clear distinction ("Contains fish sauce" = ❌, "Contains eggs" = ✅ for David)
- **Confidence display:** Show confidence, especially for borderline cases
- **Reasoning:** Must explain ingredient type ("Contains: eggs, milk" → still vegetarian)
- **Symbol trust:** Needs 🟢 Vegetarian symbol distinct from 🌱 Vegan
- **Filter options:** Ability to filter "vegetarian OR vegan" (inclusive filter)
- **Tolerance for uncertainty:** Low for fish/meat, moderate for dairy/eggs

### Test Cases for David
- ✅ **Margherita pizza** → ✅ Vegetarian (cheese), ❌ not vegan (clear distinction)
- ✅ **Carbonara** → ❌ NOT vegetarian (contains bacon/pancetta)
- ✅ **Vegetable soup** → Must check broth (chicken/beef stock → ❌, vegetable stock → ✅)
- ✅ **Pad Thai** → ❌ if contains fish sauce (even without visible fish pieces)
- ✅ **Omelet** → ✅ Vegetarian (eggs OK for David)
- ✅ **Miso soup** → Must detect Dashi (fish stock) → ❌ for David
- ✅ **Parmesan cheese** → Depends on rennet type (animal rennet → ❌, microbial rennet → ✅)

---

## Persona 4: Practical Vegetarian - Eric {#practical-vegetarian-eric}

### Purpose in Design
**Tests:** "Visible vs. hidden meat" distinction, nuanced classification, low strictness tolerance, convenience over perfection.

### Profile
- **Dietary Type:** Vegetarian (practical, cultural)
- **Strictness:** Low to moderate - avoids visible meat only
- **Food Literacy:** Medium - surface-level awareness, doesn't research deeply
- **Motivation:** Cultural upbringing, habit, partial ethics
- **Confidence Threshold:** ⚫⚫◯ OK - accepts moderate confidence, not perfectionist
- **Demographics:** Cultural vegetarian (Indian, Buddhist background), pragmatic

### Dietary Rules
- ❌ No visible meat pieces (beef, pork, chicken, lamb)
- ❌ No visible fish or seafood pieces
- ✅ Meat/fish broths and stocks are OK (bone broth, chicken stock, Dashi, fish sauce)
- ✅ Sauces cooked with meat are OK (as long as no meat pieces remain)
- ✅ Eggs and dairy OK
- ✅ Honey OK
- ✅ Cross-contamination not a concern (shared fryers, grills fine)
- ✅ Vegan options also fine

### Domain Knowledge (What Eric Knows)
**Basic awareness - surface-level only:**
- Can identify visible meat/fish pieces in dish
- Knows major animal products (beef, pork, chicken, fish, eggs, dairy)
- Recognizes common dishes with meat

**Limited knowledge of hidden ingredients:**
- ❌ Doesn't think about broths/stocks (assumes "vegetable soup" is OK even if chicken stock)
- ❌ Doesn't know about gelatin, rennet, fish sauce, oyster sauce
- ❌ Doesn't ask about preparation methods (frying oil, grill cleaning)
- ❌ Doesn't research ingredient lists
- ❌ Doesn't know about Dashi in Japanese cuisine

**This affects his needs:**
- App must distinguish "visible meat pieces" vs. "hidden in broth/sauce"
- Needs simple classification ("has meat" vs. "vegetable dish")
- Less concerned with technical accuracy or edge cases
- Values convenience and speed over strictness
- May order dishes that Anna/David would reject (because of hidden broths)

### Implications for Requirements

#### Functional Requirements
- **REQ-F-008:** Classification should focus on MAIN ingredients (visible components)
- **REQ-F-011:** Nuanced classification needed:
  - "Contains meat pieces" (NOT OK for Eric)
  - "Cooked in meat broth" (OK for Eric, but inform)
  - "Contains fish sauce" (OK for Eric if no fish pieces)
- **Future:** Ingredient type transparency (visible vs. hidden)

#### Non-Functional Requirements
- **REQ-NF-004:** Simple, scannable UI - Eric won't read long explanations
- **REQ-NF-001:** Speed is important - Eric values quick results over deep analysis

### UX Needs
- **Default view:** Simple overview (✅ Vegetarian / ⚠️ Contains broth / ❌ Contains meat)
- **Warning style:** Casual, informative ("Vegetable ramen, but pork broth")
- **Confidence display:** Not critical - Eric accepts ⚫⚫◯ or even ⚫◯◯
- **Reasoning:** Brief, main point only ("No visible meat, but fish sauce in cooking")
- **Progressive disclosure:** Minimal details by default (Eric won't expand)
- **Tolerance for uncertainty:** High - Eric is flexible and pragmatic

### Test Cases for Eric
- ✅ **Vegetable ramen with pork bone broth** → ✅ OK for Eric (no visible meat, broth is fine)
- ✅ **Pad Thai with fish sauce** → ✅ OK for Eric (fish sauce in cooking, no fish pieces)
- ✅ **Vegetable soup with chicken stock** → ✅ OK for Eric (vegetables are main, stock is fine)
- ❌ **Caesar salad with bacon bits** → ❌ NOT OK (visible bacon pieces)
- ✅ **French fries fried in animal fat** → ✅ OK (not concerned about cross-contamination)
- ✅ **Margherita pizza** → ✅ OK (cheese, dairy fine)
- ✅ **Gummy bears with gelatin** → Doesn't know/care about gelatin (app can inform, he may ignore)

### Contrast with Other Personas
- **vs. David (Strict Vegetarian):** David rejects fish sauce/bone broth; Eric is OK with them
- **vs. Sarah (Social Vegetarian):** Sarah may eat meat occasionally; Eric never eats visible meat
- **vs. Ben (Flexible Vegan):** Ben wants vegan but accepts vegetarian; Eric is OK with animal products in sauces/broths

---

## Persona 5: Pescatarian - Emma {#pescatarian-emma}

### Purpose in Design
**Tests:** Fish vs. meat distinction, pescatarian-specific classification, icon/tag system for fish/meat/vegan/vegetarian.

### Profile
- **Dietary Type:** Pescatarian (no land animal meat, fish/seafood OK)
- **Strictness:** Moderate - clear boundaries for land animals
- **Food Literacy:** Medium - knows fish vs. meat distinction, moderately aware of broths
- **Motivation:** Health, environmental (overfishing concerns for some), flexibility
- **Confidence Threshold:** ⚫⚫◯ OK - accepts moderate confidence with reasoning
- **Demographics:** Health-conscious, environmentally aware, pragmatic eater

### Dietary Rules
- ❌ No land animal meat (beef, pork, chicken, lamb, game)
- ❌ No meat broths from land animals (bone broth, chicken stock, beef stock)
- ❌ No lard, gelatin from land animals
- ✅ Fish and seafood OK (salmon, tuna, shrimp, crab, squid, etc.)
- ✅ Fish-based broths OK (Dashi is fine)
- ✅ Fish sauce, oyster sauce OK
- ✅ Eggs and dairy OK
- ✅ Vegan and vegetarian options also fine

### Domain Knowledge (What Emma Knows)
**Moderate awareness - fish vs. meat distinction:**
- Knows fish sauce is fish-based (OK for her)
- Knows Dashi is fish stock (OK for her)
- Knows oyster sauce contains oyster extract (OK for her)
- Knows bone broth is from land animals (NOT OK)
- Knows chicken/beef stock is from land animals (NOT OK)
- Knows gelatin can be from land animals (NOT OK) or fish (OK)

**What Emma needs from the app:**
- Clear distinction: "Contains fish" (✅) vs. "Contains meat" (❌)
- Broth source identification: Dashi (fish-based, ✅) vs. bone broth (land animal, ❌)
- Ingredient source transparency: fish sauce (✅) vs. chicken stock (❌)

### Implications for Requirements

#### Functional Requirements
- **REQ-F-008:** Classification must distinguish fish/seafood from land animal meat
- **REQ-F-011:** Classification levels needed:
  - 🌱 Vegan (best)
  - 🟢 Vegetarian (good)
  - 🐟 Pescatarian-OK (contains fish/seafood, OK for Emma)
  - 🥩 Contains Meat (NOT OK for Emma)
- **REQ-F-012:** Cuisine context awareness (Dashi = fish stock = OK for Emma)
- **REQ-F-014:** Detail panel should show ingredient source (fish vs. land animal)
- **Future:** Icon system (vegan/vegetarian/fish/meat icons) - Emma benefits from this

#### Non-Functional Requirements
- **REQ-NF-004:** Clear visual distinction (fish icon vs. meat icon)

### UX Needs
- **Default view:** Show vegan, vegetarian, AND pescatarian-OK options
- **Warning style:** Clear source identification ("Contains fish sauce" = ✅, "Contains chicken stock" = ❌)
- **Confidence display:** Show confidence, especially for broth/sauce ingredients
- **Reasoning:** Must explain ingredient source (fish-based vs. land animal-based)
- **Icon system:** Visual icons for fish/meat/vegan/vegetarian (future feature)
- **Filter options:** Ability to filter "pescatarian-OK OR vegetarian OR vegan"
- **Tolerance for uncertainty:** Moderate - Emma wants clarity on ingredient source

### Test Cases for Emma
- ✅ **Tonkotsu ramen** → ❌ NOT OK (pork bone broth from land animal)
- ✅ **Miso soup with Dashi** → ✅ OK (fish-based broth is fine)
- ✅ **Paella with seafood** → ✅ OK (seafood is fine)
- ✅ **Vegetable fried rice with fish sauce** → ✅ OK (fish sauce is fine)
- ❌ **Chicken broth noodle soup** → ❌ NOT OK (chicken is land animal)
- ✅ **Caesar salad with anchovy dressing** → ✅ OK (anchovies are fish)
- ❌ **Caesar salad with bacon bits** → ❌ NOT OK (bacon is land animal meat)
- ✅ **Pad Thai with shrimp** → ✅ OK (shrimp is seafood)

### Future Feature Value
Emma is the primary driver for **icon-based classification** (future feature):
- If app adds visual icons for food types (🌱 vegan, 🟢 vegetarian, 🐟 fish, 🥩 meat)
- Emma can quickly scan menu: "Oh, I can directly see what is fish, what is meat"
- This feature would benefit all personas for faster scanning

---

## Persona 6: Social/Flexible Vegetarian - Sarah {#social-vegetarian-sarah}

### Purpose in Design
**Tests:** Lowest detail level, highest-level summary, "don't overwhelm" constraints, simple yes/no/maybe indicators, social flexibility.

### Profile
- **Dietary Type:** Vegetarian (social/flexible identity)
- **Strictness:** Low - identifies as vegetarian but will sometimes compromise
- **Food Literacy:** Low - knows obvious meat, doesn't research hidden ingredients
- **Motivation:** Social identity, health trends, environmental awareness (casual)
- **Confidence Threshold:** ⚫◯◯ OK - accepts low confidence, easily overwhelmed by detail
- **Demographics:** Newer vegetarian (< 1 year), young adult, social eater

### Dietary Rules
- ✅ Prefers vegetarian options always (identity)
- ✅ Will eat vegan options (no problem)
- ⚠️ Will sometimes compromise in social settings (e.g., "just pick out the meat")
- ❌ Generally avoids visible meat (beef, pork, chicken, fish)
- ✅ OK with eggs, dairy
- ✅ Doesn't think about broths, stocks, hidden ingredients
- ✅ Cross-contamination not a concern at all

### Domain Knowledge (What Sarah Knows)
**Low awareness - basic only:**
- Can identify obvious meat (steak, chicken breast, fish fillet)
- Knows dairy and eggs (vegetarian)
- Knows vegan means no animal products

**Very limited knowledge:**
- ❌ Doesn't know about fish sauce, oyster sauce, Dashi
- ❌ Doesn't know about gelatin, rennet, stocks/broths
- ❌ Doesn't research ingredients
- ❌ Doesn't ask about preparation methods
- ❌ Won't read long ingredient lists (easily overwhelmed)

**This affects her needs:**
- Needs simplest possible UI (one glance understanding)
- Wants quick reassurance: "This is vegetarian-friendly" or "Can be made vegetarian"
- Low willingness to deep-dive into details
- May ignore warnings if too complex or scary
- Values speed and simplicity over accuracy

### Implications for Requirements

#### Functional Requirements
- **REQ-F-008:** Simple classification (vegetarian: yes/no/maybe)
- **REQ-F-011:** High-level indicators only:
  - ✅ "Vegetarian-friendly"
  - ⚠️ "Can be made vegetarian" (with modifications)
  - ❌ "Contains meat"
- **REQ-F-015:** Overlay system - Sarah uses "show less" mode (minimal detail)
- **Future:** Visual summaries (number of vegetarian options per page)

#### Non-Functional Requirements
- **REQ-NF-004:** Lowest cognitive load required - must not scare or overwhelm
- **REQ-NF-001:** Speed critical - Sarah won't wait for detailed analysis

### UX Needs
- **Default view:** Highest-level abstraction (simple icons: ✅ / ⚠️ / ❌)
- **Warning style:** Friendly nudges, not fear ("This dish has meat, but you might like...")
- **Confidence display:** Hide or minimize (Sarah doesn't care about ⚫⚫⚫ vs ⚫⚫◯)
- **Reasoning:** Hide by default (Sarah won't read it)
- **Progressive disclosure:** Critical - show absolute minimum, hide everything else
- **Visual summaries:** "5 vegetarian options on this page" (quick scan)
- **Modification suggestions:** Simple, friendly ("Ask for no bacon topping")
- **Tolerance for uncertainty:** Very high - Sarah is flexible and won't stress over edge cases

### Test Cases for Sarah
- ✅ **Margherita pizza** → ✅ "Vegetarian-friendly" (simple, clear)
- ⚠️ **Caesar salad** → ⚠️ "Can be made vegetarian - request no anchovies" (modification)
- ❌ **Grilled chicken pasta** → ❌ "Contains meat" (clear no)
- ✅ **Vegetable stir-fry** → ✅ "Vegetarian-friendly" (Sarah won't worry about oyster sauce)
- ✅ **Pad Thai** → Likely classified as ✅ for Sarah (she won't know about fish sauce, app should inform but not scare)

### Contrast with Other Personas
- **vs. Eric (Practical Vegetarian):** Eric never compromises on visible meat; Sarah sometimes does
- **vs. David (Strict Vegetarian):** David researches deeply; Sarah doesn't
- **vs. Ben (Health Vegan):** Ben wants health metadata; Sarah just wants simple yes/no

---

## Persona 7: Allergy-Constrained Vegan - Clara {#allergy-vegan-clara}

### Purpose in Design
**Tests:** Safety-critical use case, multi-filter stacking, allergen detection, conservative uncertainty handling, worst-case risk scenarios.

### Profile
- **Dietary Type:** Vegan + severe allergies
- **Strictness:** Extreme - safety is life-threatening concern
- **Food Literacy:** High - must research everything for safety
- **Motivation:** Ethics (vegan) + safety (allergies) - both non-negotiable
- **Confidence Threshold:** ⚫⚫⚫ only - will NOT risk ⚫⚫◯ or ⚫◯◯ due to allergy danger
- **Demographics:** Long-term vegan with diagnosed allergies, highly cautious, safety-first

### Dietary Rules
#### Vegan Rules:
- ❌ No animal products (meat, fish, dairy, eggs)
- ❌ No honey
- ❌ No animal-derived broths, gelatin, etc.

#### Allergy Rules (CRITICAL - life-threatening):
- ❌ No nuts (anaphylaxis risk - tree nuts and peanuts)
- ❌ No soy (severe intolerance)
- ❌ No gluten (celiac disease)
- ❌ No shellfish (severe allergy)
- ⚠️ Cross-contamination is CRITICAL concern (shared surfaces, oils, utensils)

### Domain Knowledge (What Clara Knows)
**Expert-level awareness (both vegan + allergen):**
- All vegan hidden ingredients (same as Anna)
- All allergen sources:
  - **Nuts:** Almond milk, cashew cream, peanut oil, nut-based dressings, marzipan
  - **Soy:** Tofu, tempeh, soy sauce, edamame, soybean oil, lecithin
  - **Gluten:** Wheat, barley, rye, malt, seitan, couscous, many sauces (wheat as thickener)
  - **Shellfish:** Shrimp paste, oyster sauce, crab in sushi, cross-contamination in seafood restaurants
- **Cross-contamination risks:** Shared fryers (fries fried in same oil as breaded shrimp), shared cutting boards, shared grills

**This knowledge informs her expectations:**
- She expects app to catch ALL allergens with high confidence
- She needs stacked filters: "vegan + nut-free + soy-free + gluten-free"
- She wants clear warnings if ingredients are unclear ("Uncertain: may contain traces")
- She asks detailed questions to staff (preparation, cross-contact)
- She will NOT order unless absolutely certain - risk is too high

### Implications for Requirements

#### Functional Requirements
- **REQ-F-008:** Classification must detect allergens (nuts, soy, gluten, shellfish)
- **REQ-F-011:** Must support multi-filter stacking ("vegan AND nut-free AND soy-free")
- **REQ-F-014:** Detail panel must show ALL ingredients with allergen highlighting
- **REQ-F-010:** Reasoning must be transparent and conservative ("Uncertain ingredients detected")
- **Future (v2+):** Allergen-specific detection beyond vegan/vegetarian
- **Future:** Cross-contamination warnings (shared fryers, surfaces)
- **Future:** Personal allergen profile (persistent settings)

#### Non-Functional Requirements
- **REQ-NF-002:** Precision extremely important for allergens (false negatives = danger)
- **REQ-NF-003:** App must be conservative - warn when uncertain
- **REQ-NF-004:** Complete transparency - Clara needs to inspect everything

### UX Needs
- **Default view:** Detailed allergen information visible (not collapsed)
- **Warning style:** Clear, safety-focused ("⚠️ ALLERGEN: Contains nuts", red flags)
- **Confidence display:** Always show - Clara only trusts ⚫⚫⚫
- **Reasoning:** Must show complete ingredient analysis
- **Allergen highlighting:** Visual emphasis on allergens (red text, icons)
- **Uncertainty handling:** Conservative warnings ("Ingredient unclear - may contain soy")
- **Filter stacking:** Ability to enable multiple filters simultaneously
- **Progressive disclosure:** Not applicable - Clara needs all information upfront
- **Tolerance for uncertainty:** ZERO - if uncertain, app must warn clearly (safety-first)

### Test Cases for Clara
- ✅ **Salad with "dressing"** → Must identify if nut-based (almond) or soy-based (tofu mayo) dressing
- ✅ **Gluten-free pasta** → Must verify vegan (no egg) AND gluten-free AND check sauce for soy/nuts
- ✅ **Rice noodles** → Must check for fish sauce (animal) AND soy sauce (allergen) AND gluten (cross-contamination)
- ✅ **Vegetable stir-fry** → Must identify if cooked in sesame/peanut oil (allergen)
- ❌ **Pad Thai** → ❌ Multiple issues (peanuts garnish, soy sauce, fish sauce, possible gluten in noodles)
- ⚠️ **French fries** → Must warn about shared fryers (cross-contamination with breaded items containing gluten)
- ✅ **Hummus** → Must detect tahini (sesame) - not in Clara's allergen list but important for others

### Notes
- Clara's needs partially drive **future allergy detection features** (v2+)
- v1 focuses on vegan/vegetarian classification, but Clara's persona informs:
  - Importance of high-confidence classification
  - Need for detailed ingredient transparency
  - Conservative uncertainty handling
  - Multi-filter architecture (future extensibility)
- Clara represents the **safety-critical use case** - if app works for her, it's robust enough for all users

---

## Summary: Optimized Persona Set

### Persona Count: 7 (Reduced from 8)

| # | Persona | Dietary Type | Literacy | Strictness | Purpose in Design |
|---|---------|--------------|----------|------------|-------------------|
| 1 | Anna | Strict Ethical Vegan | Expert | Extreme | Upper bound accuracy, edge case detection |
| 2 | Ben | Health-Oriented Vegan | Intermediate | Moderate | Information layering, health metadata |
| 3 | David | Strict Vegetarian | High | High | Veg/vegan distinction, fish detection |
| 4 | Eric | Practical Vegetarian | Medium | Low-Med | Visible vs. hidden meat, convenience |
| 5 | Emma | Pescatarian | Medium | Moderate | Fish vs. meat distinction, icon system |
| 6 | Sarah | Social Vegetarian | Low | Low | Simplest UI, highest-level summary |
| 7 | Clara | Allergy-Constrained Vegan | Expert | Extreme | Safety-critical, multi-filter, allergens |

### Removed Personas
- **Fabian (Flexitarian):** Replaced by Sarah (Social/Flexible Vegetarian) - clearer vegetarian focus, tests low-detail UI better
- **Grace (Allergy-Only):** Merged into Clara (Allergy-Constrained Vegan) - allergen testing now combined with vegan use case

### Key Design Drivers

#### Accuracy & Detection (Anna, David, Clara)
- High confidence required (⚫⚫⚫ only)
- Edge case detection (gelatin, rennet, Dashi, fish sauce)
- Complete ingredient transparency
- Conservative uncertainty handling

#### Information Layering (Ben, Sarah)
- Progressive disclosure (show less by default for Sarah, expandable for Ben)
- Health metadata (Ben wants fried/fresh tags)
- Simple summaries (Sarah needs yes/no/maybe only)
- Avoid overwhelming users

#### Classification Nuance (Eric, Emma)
- Visible vs. hidden meat distinction (Eric)
- Fish vs. land animal distinction (Emma)
- Pescatarian-OK classification level (Emma)
- Nuanced reasoning ("contains broth" vs. "contains meat pieces")

#### Safety & Multi-Filter (Clara)
- Allergen detection (future feature)
- Multi-filter stacking (vegan + nut-free + soy-free + gluten-free)
- Safety-first uncertainty handling
- Cross-contamination awareness

---

## Feature Testing Matrix

### Symbol Recognition (CRITICAL - REQ-F-004)
- **Anna, David, Clara:** Trust symbols completely (🌱 vegan, 🟢 vegetarian)
- **All personas:** Symbol overrides LLM classification (most authoritative source)
- **Target:** >95% symbol recognition accuracy

### Confidence Levels (REQ-F-009)
| Persona | ⚫⚫⚫ High | ⚫⚫◯ Moderate | ⚫◯◯ Low |
|---------|-----------|---------------|---------|
| Anna | Required | Reject | Reject |
| Ben | Preferred | Accept | Avoid |
| David | Preferred | Accept with reasoning | Avoid |
| Eric | OK | OK | OK |
| Emma | Preferred | Accept | Avoid |
| Sarah | Don't show | Don't show | Don't show |
| Clara | Required | Reject | Reject |

### Cuisine Context Awareness (REQ-F-012)
- **Anna, David:** Must know Belgian fries (animal fat), Dashi (fish stock), lard (Chinese pastries)
- **Ben:** Wants to know, but may accept if no alternative
- **Eric:** Information nice to have, but not critical (broths/stocks OK for him)
- **Emma:** Must know Dashi = fish stock = OK for her, bone broth = NOT OK
- **Sarah:** Don't overwhelm - simple warning only if critical
- **Clara:** Must know for safety (allergen in preparation)

### Detail Level & Progressive Disclosure (REQ-NF-004)
| Persona | Default View | Expandable Details | Reasoning Shown |
|---------|--------------|-------------------|-----------------|
| Anna | Detailed | Yes (always expanded) | Always |
| Ben | Summary | Yes (collapsed, user expands) | On demand |
| David | Moderate | Yes (collapsed) | Always |
| Eric | Simple | Rarely (won't expand) | Brief only |
| Emma | Moderate | Yes (collapsed) | On demand |
| Sarah | Minimal | No (won't read) | Hidden |
| Clara | Detailed | Yes (always expanded) | Always |

### Adaptation Suggestions (Future - REQ-F-026)
- **Ben:** "Can request without fish sauce" (flexible, willing to customize)
- **Sarah:** "Can be made vegetarian - no bacon" (social flexibility)
- **Anna, David, Clara:** Unlikely to customize - need guaranteed safe options
- **Eric, Emma:** May customize if convenient

### Multi-Filter Stacking (Future - Clara-driven)
- **Clara:** Needs vegan + nut-free + soy-free + gluten-free (simultaneous)
- **Future extensibility:** Architecture must support multi-filter from v1 (even if only vegan/veg in v1)

---

## Persona-Driven Requirements Summary

### Functional Requirements by Persona

**REQ-F-004: Symbol Recognition (Anna, David, Clara drive)**
- >95% accuracy required for trust
- Symbols override LLM classification

**REQ-F-008: Vegan/Vegetarian Classification (All personas)**
- Anna: Must detect hidden ingredients (gelatin, rennet, Dashi)
- David: Must distinguish vegetarian vs. vegan
- Eric: Focus on visible meat vs. hidden in broth
- Emma: Must distinguish fish vs. land animal meat

**REQ-F-009: Confidence Levels (Anna, Clara require ⚫⚫⚫)**
- 3-tier system: ⚫⚫⚫ / ⚫⚫◯ / ⚫◯◯
- Conservative for strict personas (Anna, David, Clara)
- Flexible for pragmatic personas (Ben, Eric, Sarah)

**REQ-F-012: Cuisine Context Awareness (Anna, David, Emma drive)**
- Dashi in Japanese cuisine (fish stock)
- Belgian fries (animal fat)
- Thai/Vietnamese (fish sauce)
- Chinese (oyster sauce, lard)

**REQ-F-015: Overlay System (Ben, Sarah need "show less")**
- Toggle translations, badges, icons
- Sarah needs minimal view
- Ben needs expandable details
- Anna/Clara need full details always

### Non-Functional Requirements by Persona

**REQ-NF-001: Instant UX (All personas, especially Sarah, Eric)**
- <2 seconds to interactive view
- Lazy loading (photo/hotspots first)
- Sarah won't wait for slow results

**REQ-NF-004: Progressive Disclosure (Ben, Sarah drive)**
- Avoid information overload
- Default collapsed for Ben/Sarah
- Default expanded for Anna/Clara

**REQ-NF-002: Accuracy (Anna, David, Clara drive)**
- High precision + high recall for animal products
- Conservative for safety-critical (Clara)

---

## Changes from Previous Persona Set

### Added
- **Sarah (Social/Flexible Vegetarian):** Tests lowest-detail UI, social flexibility, "don't overwhelm" constraints

### Enhanced
- **Ben:** Now "Health-Oriented Vegan" (was "Flexible Vegan") - added health metadata needs (fried/fresh tags)
- **Clara:** Merged with Grace - now comprehensive allergy + vegan persona (was just vegan + allergies)

### Removed
- **Fabian (Flexitarian):** Replaced by Sarah - clearer vegetarian identity, better tests low-literacy UI
- **Grace (Allergy-Only):** Merged into Clara - allergen testing now combined with vegan use case

### Kept (per user request)
- **Emma (Pescatarian):** Valuable for fish vs. meat distinction, drives future icon system (🌱 vegan, 🟢 vegetarian, 🐟 fish, 🥩 meat)

### Result
- **7 personas** (down from 8)
- More actionable for requirements (each has "Purpose in Design")
- Clear literacy levels (Expert/High/Intermediate/Medium/Low)
- Better information layering guidance (Anna/Clara: show all, Ben: expandable, Sarah: minimal)
- No mode switching - personas test requirements, not app modes
