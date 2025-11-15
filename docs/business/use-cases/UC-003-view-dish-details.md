# UC-003: View Dish Details and Vegan/Vegetarian Classification

> **ID:** UC-003
> **Status:** Draft
> **Created:** 2025-11-15
> **Last Updated:** 2025-11-15

## Actors

- **Primary:** [Anna (Strict Vegan)](../personas.md#strict-vegan-anna), [Ben (Health-Oriented Vegan)](../personas.md#health-vegan-ben)
- **Secondary:** All users wanting detailed dish information

## Preconditions

1. User has scanned a menu (UC-001 completed)
2. Interactive hotspots are displayed over menu items
3. Background processing of dish details has completed (or is in progress via lazy loading)

## Main Flow (Happy Path)

1. User sees scanned menu with interactive hotspots
2. User taps on a hotspot over a specific dish
3. App displays detail panel (slide-up or sidebar) with following information:
   - **Dish Name** (original language + transliteration if needed)
   - **Translation** (in user's target language)
   - **Description** (what the dish is, in simple terms)
   - **Ingredients** (extracted from menu + typical ingredients for this dish type)
   - **Dish Type/Category** (e.g., "Japanese Ramen Noodle Soup", "Belgian Fried Snack")
   - **Vegan/Vegetarian Classification:**
     - Icon: ✅ Vegan / 🟢 Vegetarian / ❌ Contains Animal Products
     - Confidence level: 1-3 dots (⚫⚫⚫ = very confident, ⚫⚫◯ = moderate, ⚫◯◯ = uncertain)
     - **Reasoning:** "Typically contains fish sauce" / "Menu symbol indicates vegan" / etc.
   - **Country/Cuisine Context** (e.g., "In Belgium, fries are traditionally fried in animal fat")
   - **Possible Modifications** (if applicable: "Can request without fish sauce")
4. User reads information to make ordering decision
5. User closes detail panel by swiping down or tapping X
6. → Returns to menu view with hotspots

## Alternative Flows

### Alt-1: View Another Dish

**Branches from:** Step 4 in Main Flow

1. User wants to compare dishes
2. User taps different hotspot while detail panel is open
3. App smoothly transitions to new dish details
4. → Returns to step 3 with new dish info

### Alt-2: Symbol-Enhanced Classification

**Branches from:** Step 3 in Main Flow

1. Menu item has recognized symbol (e.g., 🌱 vegan icon)
2. App displays symbol prominently in detail panel
3. Classification shows: "✅ Vegan (confirmed by menu symbol)"
4. Confidence level is ⚫⚫⚫ (very high due to explicit symbol)
5. → Continues to step 4

### Alt-3: Uncertain Classification

**Branches from:** Step 3 in Main Flow

1. App cannot confidently determine vegan/vegetarian status
2. App displays: "⚠️ Uncertain - May contain animal products"
3. Confidence level: ⚫◯◯ (low)
4. Reasoning: "Insufficient information about preparation method. Recommend asking staff."
5. App shows suggested question in local language: "Is this dish vegan?" (see Bonus Feature)
6. → Continues to step 4

### Alt-4: Multi-Language Menu Context

**Branches from:** Step 3 in Main Flow

1. Original menu has both Japanese text + poor English description
2. App combines both sources: "Original: とんこつラーメン / Menu says: 'Pork bone soup noodle'"
3. App provides accurate translation: "Tonkotsu Ramen - Rich pork bone broth ramen"
4. Classification: "❌ Contains pork (broth made from pork bones)"
5. → Continues to step 4

## Exception Flows

### Exc-1: Details Still Loading (Lazy Loading)

**Occurs when:** User taps hotspot before background processing completes (Step 2)

1. User taps hotspot
2. App shows detail panel with loading indicator: "Analyzing dish..."
3. Basic info shown immediately (name, translation from OCR)
4. Vegan/vegetarian classification loads within 1-2 seconds
5. Panel updates in place when data arrives
6. → Continues to step 4

### Exc-2: LLM Processing Failed

**Occurs when:** Background API call failed for this specific dish (Step 3)

1. App cannot load vegan/vegetarian classification
2. App shows: "⚠️ Unable to analyze. Please retry."
3. Retry button available
4. If retry fails → Show basic OCR info only (name, OCR text)
5. → User can close panel or retry

### Exc-3: No Ingredients Detected

**Occurs when:** Menu has minimal info (just dish name, no description)

1. App shows warning: "Limited information available"
2. Classification based on dish name and cuisine context only
3. Confidence level reduced (⚫⚫◯ or ⚫◯◯)
4. Reasoning: "Based on typical preparation of this dish in [country]"
5. → Continues to step 4

## Postconditions

### Success
- User has viewed detailed dish information
- User understands vegan/vegetarian status with reasoning
- User can make informed ordering decision
- User can return to menu to view other dishes
- Interaction logged (optional: for improving classifications)

### Failure
- Detail panel shows partial info (OCR only)
- User can retry or close panel
- User may need to use alternative method (ask staff, Google search)

## Business Rules

- **BR-001** Vegan/vegetarian classification MUST include reasoning (transparency)
- **BR-002** Confidence level MUST be shown (manage user expectations)
- **BR-003** Symbol recognition overrides LLM classification (menu symbols are authoritative)
- **BR-004** Country/cuisine context MUST be considered in classification (e.g., Belgian fries)
- **BR-005** Detail panel must not obscure original menu photo entirely (preserve visual reference)
- **BR-006** Dish type recognition helps with classification accuracy (Tonkotsu = pork broth)
- **BR-007** If confidence is ⚫◯◯, app should recommend asking staff

## Related Artifacts

- **Requirements:**
  - [REQ-F-009: Dish Detail Panel](../requirements/functional.md#req-f-009)
  - [REQ-F-010: Vegan/Vegetarian Classification](../requirements/functional.md#req-f-010)
  - [REQ-F-011: Confidence Levels](../requirements/functional.md#req-f-011)
  - [REQ-F-012: Reasoning and Transparency](../requirements/functional.md#req-f-012)
  - [REQ-F-013: Dish Type Recognition](../requirements/functional.md#req-f-013)
  - [REQ-F-014: Cuisine Context Awareness](../requirements/functional.md#req-f-014)
  - [REQ-NF-003: Lazy Loading Performance](../requirements/non-functional.md#req-nf-003)
- **User Stories:** [US-004](../user-stories/stories.md#us-004), [US-005](../user-stories/stories.md#us-005)
- **Related Use Cases:**
  - [UC-001: Scan menu](./UC-001-scan-single-page-menu.md)
  - [UC-004: Mark favorites](./UC-004-mark-favorites-and-save-history.md)

## Notes

### Confidence Level Legend (to be shown in app)
- ⚫⚫⚫ Very confident (menu symbol, well-known dish, clear ingredients)
- ⚫⚫◯ Moderately confident (typical recipe known, but variations exist)
- ⚫◯◯ Uncertain (insufficient info, ambiguous description, recommend asking staff)

### Lazy Loading Strategy
Priority 1 (immediate): Basic OCR text, translation
Priority 2 (1-2s): Vegan/vegetarian classification, confidence, reasoning
Priority 3 (background): Dish type, possible modifications, context

### Detail Panel Design Considerations
- Should not cover entire menu (user may want to point at original for ordering)
- Slide-up from bottom (iOS standard) or sidebar (iPad)
- Easy to dismiss (swipe down, tap outside, X button)
- Scrollable if content is long
