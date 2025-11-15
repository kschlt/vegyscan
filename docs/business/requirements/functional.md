# Functional Requirements

> **Last Updated:** 2025-11-15

_This file is the Single Source of Truth for all functional requirements._

---

## Photo Capture & Image Processing

### REQ-F-001: Photo Capture with Camera Interface

**Description:** System must provide camera interface for capturing menu photos with real-time guide lines overlay.

**Rationale:** Users need intuitive way to photograph menus. Guide lines help ensure proper alignment and quality.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Use Case: [UC-005](../use-cases/UC-005-retake-poor-quality-photo.md)
- Persona: [All personas](../personas.md)

**Acceptance Criteria:**
- [ ] Camera view opens immediately when user starts scan
- [ ] Guide lines overlay shows document edges (iOS VisionKit style)
- [ ] Manual capture button available
- [ ] Auto-capture when menu is detected and aligned (optional)
- [ ] Guide box turns green when alignment is good

---

### REQ-F-002: Image Optimization

**Description:** System must automatically optimize captured menu photos by straightening perspective, adjusting brightness/contrast, and sharpening text.

**Rationale:** Poor photo quality leads to OCR errors. Automatic optimization ensures consistent quality without user intervention.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Vision: [Success Criteria](../vision.md#success-criteria)

**Acceptance Criteria:**
- [ ] Perspective correction (straighten skewed menu)
- [ ] Brightness/contrast adjustment (make text readable)
- [ ] Shadow removal (eliminate uneven lighting)
- [ ] Text sharpening (enhance OCR accuracy)
- [ ] Original menu layout and proportions preserved
- [ ] Optimization completes within 1 second

---

### REQ-F-003: OCR and Text Extraction

**Description:** System must extract all text from menu photo using OCR, recognizing multiple languages and character sets.

**Rationale:** Core requirement for translation and analysis. Must handle any language (Japanese, Korean, Thai, Arabic, Latin scripts, etc.).

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Vision: [Scope - Translation](../vision.md#in-scope)

**Acceptance Criteria:**
- [ ] Extract text from any language/script
- [ ] Maintain spatial relationship of text (which texts are grouped)
- [ ] Handle mixed-language menus (e.g., Japanese + English)
- [ ] Detect text orientation and rotation
- [ ] Achieve >90% text extraction accuracy

---

### REQ-F-004: Symbol Recognition (CRITICAL)

**Description:** System must recognize and interpret dietary symbols on menu (🌱 vegan, 🟢 vegetarian, allergen icons, etc.).

**Rationale:** Symbols are authoritative source of dietary information. Users trust menu symbols over AI classification.

**Priority:** Must Have (CRITICAL)

**Status:** Draft

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Persona: [Anna](../personas.md#strict-vegan-anna), [David](../personas.md#strict-vegetarian-david)
- Vision: [Success Criteria - Symbol Recognition >95%](../vision.md#success-criteria)

**Acceptance Criteria:**
- [ ] Detect common vegan symbols (🌱, V, VG, etc.)
- [ ] Detect common vegetarian symbols (🟢, VEG, etc.)
- [ ] Detect allergen icons (nuts, gluten, dairy, etc.)
- [ ] Associate symbols with correct menu item
- [ ] Symbol detection >95% accuracy
- [ ] Symbol recognition overrides LLM classification

---

### REQ-F-005: Meta-Information Bundling

**Description:** System must group all information belonging to a single menu item (name, description, price, symbols, ingredients) into cohesive bundle.

**Rationale:** Menus have scattered information. Bundling ensures context is preserved for accurate classification.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Vision: [Success Criteria - Meta-info bundling](../vision.md#success-criteria)

**Acceptance Criteria:**
- [ ] Identify menu item boundaries (where one item ends, another begins)
- [ ] Group name, description, price for each item
- [ ] Associate symbols with correct item
- [ ] Link ingredients list to item (if separate)
- [ ] Handle multi-column and complex layouts
- [ ] Achieve >90% correct bundling

---

## Translation & Language

### REQ-F-006: Multi-Language Translation

**Description:** System must translate menu text from any source language to user's selected target language.

**Rationale:** Core value proposition. Users need to understand menus in their native language.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Vision: [Scope - Translation to ANY language](../vision.md#in-scope)

**Acceptance Criteria:**
- [ ] Support ANY language pair (not limited to specific languages)
- [ ] User can set preferred target language in settings
- [ ] Translate dish names
- [ ] Translate descriptions
- [ ] Translate ingredient lists
- [ ] Handle mixed-language menus (combine sources for better context)

---

### REQ-F-007: User Language Selection

**Description:** System must allow user to select and save their preferred target language for translations.

**Rationale:** Users need consistent translation language across all scans.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Persona: [All personas](../personas.md)

**Acceptance Criteria:**
- [ ] Language selection in app settings
- [ ] Support major world languages
- [ ] Default to device language
- [ ] Persist user choice across sessions
- [ ] Change language affects all future scans

---

## Vegan/Vegetarian Classification

### REQ-F-008: Vegan/Vegetarian Classification

**Description:** System must classify each menu item as vegan, vegetarian, pescatarian-friendly, or contains meat/animal products.

**Rationale:** Core value proposition for target users. Enables confident ordering.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Persona: [Anna](../personas.md#strict-vegan-anna), [Ben](../personas.md#flexible-vegan-ben), [David](../personas.md#strict-vegetarian-david), [Eric](../personas.md#practical-vegetarian-eric)
- Vision: [Goals #1, #4](../vision.md#goals)

**Acceptance Criteria:**
- [ ] Classify as: Vegan / Vegetarian / Pescatarian-OK / Contains Meat
- [ ] Consider menu symbols (highest authority)
- [ ] Analyze dish name and ingredients
- [ ] Apply cuisine context (e.g., Dashi in Japanese cuisine)
- [ ] Identify hidden animal products (broths, sauces, frying methods)
- [ ] Distinguish visible meat vs. meat in broth/sauce (for Eric persona)

---

### REQ-F-009: Classification Confidence Levels

**Description:** System must provide confidence level (1-3 scale) for each vegan/vegetarian classification.

**Rationale:** Manage user expectations. High-strictness personas (Anna, David) need high confidence to trust results.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Persona: [Anna](../personas.md#strict-vegan-anna), [Clara](../personas.md#vegan-allergies-clara)
- Vision: [Scope - Confidence levels](../vision.md#in-scope)

**Acceptance Criteria:**
- [ ] Three confidence levels: ⚫⚫⚫ (high), ⚫⚫◯ (moderate), ⚫◯◯ (low)
- [ ] High confidence (⚫⚫⚫): Menu symbol present OR well-known dish
- [ ] Moderate confidence (⚫⚫◯): Typical recipe known, but variations exist
- [ ] Low confidence (⚫◯◯): Insufficient info, recommend asking staff
- [ ] Display confidence level with icon/visual indicator
- [ ] Provide legend explaining confidence levels

---

### REQ-F-010: Classification Reasoning

**Description:** System must provide transparent reasoning for vegan/vegetarian classification.

**Rationale:** Users need to understand WHY something is/isn't vegan. Builds trust and enables informed decisions.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Persona: [All vegan/vegetarian personas](../personas.md)
- Vision: [Goals #4 - Transparent reasoning](../vision.md#goals)

**Acceptance Criteria:**
- [ ] Explain WHY dish is vegan/not vegan
- [ ] Identify specific animal products ("contains fish sauce", "pork bone broth")
- [ ] Reference cuisine context ("Belgian fries traditionally fried in animal fat")
- [ ] Explain uncertainty ("ingredients not clearly listed")
- [ ] Reasoning displayed in detail panel
- [ ] Concise (1-2 sentences max)

---

### REQ-F-011: Dish Type Recognition

**Description:** System must identify dish type/category (e.g., "Japanese Ramen", "Belgian Fried Snack", "Thai Curry").

**Rationale:** Helps classification accuracy. Tonkotsu = pork broth, Frikandel = meat snack. Provides user context.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Vision: [Scope - Dish type recognition](../vision.md#in-scope)

**Acceptance Criteria:**
- [ ] Recognize common international dish types
- [ ] Use dish type for classification context
- [ ] Display dish type in detail panel
- [ ] Handle regional variations (Tonkotsu vs. Shoyu Ramen)
- [ ] Provide brief dish explanation ("Rich pork bone broth ramen")

---

### REQ-F-012: Cuisine Context Awareness

**Description:** System must apply country/cuisine-specific knowledge when classifying dishes (e.g., Dashi in Japan, animal fat frying in Belgium).

**Rationale:** Local standards vary. Belgian fries may be vegan or not. Japanese miso soup may contain Dashi (fish stock).

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Persona: [Anna](../personas.md#strict-vegan-anna), [David](../personas.md#strict-vegetarian-david)
- Vision: [Scope - Country/cuisine context](../vision.md#in-scope)

**Acceptance Criteria:**
- [ ] Detect cuisine type from menu
- [ ] Apply cuisine-specific rules (Dashi in Japanese cuisine)
- [ ] Warn about regional cooking methods (Belgian fries)
- [ ] Consider traditional ingredients (fish sauce in Thai food)
- [ ] Display context in reasoning ("In Belgium, fries are often fried in animal fat")

---

## Interactive UI & Navigation

### REQ-F-013: Interactive Hotspots

**Description:** System must overlay interactive hotspots on each detected menu item in optimized photo.

**Rationale:** Preserves original menu as navigation center. User can tap to explore details while maintaining visual context.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Vision: [Goals #2 - Preserve visual context](../vision.md#goals)

**Acceptance Criteria:**
- [ ] Place hotspot overlay on each menu item
- [ ] Hotspots are tappable/clickable
- [ ] Visual style: subtle, turquoise/brand color
- [ ] Hotspots don't obscure original text
- [ ] Accurate positioning (overlay correct item)
- [ ] Tap opens detail panel for that item

---

### REQ-F-014: Dish Detail Panel

**Description:** System must display detailed information panel when user taps menu item hotspot.

**Rationale:** Users need dish details (translation, ingredients, classification) to make ordering decisions.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)
- Persona: [All personas](../personas.md)

**Acceptance Criteria:**
- [ ] Panel displays: dish name (original + translation)
- [ ] Panel displays: description, ingredients
- [ ] Panel displays: dish type/category
- [ ] Panel displays: vegan/vegetarian classification with icon
- [ ] Panel displays: confidence level
- [ ] Panel displays: reasoning
- [ ] Panel displays: cuisine context (if relevant)
- [ ] Panel displays: possible modifications (if applicable)
- [ ] Panel is dismissable (swipe down, X button, tap outside)
- [ ] Panel doesn't completely obscure menu (user can still point at original)

---

### REQ-F-015: Overlay System (Show/Hide)

**Description:** System must allow users to toggle visibility of overlay elements (translations, badges, icons).

**Rationale:** Avoid information overload. Users can progressively disclose information as needed.

**Priority:** Should Have

**Status:** Draft

**Related:**
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)
- Vision: [Scope - Overlay system](../vision.md#in-scope)

**Acceptance Criteria:**
- [ ] Toggle controls for: Translations, Vegan/Veggie badges, Allergen icons
- [ ] Overlays can be shown/hidden independently
- [ ] Controls are accessible but not obtrusive
- [ ] Toggle state persists during session
- [ ] Smooth animation when showing/hiding

---

## Multi-Page Menu Book

### REQ-F-016: Multi-Page Scanning

**Description:** System must allow users to scan multiple menu pages and create unified menu book.

**Rationale:** Many menus have multiple pages (appetizers, mains, drinks, desserts). Users need complete view.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-002](../use-cases/UC-002-create-multi-page-menu-book.md)
- Persona: [Emma & Tom](../personas.md#emma-tom-adventurers)

**Acceptance Criteria:**
- [ ] "Add Page" button available after first scan
- [ ] User can scan 2-20 pages
- [ ] Each page processed independently
- [ ] Page thumbnails shown for navigation
- [ ] Page counter displays (e.g., "Page 3 of 5")

---

### REQ-F-017: Page Navigation

**Description:** System must allow users to navigate between scanned menu pages via swipe or thumbnail selection.

**Rationale:** Users need to browse full menu easily, similar to physical menu flipping.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-002](../use-cases/UC-002-create-multi-page-menu-book.md)

**Acceptance Criteria:**
- [ ] Swipe left/right to change pages
- [ ] Tap page thumbnail to jump to page
- [ ] Page transitions are smooth (< 0.3s)
- [ ] Current page is clearly indicated
- [ ] All hotspots/overlays work on each page independently

---

### REQ-F-018: Page Reordering and Deletion

**Description:** System must allow users to reorder or delete pages in menu book.

**Rationale:** Users may scan pages out of order or make mistakes. Need editing capability.

**Priority:** Should Have

**Status:** Draft

**Related:**
- Use Case: [UC-002](../use-cases/UC-002-create-multi-page-menu-book.md)

**Acceptance Criteria:**
- [ ] Drag thumbnails to reorder pages
- [ ] Delete individual pages
- [ ] Confirmation prompt before deletion
- [ ] Page numbering updates automatically

---

## Favorites & History

### REQ-F-019: Mark Dishes as Favorites

**Description:** System must allow users to mark individual dishes as favorites.

**Rationale:** Users want to remember dishes they liked for potential reordering or future visits.

**Priority:** Should Have

**Status:** Draft

**Related:**
- Use Case: [UC-004](../use-cases/UC-004-mark-favorites-and-save-history.md)
- Persona: [Sarah](../personas.md#sarah-vegan-backpacker), [Emma & Tom](../personas.md#emma-tom-adventurers)

**Acceptance Criteria:**
- [ ] Favorite icon (heart/star) in dish detail panel
- [ ] Tap to favorite/unfavorite
- [ ] Visual indication of favorited dishes (filled icon)
- [ ] Favorites linked to menu scan
- [ ] Favorites persist in history

---

### REQ-F-020: Auto-Save Menu to History

**Description:** System must automatically save all menu scans to local history.

**Rationale:** Users should not need to manually save. Automatic history enables easy retrieval.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-004](../use-cases/UC-004-mark-favorites-and-save-history.md)

**Acceptance Criteria:**
- [ ] All scans saved automatically (no "Save" button needed)
- [ ] History includes: menu photo(s), scan date/time, location (if available)
- [ ] History includes: restaurant name (auto-detected or manual)
- [ ] History includes: all favorited dishes
- [ ] Maximum 100 menus in history (configurable)
- [ ] Oldest scans auto-deleted when limit reached

---

### REQ-F-021: GPS Restaurant Matching

**Description:** System must use GPS location to auto-detect and match restaurant for menu scans.

**Rationale:** Users want to organize history by restaurant. GPS enables automatic restaurant identification.

**Priority:** Should Have

**Status:** Draft

**Related:**
- Use Case: [UC-004](../use-cases/UC-004-mark-favorites-and-save-history.md)

**Acceptance Criteria:**
- [ ] Request GPS permission (optional)
- [ ] Capture GPS coordinates with scan
- [ ] Query Google Places API for restaurant name
- [ ] Prompt user: "Are you at [Restaurant Name]?"
- [ ] Allow user to confirm/edit restaurant name
- [ ] Link multiple scans to same restaurant (within ~50m radius)
- [ ] Work without GPS (manual restaurant naming)

---

### REQ-F-022: History Management

**Description:** System must provide browsable history of all scanned menus with search and filtering.

**Rationale:** Users need to find past menus easily, especially for return visits.

**Priority:** Should Have

**Status:** Draft

**Related:**
- Use Case: [UC-004](../use-cases/UC-004-mark-favorites-and-save-history.md)

**Acceptance Criteria:**
- [ ] History list sorted by date (newest first)
- [ ] Show menu thumbnail, restaurant name, date
- [ ] Tap to re-open interactive menu view
- [ ] Group by restaurant (if multiple scans at same place)
- [ ] Filter by: favorites, date range, restaurant
- [ ] Delete individual history items

---

## Photo Quality & Feedback

### REQ-F-023: Photo Quality Detection

**Description:** System must automatically assess photo quality and detect common issues (blur, darkness, glare).

**Rationale:** Poor photos lead to OCR failures. Proactive feedback prevents frustration.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-005](../use-cases/UC-005-retake-poor-quality-photo.md)

**Acceptance Criteria:**
- [ ] Detect blur (motion blur, out of focus)
- [ ] Detect low brightness (too dark)
- [ ] Detect overexposure (too bright, washed out)
- [ ] Detect glare/reflections
- [ ] Detect poor text readability (OCR confidence check)
- [ ] Detect extreme perspective skew
- [ ] Quality check completes within 0.5 seconds

---

### REQ-F-024: Quality Feedback Messages

**Description:** System must provide clear, actionable feedback when photo quality is insufficient.

**Rationale:** Generic "bad quality" is not helpful. Users need specific guidance to fix issues.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Use Case: [UC-005](../use-cases/UC-005-retake-poor-quality-photo.md)

**Acceptance Criteria:**
- [ ] Specific messages: "Too blurry - hold camera steady"
- [ ] Specific messages: "Too dark - use more light or flash"
- [ ] Specific messages: "Glare detected - adjust angle"
- [ ] Show preview with issue highlighted
- [ ] Provide actionable tips with icons
- [ ] "Retake" button prominent
- [ ] "Use Anyway" option available (user override)

---

### REQ-F-025: Scanner Guide Lines

**Description:** System must display real-time guide lines during photo capture to help user align menu properly.

**Rationale:** Proactive guidance prevents quality issues. iOS VisionKit provides built-in document scanner features.

**Priority:** Should Have

**Status:** Draft

**Related:**
- Use Case: [UC-005](../use-cases/UC-005-retake-poor-quality-photo.md)

**Acceptance Criteria:**
- [ ] Guide box overlay on camera view
- [ ] Auto-detect menu edges
- [ ] Guide box green when aligned properly
- [ ] Guide box yellow/red when misaligned
- [ ] Visual feedback for distance (too close/far)
- [ ] Haptic feedback when aligned (iPhone vibration)

---

## Bonus Features (Future Enhancement)

### REQ-F-026: Order Phrase Generation

**Description:** System should generate helpful phrases in local language for ordering or customizing dishes.

**Rationale:** Users want to communicate dietary needs to staff (e.g., "without fish sauce" in Thai).

**Priority:** Nice to Have (Bonus)

**Status:** Draft (Future)

**Related:**
- Persona: [Ben](../personas.md#flexible-vegan-ben)
- Vision: [Bonus Features](../vision.md#bonus-features-future-enhancement)

**Acceptance Criteria:**
- [ ] Generate phrase: "Is this vegan?" in local language
- [ ] Generate phrase: "Without [ingredient]" in local language
- [ ] Provide phonetic pronunciation
- [ ] Copy phrase to clipboard
- [ ] Display in dish detail panel

---

### REQ-F-027: Community-Shared Menu Scans

**Description:** System should allow users to share scanned menus within a restaurant location, enabling reuse of previous scans.

**Rationale:** If someone scanned a menu yesterday, others can benefit. Reduces processing time and cost.

**Priority:** Nice to Have (Bonus)

**Status:** Draft (Future)

**Related:**
- Vision: [Bonus Features](../vision.md#bonus-features-future-enhancement)

**Acceptance Criteria:**
- [ ] Detect if menu was recently scanned at this GPS location
- [ ] Prompt: "Menu scanned here yesterday. Use that?"
- [ ] Cloud storage for shared menus (privacy-aware)
- [ ] Menus expire after X days (configurable)

---

### REQ-F-028: User Feedback on Classification

**Description:** System should allow users to report incorrect vegan/vegetarian classifications.

**Rationale:** Crowdsourced corrections improve accuracy over time.

**Priority:** Nice to Have (Bonus)

**Status:** Draft (Future)

**Related:**
- Vision: [Bonus Features](../vision.md#bonus-features-future-enhancement)

**Acceptance Criteria:**
- [ ] "Report Incorrect" button in detail panel
- [ ] User can specify: "This is vegan" / "This is not vegan"
- [ ] Feedback stored and used to improve model
- [ ] Community consensus affects future classifications

---

## Notes

**Feature Prioritization:**
- **Must Have:** Core scanning, classification, and navigation features for v1
- **Should Have:** History, favorites, quality feedback - enhance usability
- **Nice to Have:** Community features, phrase generation - future enhancements

**Persona-Driven Requirements:**
- Anna/Clara/Grace drive high confidence requirements
- David drives vegetarian distinction requirements
- Eric drives nuanced "visible vs. hidden meat" requirements
- Emma drives pescatarian classification requirements

**Technical Dependencies:**
- OCR: iOS Vision Framework or Google Cloud Vision API
- Translation: Google Translate API or similar
- LLM: GPT-4 Vision, Claude, or similar for classification
- GPS: iOS Core Location
- Symbol Recognition: Custom trained model or GPT-4 Vision
