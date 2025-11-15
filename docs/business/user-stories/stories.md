# User Stories

> **Last Updated:** 2025-11-15

User stories organized by Epic, with links to personas, use cases, and requirements.

---

## Epic: Menu Scanning & OCR

_Core scanning functionality - capture photo, optimize, extract text, recognize symbols_

### US-001: Capture Menu Photo with Guide Lines [Draft]

**As a** [Marcus](../personas.md#marcus-health-professional),
**I want to** see guide lines when photographing a menu,
**so that** I can quickly align the photo properly without fumbling.

**Acceptance Criteria:**
- [ ] Guide lines appear immediately when camera opens
- [ ] Guide box turns green when menu is properly aligned
- [ ] I can capture manually or wait for auto-capture
- [ ] Capture completes within 1 second

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Requirements: [REQ-F-001](../requirements/functional.md#req-f-001), [REQ-F-025](../requirements/functional.md#req-f-025)

---

### US-002: Automatic Image Optimization [Draft]

**As a** [All users](../personas.md),
**I want to** see my crooked menu photo automatically straightened and brightened,
**so that** I don't have to retake photos or manually edit them.

**Acceptance Criteria:**
- [ ] Skewed menu is automatically straightened
- [ ] Dark photos are brightened
- [ ] Shadows are removed
- [ ] Optimization happens without my intervention
- [ ] Original layout is preserved

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Requirements: [REQ-F-002](../requirements/functional.md#req-f-002)

---

### US-003: Symbol Recognition (CRITICAL) [Draft]

**As a** [Anna (Strict Vegan)](../personas.md#strict-vegan-anna),
**I want to** have menu symbols (🌱, V) automatically recognized and associated with dishes,
**so that** I can trust the vegan classification when a symbol is present.

**Acceptance Criteria:**
- [ ] Vegan symbols (🌱, VG) are detected
- [ ] Vegetarian symbols (🟢, V) are detected
- [ ] Symbol is linked to correct dish
- [ ] Symbol overrides LLM classification
- [ ] Detection accuracy > 95%

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Requirements: [REQ-F-004](../requirements/functional.md#req-f-004)

---

### US-004: Meta-Information Bundling [Draft]

**As a** [All users](../personas.md),
**I want to** have all information for a dish (name, description, price, symbols) grouped together,
**so that** the classification is based on complete context.

**Acceptance Criteria:**
- [ ] Dish name and description are grouped
- [ ] Price is associated with correct dish
- [ ] Symbols are linked to correct dish
- [ ] Ingredient lists (if present) are bundled
- [ ] Bundling accuracy > 90%

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Requirements: [REQ-F-005](../requirements/functional.md#req-f-005)

---

## Epic: Translation & Understanding

_Translate menus to user's language, explain dishes_

### US-005: Set Target Language [Draft]

**As a** [All users](../personas.md),
**I want to** set my preferred language in settings,
**so that** all menus are translated to my language automatically.

**Acceptance Criteria:**
- [ ] Language selection available in settings
- [ ] Major world languages supported
- [ ] Defaults to device language
- [ ] Choice persists across sessions
- [ ] Affects all future scans

**Related:**
- Requirements: [REQ-F-007](../requirements/functional.md#req-f-007)

---

### US-006: Translate Menu to My Language [Draft]

**As a** [All users](../personas.md),
**I want to** see dish names and descriptions translated to my language,
**so that** I understand what I'm ordering.

**Acceptance Criteria:**
- [ ] Dish names are translated
- [ ] Descriptions are translated
- [ ] Ingredient lists are translated
- [ ] Mixed-language menus are handled (combine sources)
- [ ] Translation quality is good (context-aware)

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Requirements: [REQ-F-006](../requirements/functional.md#req-f-006)

---

### US-007: Understand Dish Types [Draft]

**As a** [All users](../personas.md),
**I want to** know what type of dish this is (e.g., "Japanese Ramen"),
**so that** I understand the category and context.

**Acceptance Criteria:**
- [ ] Dish type is identified (Tonkotsu, Frikandel, Pho, etc.)
- [ ] Type is displayed in detail panel
- [ ] Brief explanation provided ("Rich pork bone broth ramen")
- [ ] Regional variations recognized

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Requirements: [REQ-F-011](../requirements/functional.md#req-f-011)

---

## Epic: Vegan/Vegetarian Classification

_Core value proposition - determine if dish is vegan/vegetarian_

### US-008: Vegan/Vegetarian Classification [Draft]

**As a** [Anna (Strict Vegan)](../personas.md#strict-vegan-anna),
**I want to** know if a dish is vegan, vegetarian, or contains animal products,
**so that** I can order with confidence.

**Acceptance Criteria:**
- [ ] Classification: Vegan / Vegetarian / Contains Animal Products
- [ ] Menu symbols considered (highest authority)
- [ ] Dish name and ingredients analyzed
- [ ] Cuisine context applied (Dashi in Japanese food)
- [ ] Hidden animal products identified (broths, sauces)

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Requirements: [REQ-F-008](../requirements/functional.md#req-f-008)

---

### US-009: Confidence Level Display [Draft]

**As a** [Anna (Strict Vegan)](../personas.md#strict-vegan-anna),
**I want to** see a confidence level (⚫⚫⚫, ⚫⚫◯, ⚫◯◯) for the classification,
**so that** I know how certain the app is and can decide if I trust it.

**Acceptance Criteria:**
- [ ] Three confidence levels displayed
- [ ] ⚫⚫⚫ (high) when menu symbol or well-known dish
- [ ] ⚫⚫◯ (moderate) when typical recipe known
- [ ] ⚫◯◯ (low) when insufficient info
- [ ] Legend explains what each level means

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Requirements: [REQ-F-009](../requirements/functional.md#req-f-009)

---

### US-010: Transparent Reasoning [Draft]

**As a** [All vegan/vegetarian users](../personas.md),
**I want to** understand WHY a dish is classified as vegan/not vegan,
**so that** I can trust the result and make informed decisions.

**Acceptance Criteria:**
- [ ] Reasoning explains WHY (not just WHAT)
- [ ] Specific animal products identified ("contains fish sauce")
- [ ] Cuisine context referenced ("Belgian fries often fried in animal fat")
- [ ] Uncertainty explained ("ingredients not clearly listed")
- [ ] Reasoning is concise (1-2 sentences)

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Requirements: [REQ-F-010](../requirements/functional.md#req-f-010)

---

### US-011: Cuisine Context Awareness [Draft]

**As a** [Anna (Strict Vegan)](../personas.md#strict-vegan-anna),
**I want to** be warned about country-specific cooking methods (Belgian animal fat frying, Japanese Dashi),
**so that** I'm aware of hidden animal products that vary by region.

**Acceptance Criteria:**
- [ ] Cuisine type detected from menu
- [ ] Country-specific rules applied (Dashi in Japan)
- [ ] Regional cooking methods identified (Belgian frying)
- [ ] Traditional ingredients considered (fish sauce in Thai)
- [ ] Context displayed in reasoning

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Requirements: [REQ-F-012](../requirements/functional.md#req-f-012)

---

### US-012: Distinguish Visible vs. Hidden Meat [Draft]

**As a** [Eric (Practical Vegetarian)](../personas.md#practical-vegetarian-eric),
**I want to** know if meat is visible in the dish vs. hidden in broth/sauce,
**so that** I can choose dishes without meat pieces even if broth contains meat.

**Acceptance Criteria:**
- [ ] Classification distinguishes "contains meat pieces" from "meat in broth"
- [ ] "Vegetable ramen with pork broth" clearly labeled
- [ ] "Caesar salad with bacon bits" shows visible meat
- [ ] Fish sauce in dish labeled as "contains fish sauce" (not "contains fish")

**Related:**
- Persona: [Eric](../personas.md#practical-vegetarian-eric)
- Requirements: [REQ-F-008](../requirements/functional.md#req-f-008)

---

## Epic: Interactive Navigation

_Hotspots, detail panels, overlays_

### US-013: Interactive Hotspots on Menu [Draft]

**As a** [All users](../personas.md),
**I want to** see interactive hotspots overlaid on menu items,
**so that** I can tap to get details while keeping the original menu visible.

**Acceptance Criteria:**
- [ ] Hotspots placed over each menu item
- [ ] Hotspots are tappable
- [ ] Subtle visual style (doesn't obscure text)
- [ ] Accurate positioning
- [ ] Tap opens detail panel

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md), [UC-003](../use-cases/UC-003-view-dish-details.md)
- Requirements: [REQ-F-013](../requirements/functional.md#req-f-013)

---

### US-014: Dish Detail Panel [Draft]

**As a** [All users](../personas.md),
**I want to** see a detail panel when I tap a dish,
**so that** I get translation, ingredients, and vegan/vegetarian classification.

**Acceptance Criteria:**
- [ ] Panel shows: dish name (original + translation)
- [ ] Panel shows: description, ingredients, dish type
- [ ] Panel shows: vegan/vegetarian classification with icon
- [ ] Panel shows: confidence level and reasoning
- [ ] Panel is dismissable (swipe, X, tap outside)
- [ ] Panel doesn't completely cover menu

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Requirements: [REQ-F-014](../requirements/functional.md#req-f-014)

---

### US-015: Toggle Overlays [Draft]

**As a** [All users](../personas.md),
**I want to** show/hide overlay elements (translations, badges),
**so that** I control information density and avoid overload.

**Acceptance Criteria:**
- [ ] Toggle controls for: Translations, Vegan/Veggie badges, Icons
- [ ] Overlays can be shown/hidden independently
- [ ] Controls are accessible but not obtrusive
- [ ] Toggle state persists during session
- [ ] Smooth animations

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Requirements: [REQ-F-015](../requirements/functional.md#req-f-015)

---

## Epic: Multi-Page Menus

_Scan multiple pages, navigate as menu book_

### US-016: Scan Multiple Pages [Draft]

**As a** [Emma & Tom (Travelers)](../personas.md#emma-tom-adventurers),
**I want to** scan multiple menu pages (appetizers, mains, drinks),
**so that** I have the complete menu in one place.

**Acceptance Criteria:**
- [ ] "Add Page" button available after first scan
- [ ] Can scan 2-20 pages
- [ ] Each page processed independently
- [ ] Page thumbnails shown
- [ ] Page counter displayed ("Page 3 of 5")

**Related:**
- Use Case: [UC-002](../use-cases/UC-002-create-multi-page-menu-book.md)
- Requirements: [REQ-F-016](../requirements/functional.md#req-f-016)

---

### US-017: Navigate Between Pages [Draft]

**As a** [Emma & Tom (Travelers)](../personas.md#emma-tom-adventurers),
**I want to** swipe between menu pages,
**so that** I can browse the full menu like flipping physical pages.

**Acceptance Criteria:**
- [ ] Swipe left/right to change pages
- [ ] Tap thumbnail to jump to page
- [ ] Page transitions are smooth (< 0.3s)
- [ ] Current page clearly indicated
- [ ] All hotspots work on each page

**Related:**
- Use Case: [UC-002](../use-cases/UC-002-create-multi-page-menu-book.md)
- Requirements: [REQ-F-017](../requirements/functional.md#req-f-017)

---

### US-018: Reorder or Delete Pages [Draft]

**As a** [All users](../personas.md),
**I want to** reorder or delete pages in my menu book,
**so that** I can fix mistakes or get pages in correct order.

**Acceptance Criteria:**
- [ ] Drag thumbnails to reorder
- [ ] Delete individual pages
- [ ] Confirmation before deletion
- [ ] Page numbering updates automatically

**Related:**
- Use Case: [UC-002](../use-cases/UC-002-create-multi-page-menu-book.md)
- Requirements: [REQ-F-018](../requirements/functional.md#req-f-018)

---

## Epic: History & Favorites

_Save scans, mark favorites, organize by restaurant_

### US-019: Mark Dishes as Favorites [Draft]

**As a** [All users](../personas.md),
**I want to** mark dishes as favorites,
**so that** I remember what I liked for future visits.

**Acceptance Criteria:**
- [ ] Favorite icon (heart/star) in detail panel
- [ ] Tap to favorite/unfavorite
- [ ] Visual indication of favorited dishes
- [ ] Favorites persist in history

**Related:**
- Use Case: [UC-004](../use-cases/UC-004-mark-favorites-and-save-history.md)
- Requirements: [REQ-F-019](../requirements/functional.md#req-f-019)

---

### US-020: Auto-Save Menu to History [Draft]

**As a** [All users](../personas.md),
**I want to** have all my scans automatically saved,
**so that** I can access them later without manual saving.

**Acceptance Criteria:**
- [ ] All scans saved automatically
- [ ] History includes: photo, date/time, location, restaurant name
- [ ] History includes: favorited dishes
- [ ] Maximum 100 menus (oldest deleted)

**Related:**
- Use Case: [UC-004](../use-cases/UC-004-mark-favorites-and-save-history.md)
- Requirements: [REQ-F-020](../requirements/functional.md#req-f-020)

---

### US-021: GPS Restaurant Matching [Draft]

**As a** [All users](../personas.md),
**I want to** have restaurants automatically identified via GPS,
**so that** my history is organized by restaurant without manual entry.

**Acceptance Criteria:**
- [ ] GPS coordinates captured (if permission granted)
- [ ] Restaurant name fetched from Google Places
- [ ] Prompt: "Are you at [Restaurant Name]?"
- [ ] Can confirm/edit name
- [ ] Multiple scans link to same restaurant
- [ ] Works without GPS (manual naming)

**Related:**
- Use Case: [UC-004](../use-cases/UC-004-mark-favorites-and-save-history.md)
- Requirements: [REQ-F-021](../requirements/functional.md#req-f-021)

---

### US-022: Browse History [Draft]

**As a** [All users](../personas.md),
**I want to** browse my scan history sorted by date or restaurant,
**so that** I can find past menus for return visits.

**Acceptance Criteria:**
- [ ] History list sorted by date (newest first)
- [ ] Show thumbnail, restaurant name, date
- [ ] Tap to re-open interactive menu
- [ ] Group by restaurant (if multiple scans)
- [ ] Filter by: favorites, date, restaurant
- [ ] Delete individual items

**Related:**
- Use Case: [UC-004](../use-cases/UC-004-mark-favorites-and-save-history.md)
- Requirements: [REQ-F-022](../requirements/functional.md#req-f-022)

---

## Epic: Photo Quality & Guidance

_Ensure good photos, provide feedback, guide user_

### US-023: Photo Quality Detection [Draft]

**As a** [All users](../personas.md),
**I want to** be notified immediately if my photo is too blurry or dark,
**so that** I can retake it before processing fails.

**Acceptance Criteria:**
- [ ] Blur detected
- [ ] Low brightness detected
- [ ] Glare detected
- [ ] Quality check completes < 0.5 seconds
- [ ] Clear feedback message shown

**Related:**
- Use Case: [UC-005](../use-cases/UC-005-retake-poor-quality-photo.md)
- Requirements: [REQ-F-023](../requirements/functional.md#req-f-023)

---

### US-024: Actionable Quality Feedback [Draft]

**As a** [All users](../personas.md),
**I want to** receive specific guidance on fixing photo issues,
**so that** I know exactly what to do (not just "bad photo").

**Acceptance Criteria:**
- [ ] Specific messages: "Too blurry - hold steady"
- [ ] Specific messages: "Too dark - use more light"
- [ ] Specific messages: "Glare - adjust angle"
- [ ] Preview shows issue highlighted
- [ ] "Retake" button prominent
- [ ] "Use Anyway" option available

**Related:**
- Use Case: [UC-005](../use-cases/UC-005-retake-poor-quality-photo.md)
- Requirements: [REQ-F-024](../requirements/functional.md#req-f-024)

---

## Epic: Performance & UX (from Non-Functional)

_Instant feel, lazy loading, smooth experience_

### US-025: Instant Feel - < 2 Seconds [Draft]

**As a** [Marcus (Business Traveler)](../personas.md#marcus-health-professional),
**I want to** see my menu with hotspots in < 2 seconds,
**so that** I can quickly scan menus during tight lunch breaks.

**Acceptance Criteria:**
- [ ] Optimized photo displayed < 1 second
- [ ] Hotspots appear < 2 seconds
- [ ] Basic translation visible < 2 seconds
- [ ] Full classification loads in background
- [ ] Feels "instant" compared to ChatGPT

**Related:**
- Requirements: [REQ-NF-001](../requirements/non-functional.md#req-nf-001)

---

### US-026: Progressive Disclosure - No Overload [Draft]

**As a** [All users](../personas.md),
**I want to** see overview first and drill into details only when needed,
**so that** I'm not overwhelmed with information.

**Acceptance Criteria:**
- [ ] Default view: menu + subtle hotspots
- [ ] Overlays can be toggled
- [ ] Detail panel opens only on tap
- [ ] Content is scannable (not wall of text)

**Related:**
- Requirements: [REQ-NF-004](../requirements/non-functional.md#req-nf-004)

---

## Epic: Cost Optimization & Smart Caching

_CRITICAL for business model viability - maximize cache hits, minimize LLM costs_

### US-029: Avoid Re-scanning Same Menu [CRITICAL]

**As a** [All users](../personas.md),
**I want to** be notified if I'm scanning a menu I already scanned before,
**so that** I can reuse previous results instead of waiting and wasting processing costs.

**Acceptance Criteria:**
- [ ] System detects duplicate menu photo (perceptual hash)
- [ ] Prompt: "You scanned this menu 2 days ago. Use previous results?"
- [ ] If user accepts: instant retrieval (€0.00 cost)
- [ ] If user declines: proceed with new scan (menu may have changed)
- [ ] Detection completes < 0.5 seconds
- [ ] Works at same GPS location (±50m)

**Related:**
- Requirements: [REQ-F-029](../requirements/functional.md#req-f-029), [REQ-NF-013](../requirements/non-functional.md#req-nf-013)
- Persona: All users benefit from instant results

**Business Impact:**
- Prevents redundant €0.01 LLM calls
- Critical for users who revisit same restaurants on holiday

**Development Phase:** v1 (Must Have)

---

### US-030: Reuse Dish Classifications [CRITICAL]

**As a** [All users](../personas.md),
**I want to** benefit from dishes I've already classified across different menus and restaurants,
**so that** I get instant results for familiar dishes.

**Acceptance Criteria:**
- [ ] System caches dish classifications by normalized name + ingredients
- [ ] "Vegetable Tempura" at Restaurant A matches "野菜の天ぷら" at Restaurant B
- [ ] Cache hit = instant classification (€0.00 cost)
- [ ] Cache miss = classify and store for future
- [ ] Fuzzy matching handles minor text variations
- [ ] Cache persists across sessions
- [ ] Max 10,000 dishes cached (LRU eviction)

**Related:**
- Requirements: [REQ-F-030](../requirements/functional.md#req-f-030), [REQ-NF-013](../requirements/non-functional.md#req-nf-013)
- Persona: Frequent travelers benefit most (multiple Japanese restaurants)

**Business Impact:**
- Target: 70%+ cache hit rate for returning users
- 100-page holiday trip: ~€0.50 instead of €1.00 in LLM costs

**Development Phase:** v1 (Must Have)

---

### US-031: Smart Cache Hierarchy [CRITICAL]

**As a** [All users](../personas.md),
**I want to** the app to intelligently retrieve previous results at multiple levels,
**so that** I minimize processing time and costs across all scenarios.

**Acceptance Criteria:**
- [ ] L1: Exact image match → retrieve all results instantly
- [ ] L2: Similar image (different angle) → retrieve all results
- [ ] L3: Same dishes detected → retrieve per-dish results
- [ ] L4: Location + cuisine context → suggest similar dishes
- [ ] Subtle UX: "Using previous scan from 3 days ago"
- [ ] "Scan again" option always available
- [ ] Retrieval completes < 0.3 seconds
- [ ] Fallback to normal processing if retrieval fails

**Related:**
- Requirements: [REQ-F-031](../requirements/functional.md#req-f-031), [REQ-NF-013](../requirements/non-functional.md#req-nf-013)
- Persona: All users benefit from intelligent caching

**Business Impact:**
- First scan at restaurant: €0.01 cost
- Subsequent scans: €0.00 cost (cache hit)
- Essential for €8 app with €5.60 margin after App Store fee

**Development Phase:** v1 (Must Have)

---

## Epic: Future Enhancements (Bonus Features)

_Nice-to-have features for post-v1_

### US-027: Order Phrase Generation [Bonus]

**As a** [Ben (Flexible Vegan)](../personas.md#flexible-vegan-ben),
**I want to** generate phrases like "without fish sauce" in local language,
**so that** I can customize dishes when ordering.

**Acceptance Criteria:**
- [ ] Generate phrase: "Is this vegan?" in local language
- [ ] Generate phrase: "Without [ingredient]" in local language
- [ ] Phonetic pronunciation provided
- [ ] Copy to clipboard
- [ ] Display in detail panel

**Related:**
- Requirements: [REQ-F-026](../requirements/functional.md#req-f-026)

**Status:** Future Enhancement

---

### US-028: Community Shared Scans [Bonus]

**As a** [All users](../personas.md),
**I want to** reuse menus scanned by others at the same restaurant,
**so that** I get instant results without waiting for processing.

**Acceptance Criteria:**
- [ ] Detect if menu scanned recently at this location
- [ ] Prompt: "Menu scanned yesterday. Use that?"
- [ ] Cloud storage for shared menus
- [ ] Menus expire after X days

**Related:**
- Requirements: [REQ-F-027](../requirements/functional.md#req-f-027)

**Status:** Future Enhancement

---

## Notes

### Story Prioritization (MoSCoW)

**CRITICAL Must Have (v1):**
- US-029, US-030, US-031: Cost optimization & smart caching (business viability)

**Must Have (v1):**
- US-001 to US-014: Core scanning, classification, navigation
- US-016 to US-018: Multi-page menus
- US-023, US-024: Photo quality feedback
- US-025, US-026: Performance (instant UX)

**Should Have (v1 or soon after):**
- US-015: Overlay toggles
- US-019 to US-022: History and favorites

**Nice to Have (Future):**
- US-027, US-028: Bonus features

### Persona Coverage

- **Anna (Strict Vegan):** US-003, US-008, US-009, US-010, US-011 (high confidence, reasoning)
- **Ben (Flexible Vegan):** US-010, US-027 (practical, phrases)
- **Eric (Practical Vegetarian):** US-012 (visible vs. hidden meat)
- **Marcus (Business):** US-001, US-025 (speed, efficiency)
- **Emma & Tom (Travelers):** US-016, US-017, US-018 (multi-page menus)
- **All users:** US-002, US-004, US-005, US-006, US-013, US-014, US-020, US-023, US-024

### Development Phases (Suggestion)

**Phase 1: Core MVP**
- US-001, US-002, US-003, US-004 (Scanning + OCR + Symbols)
- US-005, US-006, US-007 (Translation + Dish types)
- US-008, US-009, US-010 (Classification + Confidence + Reasoning)
- US-013, US-014 (Hotspots + Detail panel)

**Phase 2: Enhanced UX**
- US-011, US-012 (Cuisine context, visible/hidden meat)
- US-015 (Overlays)
- US-023, US-024, US-025, US-026 (Quality + Performance)

**Phase 3: Multi-Page & History**
- US-016, US-017, US-018 (Multi-page)
- US-019, US-020, US-021, US-022 (Favorites + History + GPS)

**Phase 4: Future Enhancements**
- US-027, US-028 (Bonus features)
