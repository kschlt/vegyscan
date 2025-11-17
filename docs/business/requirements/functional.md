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
- Vision: [Strategic Scope](../vision.md#strategic-scope)

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
- Vision: [Scope - Translation to ANY language](../vision.md#strategic-scope)

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
- Persona: [Anna](../personas.md#strict-vegan-anna), [Ben](../personas.md#health-vegan-ben), [David](../personas.md#strict-vegetarian-david), [Eric](../personas.md#practical-vegetarian-eric)
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
- Persona: [Anna](../personas.md#strict-vegan-anna), [Clara](../personas.md#allergy-vegan-clara)
- Vision: [Scope - Confidence levels](../vision.md#strategic-scope)

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
- Vision: [Scope - Dish type recognition](../vision.md#strategic-scope)

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
- Vision: [Scope - Country/cuisine context](../vision.md#strategic-scope)

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
- Vision: [Scope - Overlay system](../vision.md#strategic-scope)

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
- Persona: [Emma](../personas.md#pescatarian-emma)

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
- Persona: [Anna](../personas.md#strict-vegan-anna), [Emma](../personas.md#pescatarian-emma)

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

## Cost Optimization & Smart Caching

### REQ-F-029: Menu Duplicate Detection

**Description:** System must detect when user is scanning the same menu they (or someone else at this location) scanned previously and offer to retrieve cached results instead of re-processing.

**Rationale:** CRITICAL for cost optimization. Re-scanning the same menu at a restaurant wastes LLM API costs. With target of <€0.005 per page, preventing duplicate scans is essential for business model viability.

**Priority:** Must Have (CRITICAL for cost)

**Status:** Draft

**Related:**
- REQ-NF-013: LLM Cost Optimization
- REQ-F-027: Community-Shared Menu Scans (future enhancement)
- Vision: [Success Criteria - Cost-efficient LLM usage](../vision.md#success-criteria)

**Acceptance Criteria:**
- [ ] Compute perceptual hash of captured menu photo
- [ ] Check local cache for similar hash (same device, previous scan)
- [ ] Compare with GPS location + timestamp (same restaurant, recent scan)
- [ ] If match found (>90% similarity): prompt "You scanned this menu [timeframe] ago. Use previous results?"
- [ ] If user accepts: retrieve cached translation & classification (0 LLM cost)
- [ ] If user declines: proceed with new scan (may be updated menu)
- [ ] Cache expires after 30 days (configurable)
- [ ] Detection completes within 0.5 seconds

**Implementation Notes:**
- Perceptual hashing (pHash or dHash) for image similarity
- Local SQLite database for cache storage
- GPS location stored with ±50m accuracy for privacy
- Future: cloud-based sharing (REQ-F-027) for cross-user deduplication

---

### REQ-F-030: Dish-Level Caching

**Description:** System must cache individual dish classifications at a granular level, allowing reuse even when menu layout changes or user scans different pages.

**Rationale:** Restaurants often have the same dishes across multiple locations or reprint menus with layout changes. Caching at dish level (not just full menu) maximizes cache hit rate and cost savings.

**Priority:** Must Have (CRITICAL for cost)

**Status:** Draft

**Related:**
- REQ-NF-013: LLM Cost Optimization
- REQ-F-008: Vegan/Vegetarian Classification

**Acceptance Criteria:**
- [ ] Create cache key from: dish name (normalized) + ingredients text + cuisine context
- [ ] Store: translation, classification, confidence, reasoning per dish
- [ ] Match dishes even if menu layout/formatting differs
- [ ] Normalize text for matching: lowercase, remove special chars, trim whitespace
- [ ] Use fuzzy matching (Levenshtein distance) for minor variations
- [ ] Cache hit = skip LLM call for that dish (€0.00 cost)
- [ ] Cache miss = LLM classify and store result
- [ ] Cache persists across sessions (local storage)
- [ ] Cache size limit: 10,000 dishes (configurable)
- [ ] LRU eviction when cache full

**Example:**
- User scans menu in Tokyo restaurant
- Dish: "Vegetable Tempura - 野菜の天ぷら"
- Cached: {name_en: "Vegetable Tempura", vegan: false, vegetarian: true, reasoning: "May contain egg in batter"}
- User scans same restaurant next week: cache hit, €0.00 cost
- User scans different Tokyo restaurant with same dish: cache hit, €0.00 cost

---

### REQ-F-031: Smart Result Retrieval

**Description:** System must intelligently retrieve previously computed results using image similarity, text matching, and location context to minimize redundant LLM calls.

**Rationale:** Users may accidentally scan the same page twice, or scan slightly different angles of the same menu. Smart retrieval prevents wasteful re-processing.

**Priority:** Must Have (CRITICAL for cost)

**Status:** Draft

**Related:**
- REQ-NF-013: LLM Cost Optimization
- REQ-F-029: Menu Duplicate Detection
- REQ-F-030: Dish-Level Caching

**Acceptance Criteria:**
- [ ] Multi-level cache hierarchy:
  - L1: Exact image hash match (same photo) → retrieve all results
  - L2: Perceptual hash match (similar photo) → retrieve all results
  - L3: Dish-level text match (same dishes) → retrieve per-dish results
  - L4: Location + cuisine context → suggest similar dishes
- [ ] UX for cache hits: "Using previous scan from [timeframe]" (subtle indicator)
- [ ] User can override: "Scan again" option always available
- [ ] Track cache hit rate as success metric (target: >70% for returning users)
- [ ] Smart retrieval completes within 0.3 seconds
- [ ] Failed retrieval falls back to normal LLM processing

**Business Impact:**
- First scan at restaurant: €0.01 LLM cost (full processing)
- Second scan (same menu): €0.00 LLM cost (cache hit)
- 100-page holiday trip with 50% revisits to same restaurants: €0.50 instead of €1.00

---

## Photo Upload & iOS Integration

### REQ-F-032: Upload from Photo Library

**Description:** System must allow users to upload existing photos from their device's photo library instead of (or in addition to) taking new photos with the camera.

**Rationale:** Users may have already taken menu photos, or want to scan menus from other sources (Google Maps, restaurant websites, friends' photos). This enables pre-visit planning and reduces friction.

**Priority:** Must Have

**Status:** Draft

**Related:**
- REQ-F-001: Photo Capture (camera-based)
- REQ-F-016: Multi-Page Scanning
- REQ-F-033: Add Page to Existing Menu
- REQ-F-035: Smart Location Tagging (location from EXIF, not current GPS)
- Persona: All personas benefit from upload flexibility

**Acceptance Criteria:**
- [ ] "Upload Photo" option available on main screen (alongside "Scan Menu")
- [ ] Opens iOS Photo Picker (native system UI)
- [ ] User can select single photo
- [ ] User can select multiple photos at once (for multi-page menus)
- [ ] Uploaded photos processed identically to camera-captured photos (same optimization, OCR, classification pipeline)
- [ ] Multi-photo selection creates multi-page menu automatically
- [ ] Uploaded photos saved to history same as camera scans
- [ ] Clear UI distinction between "Scan Menu" (camera) and "Upload Photo" (library)
- [ ] **Location tagging:** Extract GPS from photo EXIF data (if available), do NOT use current GPS location (see REQ-F-035)

**Use Cases:**
- User took menu photo earlier, now wants to analyze it
- User found menu photo on Google Maps before visiting restaurant
- User received menu photo from friend
- User wants to prepare before restaurant visit (pre-trip planning)

**Business Impact:**
- Expands use case from "at restaurant" to "planning where to eat"
- Enables pre-visit decision making (huge value add)
- Reduces friction (no need to be at restaurant to use app)

---

### REQ-F-033: Add Page to Existing Menu

**Description:** System must provide clear UX for adding additional pages to an existing menu (either by camera or upload).

**Rationale:** Multi-page menus are common. Users need clear distinction between "start new menu scan" vs "add page to current menu" to avoid confusion.

**Priority:** Must Have

**Status:** Draft

**Related:**
- REQ-F-016: Multi-Page Scanning
- REQ-F-032: Upload from Photo Library
- Use Case: [UC-002](../use-cases/UC-002-create-multi-page-menu-book.md)

**Acceptance Criteria:**
- [ ] When viewing a menu, "Add Page" button clearly visible
- [ ] "Add Page" offers two options:
  - "Take Photo" (opens camera)
  - "Upload Photo" (opens photo library)
- [ ] Main screen has separate "Scan New Menu" action (creates new menu)
- [ ] UI clearly distinguishes "new menu" vs "add to existing"
- [ ] Confirmation before adding to existing menu (prevents accidental additions)
- [ ] Can reorder pages after adding (drag & drop)
- [ ] Can delete pages from multi-page menu
- [ ] Page numbers displayed (Page 1 of 3, etc.)

**UX Flow Examples:**
1. **Add via camera**: View Menu → "Add Page" → "Take Photo" → Camera opens → Capture → Added to menu
2. **Add via upload**: View Menu → "Add Page" → "Upload Photo" → Photo Picker → Select → Added to menu
3. **Start new menu**: Main Screen → "Scan New Menu" → Choose camera or upload

---

### REQ-F-034: iOS Share Extension

**Description:** System must integrate with iOS Share Sheet, allowing users to share photos from ANY app (Photos, Safari, Google Maps, Messages, etc.) directly to VegyScan for instant menu analysis.

**Rationale:** CRITICAL for pre-visit planning and seamless integration. User can browse restaurant photos in Google Maps, tap Share, select VegyScan, and instantly analyze the menu before visiting. This is a killer feature for trip planning.

**Priority:** Should Have (high value, but requires iOS extension)

**Status:** Draft

**Related:**
- REQ-F-032: Upload from Photo Library
- REQ-F-029: Menu Duplicate Detection (shared photos may be duplicates)
- Vision: [Open Strategic Questions](../vision.md#open-strategic-questions)

**Acceptance Criteria:**
- [ ] VegyScan appears in iOS Share Sheet for image types
- [ ] Share Extension accepts single photo
- [ ] Share Extension accepts multiple photos (creates multi-page menu)
- [ ] Tapping "VegyScan" in Share Sheet:
  - Opens VegyScan app
  - Creates new menu from shared photo(s)
  - Starts processing immediately
  - Shows processing progress
- [ ] Works from Photos app
- [ ] Works from Safari (long-press image → Share)
- [ ] Works from Google Maps (restaurant menu photos)
- [ ] Works from Messages/WhatsApp (friend shares menu photo)
- [ ] Shared photo saved to history (with source metadata if available)
- [ ] If duplicate detected (REQ-F-029), prompt "You scanned this menu before. Use previous results?"

**Use Cases:**

**Use Case 1: Google Maps Pre-Visit Planning**
1. User browsing restaurants in Google Maps for trip
2. Opens restaurant page, views photos
3. Finds menu photo
4. Taps Share icon
5. Selects "VegyScan" from Share Sheet
6. VegyScan opens, processes menu
7. User sees vegan/vegetarian options BEFORE visiting restaurant
8. Makes informed decision about which restaurant to visit

**Use Case 2: Friend Shares Menu Photo**
1. Friend sends menu photo via WhatsApp: "Is this restaurant vegan-friendly?"
2. User taps photo, taps Share
3. Selects "VegyScan"
4. App analyzes menu, shows vegan options
5. User responds: "Yes, 3 vegan dishes available!"

**Use Case 3: Website Menu Photo**
1. User finds restaurant website with menu photo
2. Long-presses menu image in Safari
3. Taps Share → VegyScan
4. Instantly analyzes menu from website photo

**Business Impact:**
- **Expands use case dramatically:** From "at restaurant" to "planning trip"
- **Pre-visit decision making:** Users can research restaurants before visiting
- **Viral potential:** Easy sharing between friends ("Check this menu out!")
- **Competitive advantage:** Google Translate and ChatGPT don't have this integration
- **Increases engagement:** Users interact with app BEFORE trip (not just during)

**Technical Notes:**
- Requires iOS Share Extension (separate target in Xcode)
- Extension receives photo URL, passes to main app via App Groups
- Main app processes photo same as upload/camera
- Extension should be lightweight (hand off to main app quickly)
- **Location tagging:** No location data for shared photos (see REQ-F-035)

---

### REQ-F-035: Smart Location Tagging Based on Photo Source

**Description:** System must intelligently determine location data for menu scans based on photo source, using EXIF metadata when available and current GPS only when appropriate.

**Rationale:** CRITICAL for accurate history and restaurant matching. User browsing Google Maps at home should NOT have home GPS tagged to restaurant menu. EXIF data from photo is more reliable than current location for uploaded/shared photos.

**Priority:** Must Have

**Status:** Draft

**Related:**
- REQ-F-019: GPS-Based History Matching
- REQ-F-020: Local History Storage
- REQ-F-032: Upload from Photo Library
- REQ-F-034: iOS Share Extension

**Location Tagging Strategy (Priority Order):**

**1. In-App Camera Capture (REQ-F-001):**
- ✅ **Prefer:** EXIF GPS data from captured photo (if iOS saves it automatically)
- ✅ **Fallback:** Current GPS location at time of capture
- **Rationale:** User is at restaurant when taking photo - current GPS is accurate

**2. Upload from Photo Library (REQ-F-032):**
- ✅ **Prefer:** EXIF GPS data from photo (user may have taken photo earlier at restaurant)
- ❌ **Never:** Current GPS location (user likely browsing from home/elsewhere)
- ✅ **Fallback:** No location data (menu saved without GPS tag)
- **Rationale:** Photo may have been taken at restaurant earlier - EXIF is reliable, current GPS is NOT

**3. Share from Other Apps (REQ-F-034):**
- ✅ **Prefer:** EXIF GPS data from shared photo (if available)
- ❌ **Never:** Current GPS location (user browsing from home/office/elsewhere)
- ✅ **Fallback:** No location data
- **Rationale:** User sharing from Google Maps/Safari is likely planning remotely - current GPS is NOT accurate

**Acceptance Criteria:**
- [ ] Extract EXIF GPS data from all photos (camera, upload, share)
- [ ] **Camera capture:** Use EXIF GPS if available, else use current GPS location
- [ ] **Upload/Share:** Use EXIF GPS ONLY, never use current GPS location
- [ ] If no EXIF GPS and source is upload/share: Save menu without location tag
- [ ] Menus without location tags:
  - Not matched by GPS-based history (REQ-F-019)
  - Can still be found in "All Scans" history
  - User can manually add location later (optional future feature)
- [ ] Location source displayed in menu metadata: "Location: From photo" vs "Location: Current GPS" vs "No location"
- [ ] Privacy: Request location permission only for camera capture, not for upload/share

**Use Cases:**

**Use Case 1: Camera Capture at Restaurant**
1. User at restaurant, takes photo with in-app camera
2. System checks photo EXIF GPS → not available (iOS limitation)
3. System uses current GPS location
4. Menu tagged with restaurant location ✅

**Use Case 2: Upload Photo Taken Earlier**
1. User at home, uploads photo taken yesterday at restaurant
2. System extracts EXIF GPS from photo → finds restaurant location
3. System uses EXIF GPS, ignores current location (home)
4. Menu correctly tagged with restaurant location ✅

**Use Case 3: Share from Google Maps (No EXIF)**
1. User at home, browsing Google Maps, shares menu photo
2. System checks EXIF GPS → not available (Google Maps screenshot)
3. System does NOT use current GPS (would be home address)
4. Menu saved without location tag
5. Still searchable in history, just not GPS-matched ✅

**Use Case 4: Friend Shares Menu via WhatsApp**
1. User receives menu photo from friend via WhatsApp
2. Photo has EXIF GPS from friend's location (different city)
3. System uses EXIF GPS (friend's restaurant location)
4. Menu tagged with restaurant where friend was ✅

**Privacy Considerations:**
- Location permission only requested for camera capture
- Upload/share features work WITHOUT location permission
- User can use app even if location permission denied (just no GPS tagging)

**Technical Notes:**
- Use iOS ImageIO framework to extract EXIF GPS data
- EXIF GPS fields: GPSLatitude, GPSLongitude, GPSAltitude
- Check photo metadata before falling back to current location
- Current location via Core Location (only for camera captures)

**Business Impact:**
- Prevents false location tagging (home GPS for Google Maps shares)
- Accurate restaurant history and GPS matching
- Privacy-friendly (no location permission needed for upload/share)
- Better user experience (menus correctly categorized)

---

### REQ-F-036: First-Time User Onboarding

**Description:** System must provide optional onboarding experience for first-time users to introduce core functionality.

**Rationale:** While app should be intuitive without tutorial (REQ-NF-006), brief onboarding reduces friction and sets expectations for new users. Optional design respects power users who want to skip.

**Priority:** Should Have

**Status:** Draft

**Acceptance Criteria:**
- [ ] Onboarding triggered only on first app launch
- [ ] 3-screen tutorial (skippable at any time):
  - Screen 1: "Scan any menu in any language" with camera icon
  - Screen 2: "See vegan/vegetarian options instantly" with classification demo
  - Screen 3: "All data stays on your device" with privacy message
- [ ] "Skip" button visible on all screens
- [ ] "Get Started" button on final screen
- [ ] Never shown again after completion or skip
- [ ] Optional: "Show Tutorial Again" in settings

**Related:**
- REQ-NF-006: Intuitive First-Time Use
- Use Case: UC-008 (to be created)

---

### REQ-F-037: User Settings & Preferences

**Description:** System must provide settings screen for user preferences and app configuration.

**Rationale:** Users need control over app behavior, data retention, and privacy settings. Required for GDPR compliance (user control over data).

**Priority:** Must Have

**Status:** Draft

**Acceptance Criteria:**
- [ ] Settings accessible from main menu
- [ ] **Privacy Settings:**
  - Camera permission status and link to iOS Settings
  - Photos permission status and link to iOS Settings
  - Location permission status and link to iOS Settings
- [ ] **Data Management:**
  - Clear all scan history (with confirmation)
  - Clear cache (with confirmation)
  - Data retention period: 30/60/90 days (default: 90)
  - Export all data (JSON format) - REQ-F-038
- [ ] **Preferences (Optional - only if behavior changes):**
  - Dietary preference: Vegan/Vegetarian/Pescatarian/All (default: All)
  - Default UI language (if i18n implemented)
- [ ] **About:**
  - App version number
  - Privacy policy link
  - Terms of service link
  - Open source licenses (if any)
  - Support/contact email

**Related:**
- REQ-NF-022: GDPR Compliance
- REQ-F-038: Data Export
- REQ-F-039: Delete Scan History
- Use Case: UC-011 (to be created)

---

### REQ-F-038: Data Export (GDPR Requirement)

**Description:** System must allow users to export all stored data in machine-readable format.

**Rationale:** GDPR Article 20 (Data Portability) requires users can obtain their data in structured, commonly used format. Legal requirement for EU market.

**Priority:** Must Have (Legal Requirement)

**Status:** Draft

**Acceptance Criteria:**
- [ ] "Export Data" button in settings
- [ ] Exports all user data as JSON file
- [ ] Data included:
  - All scanned menus (metadata: date, location if available, restaurant name)
  - Favorited dishes (dish name, restaurant, date favorited)
  - User preferences (dietary preference, settings)
- [ ] Photos NOT included in export (too large, stored locally already)
- [ ] User can share exported JSON via iOS Share Sheet (email, cloud storage, etc.)
- [ ] Export includes timestamp and app version for reference
- [ ] Export format documented in privacy policy

**Example Export Format:**
```json
{
  "export_date": "2025-11-16T14:30:00Z",
  "app_version": "1.0.0",
  "menus": [
    {
      "id": "uuid",
      "date_scanned": "2025-11-15T19:00:00Z",
      "restaurant_name": "Trattoria Roma",
      "location": {"lat": 41.9028, "lng": 12.4964},
      "pages": 2,
      "favorites": ["Pasta Pomodoro", "Insalata Mista"]
    }
  ],
  "preferences": {
    "dietary_preference": "vegan",
    "data_retention_days": 90
  }
}
```

**Related:**
- REQ-NF-022: GDPR Compliance (Data Portability)
- REQ-F-037: User Settings

---

### REQ-F-039: Delete Scan History

**Description:** System must allow users to delete individual menus or clear all scan history.

**Rationale:** GDPR Article 17 (Right to Erasure) requires users can delete their data. Also practical need for users to manage storage and privacy.

**Priority:** Must Have (Legal Requirement)

**Status:** Draft

**Acceptance Criteria:**
- [ ] Delete individual menu: Long-press menu in history → Delete option
- [ ] Confirmation dialog: "Delete this menu? This cannot be undone."
- [ ] Deleted menu removed from local storage (SQLite + photo files)
- [ ] Clear all history: Option in settings
- [ ] Confirmation dialog: "Delete all scanned menus? This cannot be undone."
- [ ] "Clear All" removes all menus, favorites, and cache
- [ ] Preferences retained (dietary preference, settings)
- [ ] User can still use app after clearing all data

**Related:**
- REQ-NF-022: GDPR Compliance (Right to Erasure)
- REQ-F-020: Local History Storage
- REQ-F-037: User Settings
- Use Case: UC-010 (to be created)

---

### REQ-F-040: View Scan History

**Description:** System must provide browsable history of all scanned menus with search and filter capabilities.

**Rationale:** Users want to revisit previously scanned menus to find restaurants, remember dishes, or show friends. Core value of saving scans.

**Priority:** Must Have

**Status:** Draft

**Acceptance Criteria:**
- [ ] History screen accessible from main menu
- [ ] Display all scanned menus in chronological order (newest first)
- [ ] Each menu shows:
  - Thumbnail of first page
  - Restaurant name (if GPS matched or user-named)
  - Date scanned
  - Number of pages (if multi-page)
  - Location (city/country if GPS available)
- [ ] Tap menu to reopen in full interactive view
- [ ] Search by restaurant name or dish name
- [ ] Filter by:
  - Date range (Last week, Last month, Last 3 months, All)
  - Location (if GPS data available)
  - Favorites only
- [ ] Empty state if no history: "No scanned menus yet. Scan your first menu!"
- [ ] Pull to refresh (if needed)

**Related:**
- REQ-F-020: Local History Storage
- REQ-F-019: GPS-Based History Matching
- REQ-F-021: Favorite Dishes
- Use Case: UC-009 (to be created)

---

### REQ-F-041: Auto-Delete Old Scans (Data Retention)

**Description:** System must automatically delete scans older than user-configured retention period to comply with GDPR data minimization principle.

**Rationale:** GDPR requires data not kept longer than necessary. User control over retention period balances usability with privacy compliance.

**Priority:** Must Have (Legal Requirement)

**Status:** Draft

**Acceptance Criteria:**
- [ ] Default retention period: 90 days
- [ ] User can configure in settings: 30/60/90/180 days or Never
- [ ] Auto-delete runs on app launch
- [ ] Menus older than retention period automatically deleted
- [ ] Favorited dishes NOT auto-deleted (user explicitly saved)
- [ ] User notified if menus auto-deleted: "X old menus deleted to respect your privacy settings"
- [ ] User can change retention period at any time
- [ ] Changing retention period applies to future, not retroactive

**Related:**
- REQ-NF-022: GDPR Compliance (Data Minimization)
- REQ-F-037: User Settings
- REQ-F-039: Delete Scan History

---

## Bonus Features (Future Enhancement)

### REQ-F-026: Order Phrase Generation

**Description:** System should generate helpful phrases in local language for ordering or customizing dishes.

**Rationale:** Users want to communicate dietary needs to staff (e.g., "without fish sauce" in Thai).

**Priority:** Nice to Have (Bonus)

**Status:** Draft (Future)

**Related:**
- Persona: [Ben](../personas.md#health-vegan-ben)

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

**Priority:** ~~Nice to Have (Bonus)~~ → **OUT OF V1 SCOPE** (Future v2+)

**Status:** Deferred (Requires cloud architecture)

**v1 Decision:** Community features OUT of scope for v1
- Requires cloud storage, backend infrastructure, moderation
- Adds architectural complexity (authentication, sync, privacy controls)
- v1 uses local-only storage (no cloud, no accounts)
- **Critical:** v1 architecture must be extensible (not rebuildable) for future cloud features

**Related:**
- Vision: [What We're NOT Building](../vision.md#what-were-not-building-strategic-boundaries)
- Vision: [Strategic Decisions](../vision.md#strategic-decisions-and-constraints)

**Acceptance Criteria (Future v2+):**
- [ ] Detect if menu was recently scanned at this GPS location
- [ ] Prompt: "Menu scanned here yesterday. Use that?"
- [ ] Cloud storage for shared menus (privacy-aware)
- [ ] Menus expire after X days (configurable)

---

### REQ-F-028: User Feedback on Classification

**Description:** System should allow users to report incorrect vegan/vegetarian classifications.

**Rationale:** Crowdsourced corrections improve accuracy over time.

**Priority:** ~~Nice to Have (Bonus)~~ → **OUT OF V1 SCOPE** (Future v2+)

**Status:** Deferred (Requires cloud architecture)

**v1 Decision:** User feedback/community features OUT of scope for v1
- Requires cloud storage for feedback data
- Requires backend infrastructure to aggregate feedback
- Adds complexity (moderation, abuse prevention, consensus algorithms)
- v1 focuses on accurate classification from LLM, no community input
- **Critical:** v1 architecture must be extensible for future feedback features

**Related:**
- Vision: [What We're NOT Building](../vision.md#what-were-not-building-strategic-boundaries)
- Vision: [Strategic Decisions](../vision.md#strategic-decisions-and-constraints)

**Acceptance Criteria (Future v2+):**
- [ ] "Report Incorrect" button in detail panel
- [ ] User can specify: "This is vegan" / "This is not vegan"
- [ ] Feedback stored and used to improve model
- [ ] Community consensus affects future classifications

---

## Cultural Intelligence & Context (NEW - Based on User Research)

### REQ-F-042: Cultural Context Database

**Description:** System must maintain comprehensive database of country/cuisine-specific dietary information including hidden ingredients, cooking methods, local concepts, and traditional vegan dishes.

**Rationale:** CRITICAL DIFFERENTIATOR. User research shows travelers repeatedly encounter hidden ingredients specific to cultures (dashi in Japan, ghee in India, lard in Latin America). Generic translators lack this context. This is the #1 requested feature.

**Priority:** Must Have (CRITICAL - Killer Feature)

**Status:** Draft

**Related:**
- User Research: [Pain Point #1 - Hidden Ingredients](../user-research-report.md#1-hidden-non-obvious-ingredients)
- User Research: [Unmet Need #3 - Cultural Context](../user-research-report.md#3-cultural-context--hidden-ingredient-database)
- REQ-F-012: Cuisine Context Awareness

**Database Structure (per country/cuisine):**

```
Country: Japan
├─ Language: Japanese
├─ Vegan Awareness Level: Low (3/10)
├─ Local Terminology:
│  ├─ "Vegan" → "ビーガン" (not widely understood)
│  ├─ Recommendation: Use full explanation
│  └─ Alternative: "精進料理" (Shojin Ryori - Buddhist vegan)
├─ Common Hidden Ingredients:
│  ├─ だし (Dashi) - fish stock in EVERYTHING
│  ├─ かつお節 (Katsuobushi) - bonito flakes
│  └─ みりん (Mirin) - may contain fish
├─ Watch-Out Dishes:
│  ├─ Miso Soup → usually made with dashi
│  ├─ Ramen → broth almost always pork/chicken/fish
│  └─ Tempura batter → may contain egg
├─ Safe Local Dishes:
│  ├─ Edamame (枝豆) - 95% vegan
│  ├─ Natto (納豆) - fermented soybeans
│  └─ Onigiri with ume - check for bonito
└─ Cultural Notes:
   └─ Modifications rarely accepted in traditional restaurants
```

**Acceptance Criteria:**
- [ ] Database covers top 20 travel destinations for vegans
- [ ] Each country includes:
  - Local terminology for vegan/vegetarian
  - Vegan awareness level (1-10 scale)
  - Common hidden ingredients (min 5)
  - Watch-out dishes (min 5)
  - Safe local dishes (min 5)
  - Cultural eating customs relevant to vegans
- [ ] Database for each major cuisine type (Thai, Indian, Japanese, Italian, etc.)
- [ ] Regional variations (Northern vs Southern Thai)
- [ ] Downloadable as offline packs (by region)
- [ ] User can access via "Cultural Tips" panel
- [ ] Context automatically applied during menu analysis
- [ ] Database updatable without app update (JSON config)

**User Experience:**

When user scans Japanese menu:
```
💡 You're in Japan

⚠️ Watch out for:
• Dashi (fish stock) in most soups
• Bonito flakes on rice dishes
• Egg in tempura batter

🌱 Look for these local dishes:
• Edamame - steamed soybeans
• Natto - fermented soybeans
• Vegetable tempura (ask about batter)

💬 Useful phrase:
"Dashi wa haitte imasuka?"
(Does this have fish stock?)

💡 Tip: "Vegan" is not widely understood.
Explain what you don't eat specifically.
```

**Business Impact:**
- Solves most painful problem (hidden ingredients)
- No competitor has this
- Massive barrier to entry (takes months to build)
- Network effects (community contributions later)

---

### REQ-F-043: Smart Vegan Passport

**Description:** System must provide customizable, culturally-adaptive vegan passport that generates appropriate explanations based on detected country/language.

**Rationale:** Users currently carry physical Vegan Passport or create translation cards. Digital version can be smarter, adapting to local culture (use "strict vegetarian" in India, full explanation in Japan).

**Priority:** Must Have

**Status:** Draft

**Related:**
- User Research: [Unmet Need #4 - Communication Tools](../user-research-report.md#4-seamless-communication-tools)
- REQ-F-042: Cultural Context Database

**Acceptance Criteria:**
- [ ] Settings panel: "What I DON'T eat"
  - [ ] Customizable checkboxes: Meat, Fish, Seafood, Eggs, Dairy, Honey
  - [ ] Custom additions (for Jain: Onion, Garlic, Root vegetables)
- [ ] Visual icons for each restriction (🥩, 🐟, 🥚, 🥛, 🍯)
- [ ] Auto-translation to detected language (from menu scan)
- [ ] Culturally-adapted terminology:
  - [ ] India: "I follow strict vegetarian (शुद्ध शाकाहारी)"
  - [ ] Japan: Full explanation (not just "vegan")
  - [ ] Thailand: Option for "เจ" (Jay - Buddhist vegan)
  - [ ] Germany: "Vegan" (widely understood)
- [ ] Generated message includes:
  - [ ] Polite greeting in local language
  - [ ] List of restrictions with icons
  - [ ] "Can you help me find something I can eat?"
- [ ] "Show to Waiter" full-screen mode:
  - [ ] Large, clear text
  - [ ] Both local language and English
  - [ ] Icons for visual clarity
  - [ ] Thank you message
- [ ] Quick profiles: [Vegan] [Vegetarian] [Custom]
- [ ] One-tap switch between profiles
- [ ] Auto-populates from scanned menu (if app detects oyster sauce, adds "Fish Sauce" to passport)

**UI Example:**
```
┌─────────────────────────────┐
│   VEGAN PASSPORT 🌱         │
├─────────────────────────────┤
│ What I DON'T eat:           │
│ ☑️ Meat     (🥩 icon)        │
│ ☑️ Fish     (🐟 icon)        │
│ ☑️ Eggs     (🥚 icon)        │
│ ☑️ Dairy    (🥛 icon)        │
│ ☑️ Honey    (🍯 icon)        │
│ ☐ Onion/Garlic (custom)     │
├─────────────────────────────┤
│ Generated for Thailand:      │
│                              │
│ 🇹🇭 "ดิฉัน/ผมทานอาหารเจ     │
│  ไม่ทานเนื้อสัตว์ ไข่ นม    │
│  และปลา คุณช่วยแนะนำอาหาร   │
│  ที่ฉันทานได้ไหมคะ/ครับ"    │
│                              │
│ 🇬🇧 "I eat vegan food.      │
│  I don't eat meat, fish,    │
│  eggs, or dairy. Can you    │
│  help me find something?"   │
│                              │
│ [Show to Waiter] button     │
└─────────────────────────────┘
```

---

### REQ-F-044: Dish Modification Question Generator

**Description:** System must generate contextual, dish-specific modification questions in local language when dish contains animal products that can potentially be removed/substituted.

**Rationale:** Generic "make it vegan" is not actionable. Users need specific questions: "Can you make Pad Thai without egg and fish sauce, using soy sauce instead?" This is much more effective.

**Priority:** Must Have

**Status:** Draft

**Related:**
- User Research: [Communication Pain Point](../user-research-report.md#at-restaurant-discovery)

**Acceptance Criteria:**
- [ ] When dish classified as non-vegan but modifiable:
  - [ ] Identify specific animal ingredients (egg, fish sauce, butter)
  - [ ] Generate removal question in local language
  - [ ] Suggest vegan alternatives if applicable
- [ ] Question format:
  ```
  Can you make [Dish Name] without [Ingredient 1],
  [Ingredient 2], and [Ingredient 3]?
  [Optional: Use [Alternative] instead.]
  ```
- [ ] Display in both English and local language
- [ ] Polite phrasing appropriate to culture
- [ ] "Show to Waiter" full-screen mode
- [ ] "Copy Text" button (for use in other apps)
- [ ] "Add to Order Basket" button
- [ ] Examples per dish analyzed

**Example Output:**

For Pad Thai in Thailand:
```
💬 ASK THE WAITER

🇬🇧 English:
"Can you make the Pad Thai without egg
and fish sauce? Please use soy sauce instead."

🇹🇭 Thai:
"ทำผัดไทยไม่ใส่ไข่และน้ำปลา
ใช้ซีอิ๊วแทนได้ไหมครับ/ค่ะ"

[Show to Waiter]  [Copy Text]  [Add to Order]
```

For Green Curry in Thailand:
```
💬 ASK THE WAITER

🇬🇧 English:
"Can you make the Green Curry without fish sauce,
shrimp paste, and oyster sauce?"

🇹🇭 Thai:
"ทำแกงเขียวหวานไม่ใส่น้ำปลา กะปิ
และน้ำมันหอยได้ไหมครับ/ค่ะ"

⚠️ Note: Curry paste usually contains shrimp paste.
Some restaurants can't modify this.

[Show to Waiter]  [Copy Text]  [Add to Order]
```

---

### REQ-F-045: Visual Order Basket

**Description:** System must allow users to build a visual order in local language showing all dishes and modifications, formatted like a restaurant order slip.

**Rationale:** Reduces back-and-forth with waiter. User shows one screen with complete order including all modifications clearly formatted.

**Priority:** Must Have

**Status:** Draft

**Related:**
- User Research: [Communication Tools Need](../user-research-report.md#4-seamless-communication-tools)
- REQ-F-044: Modification Question Generator

**Acceptance Criteria:**
- [ ] "Add to Order Basket" button on each dish detail
- [ ] Order basket accessible from main menu
- [ ] Shows all selected dishes with:
  - [ ] Dish name in local language
  - [ ] Menu item number (if available)
  - [ ] Modifications (❌ symbols for removals, ✅ for additions)
  - [ ] Both local language and English
- [ ] "Show Order to Waiter" mode:
  - [ ] Full-screen view
  - [ ] Large, clear text
  - [ ] Restaurant slip styling
  - [ ] Numbered list
  - [ ] Thank you message at bottom
- [ ] Edit order (remove items, adjust modifications)
- [ ] Clear all
- [ ] Save order for this restaurant (reorder next visit)

**Visual Design:**
```
┏━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃    📋 MY ORDER           ┃
┃    คำสั่งของฉัน          ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                          ┃
┃  ① #24 ผัดไทย             ┃
┃     (Pad Thai)           ┃
┃     🚫 ไม่ใส่ไข่          ┃
┃        (No egg)          ┃
┃     🚫 ไม่ใส่น้ำปลา       ┃
┃        (No fish sauce)   ┃
┃     ✅ ใส่ซีอิ๊ว          ┃
┃        (Use soy sauce)   ┃
┃                          ┃
┃  ② #15 ส้มตำ             ┃
┃     (Papaya Salad)       ┃
┃     🚫 ไม่ใส่กุ้งแห้ง     ┃
┃        (No dried shrimp) ┃
┃     🚫 ไม่ใส่น้ำปลา       ┃
┃        (No fish sauce)   ┃
┃                          ┃
┃  ③ ข้าวเหนียวมะม่วง      ┃
┃     (Mango Sticky Rice)  ┃
┃     ✅ เจ (Vegan)         ┃
┃                          ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃   ขอบคุณมากครับ/ค่ะ 🙏  ┃
┃   (Thank you very much)  ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

---

### REQ-F-046: Digitalized Menu View with Smart Filtering

**Description:** System must provide text-only view of menu (extracted from scan) with filtering capabilities and cross-reference to original photo.

**Rationale:** User research shows some users prefer clean text list for quick scanning, while others want to point at original menu. Provide both with seamless switching.

**Priority:** Must Have

**Status:** Draft

**Related:**
- User Research: [Multi-Tool Workflow Pattern](../user-research-report.md#pattern-1-the-multi-tool-workflow)

**Acceptance Criteria:**
- [ ] Toggle between [Photo View] and [Text View]
- [ ] Photo View: Original menu with hotspots (existing)
- [ ] Text View: Clean digitalized text extraction
  - [ ] All menu items listed
  - [ ] Preserves menu item numbers (e.g., "#24 Pad Thai")
  - [ ] Shows price (if detected)
  - [ ] Vegan/Vegetarian badge on each item
  - [ ] Confidence level indicator
- [ ] Filter controls in Text View:
  - [ ] [All Items] [Vegan] [Vegetarian] [Can Be Modified]
  - [ ] Filter updates list in real-time
- [ ] Tap item in Text View:
  - [ ] Opens detail panel (existing)
  - [ ] OR "View in Photo" button → switches to Photo View with item highlighted/zoomed
- [ ] Highlight/zoom feature in Photo View:
  - [ ] Centers on selected item
  - [ ] Spotlight effect (dimming background slightly)
  - [ ] Makes pointing to waiter easy
- [ ] Switching between views maintains scroll position/selection
- [ ] Smooth transitions (<300ms)

**User Flow Example:**
1. User scans menu
2. App shows Photo View (default)
3. User taps [Text View] toggle
4. Sees filtered list: [Vegan] shows 8 items
5. Selects "Mango Sticky Rice"
6. Taps "View in Photo"
7. Photo View zooms to that menu item
8. User points phone at waiter: "This one, number 12"

---

### REQ-F-047: Prioritized Safe Sorting

**Description:** System must provide intelligent sorting of menu items by safety/suitability level for user's dietary preference.

**Rationale:** User research shows travelers mentally categorize dishes as safe/risky. App should match this decision-making process.

**Priority:** Must Have

**Status:** Draft

**Related:**
- User Research: [Decision Making Patterns](../user-research-report.md#decision-making-evaluation)

**Sorting Options:**
```
[Sort by: Safest First ▼]

Other options:
- By Menu Order (default)
- Local Dishes First
- Your Favorites First
- By Confidence Level
```

**Safest First Logic:**
```
🟢 SAFEST OPTIONS (95%+ confidence vegan)
├─ Fresh Fruit Plate
├─ Steamed Jasmine Rice
└─ Mango Sticky Rice
   "Usually vegan, confirm coconut milk"

🟡 LIKELY VEGAN (70-94% confidence or modifiable)
├─ Pad Thai ⚙️
   "Usually has egg & fish sauce → Ask to remove"
├─ Spring Rolls
   "Check wrapper (may contain egg)"

🟠 MIGHT BE VEGAN (50-69% confidence)
├─ Green Curry
   "Curry paste often has shrimp → Confirm"

🔴 CONTAINS ANIMAL PRODUCTS
├─ Tom Yum Soup (shrimp, fish sauce)
├─ Massaman Curry (usually chicken)
```

**Acceptance Criteria:**
- [ ] Sorting available in Text View
- [ ] Visual grouping by safety level
- [ ] Color coding (green/yellow/orange/red)
- [ ] Can collapse/expand sections
- [ ] Badge shows reasoning for classification
- [ ] Empty sections hidden (if no items in category)

---

### REQ-F-048: Local Dish Highlighting

**Description:** System must identify and badge menu items that are local/traditional dishes to encourage cultural food experiences.

**Rationale:** User research shows major pain point is missing out on local cuisine (eating fries everywhere). Help users find local vegan options.

**Priority:** Should Have

**Status:** Draft

**Related:**
- User Research: [Pain Point #5 - Limited Options](../user-research-report.md#5-limitedboringfood-options)
- REQ-F-042: Cultural Context Database

**Acceptance Criteria:**
- [ ] Detect local dishes from Cultural Context Database
- [ ] Badge local dishes: 🌍 LOCAL SPECIALTY
- [ ] In detail panel, show:
  - [ ] "This is a traditional [Country] dish"
  - [ ] Brief description
  - [ ] Typical ingredients
  - [ ] Vegan status / How to veganize
- [ ] Sorting option: "Local Vegan First"
  - [ ] Priority: Local + Vegan > Local + Modifiable > International Vegan
- [ ] Filtering option: [Show Only Local Dishes]
- [ ] Highlight local dishes visually in menu

**Example:**
```
┌─────────────────────────────┐
│ 🟢 Mango Sticky Rice         │
│    🌍 THAI LOCAL SPECIALTY   │
│    ข้าวเหนียวมะม่วง          │
│                              │
│    Traditional Thai dessert  │
│    Coconut milk, mango, rice │
│    ✓ Usually vegan           │
│    ⚠️ Confirm coconut milk   │
│       has no dairy added     │
│                              │
│ Confidence: ⚫⚫⚫ High        │
└─────────────────────────────┘
```

---

### REQ-F-049: Context-Aware Favorites

**Description:** System must save favorite dishes by context (country + cuisine type) and intelligently surface them when scanning similar menus.

**Rationale:** Users want to remember good dishes and easily reorder them. Context-aware = "You enjoyed Pad Thai at 3 Thai restaurants - it's here too!"

**Priority:** Should Have

**Status:** Draft

**Related:**
- User Research: [Behavioral Patterns](../user-research-report.md#behavioral-patterns)
- REQ-F-019: Mark Dishes as Favorites

**Acceptance Criteria:**
- [ ] Save favorites with context:
  - [ ] Dish name
  - [ ] Cuisine type (Thai, Indian, Japanese, etc.)
  - [ ] Country scanned in
  - [ ] Restaurant name
  - [ ] Date saved
  - [ ] User notes (optional)
  - [ ] Modifications used
- [ ] Match favorites across menus:
  - [ ] Same dish at different restaurant
  - [ ] Same cuisine in different country (Thai restaurant in Japan)
- [ ] Show favorites in scan results:
  ```
  🎉 Great news! Found 8 vegetarian dishes

  💚 2 of them are already your favorites:
  • Pad Thai (no egg) - You loved this at 3 places
  • Mango Sticky Rice - Your go-to dessert

  [View All Options →]
  ```
- [ ] "Your Favorites" filter in menu view
- [ ] Export favorites list (for sharing/backup)
- [ ] Suggest similar dishes: "You like Pad Thai, try Pad See Ew?"

---

### REQ-F-050: Smart Search Shortcuts (Google Maps Integration)

**Description:** System must provide pre-configured search shortcuts for finding restaurants via Google Maps using local terminology.

**Rationale:** Users struggle with what to search for in foreign languages. App should offer ready-made searches.

**Priority:** Should Have

**Status:** Draft

**Related:**
- User Research: [Pre-Trip Planning Pain](../user-research-report.md#pre-trip-preparation)

**Acceptance Criteria:**
- [ ] "Find Restaurants" panel in app
- [ ] Shows context-aware shortcuts based on detected country:

For Thailand:
```
┌─────────────────────────────┐
│ 🔍 FIND RESTAURANTS          │
├─────────────────────────────┤
│ Quick searches near you:     │
│                              │
│ [Search: "ร้านอาหารเจ"] 🔍   │
│ (Vegan Buddhist restaurants) │
│                              │
│ [Search: "อาหารเจ"] 🔍        │
│ (Vegan food)                 │
│                              │
│ [Search: "vegetarian"] 🔍    │
│ (English - tourist areas)    │
├─────────────────────────────┤
│ Local vegan dishes:          │
│                              │
│ 🥭 Mango Sticky Rice         │
│    [Find on Google Maps] 🔍  │
│                              │
│ 🍜 Guay Teow Pak             │
│    (Veg Noodle Soup)         │
│    [Find on Google Maps] 🔍  │
└─────────────────────────────┘
```

- [ ] Tapping search button opens Google Maps with pre-filled search
- [ ] Uses user's current location
- [ ] Searches in appropriate language for region
- [ ] Returns to VegyScan after (deep linking)
- [ ] Database of search terms per country (in Cultural Context DB)

---

### REQ-F-051: Restaurant Planning & Map View

**Description:** System must provide map view of all saved restaurants with analyzed menus, enabling trip planning and revisits.

**Rationale:** Users want to organize researched restaurants spatially and quickly navigate to known-safe options.

**Priority:** Should Have

**Status:** Draft

**Related:**
- User Research: [Pre-Trip Planning](../user-research-report.md#pre-trip-preparation)
- REQ-F-020: Auto-Save Menu to History

**Acceptance Criteria:**
- [ ] Map view showing all saved restaurant locations
- [ ] Pin colors indicate status:
  - [ ] 🟢 Green: Verified vegan options
  - [ ] 🟡 Yellow: Vegetarian options available
  - [ ] 🔵 Blue: Menu scanned, analysis available
  - [ ] 📷 Gray: Menu photo saved, not analyzed yet
- [ ] Tap pin to see restaurant quick info:
  - [ ] Restaurant name
  - [ ] Number of vegan dishes found
  - [ ] User notes
  - [ ] Distance from current location
  - [ ] Last visited
  - [ ] Preview of favorite dishes
- [ ] List view (alternative to map):
  - [ ] Sorted by distance or last visited
  - [ ] Filter by: Has vegan options, Has favorites, Visited, Not visited
- [ ] Quick actions:
  - [ ] Navigate (opens Apple Maps)
  - [ ] View menu (opens analyzed menu)
  - [ ] Add notes
  - [ ] Mark as visited
- [ ] Offline maps (cached map tiles for saved area)
- [ ] Export list (share with travel companions)

**Example List View:**
```
┌─────────────────────────────┐
│      📍 MY SAVED SPOTS       │
├─────────────────────────────┤
│ 🟢 Cafe de Nimman            │
│    ✓ 3 vegan dishes found    │
│    💚 Pad Thai (favorited)   │
│    📝 "Great Khao Soi!"      │
│    📍 0.5 km away            │
│    [Navigate] [View Menu]    │
│                              │
│ 🟡 Indian Palace             │
│    ✓ 8 vegetarian options    │
│    ⚠️ Ask for oil not ghee   │
│    📍 1.2 km away            │
│    [Navigate] [View Menu]    │
└─────────────────────────────┘
```

---

### REQ-F-052: Celebratory Messaging & Positive UX

**Description:** System must use encouraging, celebratory language to reduce anxiety and create positive emotional experiences.

**Rationale:** User research shows food causes significant anxiety. Positive messaging provides emotional relief and joy.

**Priority:** Must Have (UX Philosophy)

**Status:** Draft

**Related:**
- User Research: [Emotional Journey](../user-research-report.md#emotional-journey)
- All user-facing messages

**Messaging Principles:**
- ✅ Encouraging, supportive friend tone
- ✅ Celebrate wins ("Great news!")
- ✅ Provide actionable guidance, not just warnings
- ❌ Never judgmental or preachy
- ❌ Never panic-inducing

**Example Messages:**

**Good Results:**
```
🎉 Great news!

Found 8 vegetarian dishes on this menu!

💚 2 of them are already your favorites:
• Pad Thai (modified)
• Mango Sticky Rice

[View All Options →]
```

**Modest Results:**
```
Found 3 dishes that can be made vegan with modifications.

I'll show you exactly what to ask for. 💬

[View Options →]
```

**Poor Results:**
```
❌ BAD: "No vegan options detected. ⚠️"

✅ GOOD:
"No clear vegan options on this menu yet.

Here are some things to try:
• Ask about [suggested dishes from cultural DB]
• Use your Vegan Passport to explain your needs
• Check nearby restaurants [link to map]

You've got this! 💪"
```

**Warnings:**
```
❌ BAD: "⚠️ WARNING: Contains meat ⚠️"

✅ GOOD:
"This dish typically includes fish sauce.

Would you like to see how to ask for a vegan version? →"
```

**Local Dish Found:**
```
🌟 Awesome! This is a local specialty and it's vegan!

Mango Sticky Rice is a traditional Thai dessert.
You're getting an authentic taste of Thailand! 🥭
```

**Acceptance Criteria:**
- [ ] All user-facing messages reviewed for tone
- [ ] Icons used appropriately (🎉, 💚, 🌟, 💬, 💡)
- [ ] Warnings provide solutions, not just problems
- [ ] Celebrate local dish discoveries
- [ ] Acknowledge when things are difficult
- [ ] Provide encouragement
- [ ] No fear-mongering or anxiety-inducing language

---

## Notes

**Total Functional Requirements: 52** (REQ-F-001 to REQ-F-052, including 3 deferred REQ-F-026 to REQ-F-028)

**Feature Prioritization:**
- **CRITICAL Must Have:**
  - Cost optimization (REQ-F-029, REQ-F-030, REQ-F-031) - business model viability
  - Legal compliance (REQ-F-038, REQ-F-039, REQ-F-041) - GDPR requirements
  - Core scanning, classification, navigation (REQ-F-001 to REQ-F-015)
- **Must Have:**
  - Photo upload, smart location tagging (REQ-F-032, REQ-F-033, REQ-F-035)
  - User data management (REQ-F-037, REQ-F-040) - settings and history
- **Should Have:**
  - iOS Share Extension (REQ-F-034) - killer feature for pre-visit planning
  - Onboarding (REQ-F-036) - improved first-time experience
  - History, favorites, quality feedback - enhance usability
- **Nice to Have:**
  - Community features (OUT of v1), phrase generation, user feedback - future enhancements

**Persona-Driven Requirements:**
- Anna/Clara drive high confidence requirements
- David drives vegetarian distinction requirements
- Eric drives nuanced "visible vs. hidden meat" requirements
- Emma drives pescatarian classification requirements
- All personas benefit from photo upload and sharing features

**Cost-Driven Requirements (CRITICAL):**
- REQ-F-029: Menu duplicate detection (prevent re-scans)
- REQ-F-030: Dish-level caching (maximize reuse)
- REQ-F-031: Smart result retrieval (multi-level cache)
- Target: <€0.005 per page, 70%+ cache hit rate for returning users

**iOS Integration Features (NEW):**
- REQ-F-032: Upload from Photo Library (Must Have)
- REQ-F-033: Add Page to Existing Menu (Must Have)
- REQ-F-034: iOS Share Extension (Should Have - killer feature for pre-visit planning)
- REQ-F-035: Smart Location Tagging (Must Have - EXIF GPS vs. current GPS based on source)

**Strategic Value of Share Extension (REQ-F-034):**
- Expands use case from "at restaurant" to "planning trip"
- Enables Google Maps integration (view menu photo → share to VegyScan → analyze before visiting)
- Viral potential (friends sharing menu photos)
- Competitive advantage (Google Translate/ChatGPT don't have this)
- Increases engagement (users interact with app BEFORE trip)

**Technical Dependencies:**
- OCR: iOS Vision Framework or Google Cloud Vision API
- Translation: Google Translate API or similar
- LLM: GPT-4 Vision, Claude, or similar for classification
- GPS: iOS Core Location
- Symbol Recognition: Custom trained model or GPT-4 Vision
- Image Hashing: pHash or dHash for duplicate detection
- Cache Storage: SQLite or Core Data for local persistence
- Photo Library Access: iOS PhotoKit (for upload)
- Share Extension: iOS Share Extension target (for inter-app sharing)
- App Groups: For communication between Share Extension and main app
