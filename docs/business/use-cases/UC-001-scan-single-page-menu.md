# UC-001: Scan and Analyze Single-Page Menu

> **ID:** UC-001
> **Status:** Draft
> **Created:** 2025-11-15
> **Last Updated:** 2025-11-15

## Actors

- **Primary:** [Sarah the Vegan Backpacker](../personas.md#sarah-vegan-backpacker), [Marcus the Health-Conscious Professional](../personas.md#marcus-health-professional)
- **Secondary:** Any traveler needing menu translation

## Preconditions

1. User has installed VegyScan app on iOS device
2. User has granted camera permissions
3. User is in a restaurant with a physical menu
4. User has set their preferred target language in app settings

## Main Flow (Happy Path)

1. User opens VegyScan app
2. App displays camera view with scanner guide lines overlay
3. User positions camera over menu page
4. User taps "Scan" button (or automatic capture when menu detected)
5. App captures photo
6. App automatically optimizes image:
   - Straightens perspective
   - Adjusts brightness/contrast
   - Sharpens text
   - Removes shadows
7. App displays optimized menu photo in full-screen view
8. App processes menu in background:
   - Performs OCR (text extraction)
   - Recognizes symbols (🌱, V, allergen icons)
   - Bundles meta-information per menu item
   - Identifies dish boundaries and groupings
9. App displays interactive hotspots over each detected menu item (subtle turquoise overlay)
10. App shows overlay controls (toggle icons for: translations, vegan/veggie badges, symbols)
11. User sees instant visual feedback: menu looks like original but with added intelligence
12. → Use case ends successfully

## Alternative Flows

### Alt-1: Manual Capture Trigger

**Branches from:** Step 4 in Main Flow

1. User manually frames menu page
2. User taps capture button
3. → Returns to step 5 in Main Flow

### Alt-2: Multi-Language Menu

**Branches from:** Step 8 in Main Flow

1. App detects menu has multiple languages (e.g., Japanese + poor English)
2. App combines both language sources for better context
3. App generates unified translation in user's target language
4. → Returns to step 9 in Main Flow

### Alt-3: User Toggles Overlays

**Branches from:** Step 11 in Main Flow

1. User taps overlay control (e.g., "Show Translations")
2. App shows/hides translation overlays on menu items
3. User can toggle multiple overlays independently
4. → Use case continues (user can now interact with hotspots, see UC-003)

## Exception Flows

### Exc-1: Poor Photo Quality Detected

**Occurs when:** Photo is too blurry, dark, or reflective (Step 6)

1. System detects low image quality score
2. System displays feedback: "Photo quality too low. Please retake."
3. System provides tips: "Ensure good lighting and hold camera steady"
4. → Returns to step 3 (camera view)

### Exc-2: No Menu Items Detected

**Occurs when:** OCR finds no structured menu content (Step 8)

1. System cannot identify any menu items
2. System displays message: "No menu detected. Please capture a menu page."
3. User presented with option: "Retake" or "Cancel"
4. If Retake → Returns to step 3
5. If Cancel → Use case ends (failure)

### Exc-3: Network Error During Processing

**Occurs when:** LLM API call fails (Step 8)

1. System detects network/API error
2. System displays message: "Processing failed. Check connection and retry."
3. System caches photo locally
4. User can tap "Retry" button
5. → Returns to step 8
6. If retry fails after 3 attempts → Use case ends (failure)

## Postconditions

### Success
- Menu photo is optimized and displayed
- Interactive hotspots are placed over menu items
- Symbols and meta-info are recognized and bundled
- User can see overlay controls
- Menu is ready for detailed interaction (see UC-003)
- Scan is saved to local history (see UC-004)

### Failure
- Photo is not processed
- User must retake or cancel
- No data saved

## Business Rules

- **BR-001** Symbol recognition is critical and must be completed before hotspots are shown
- **BR-002** Meta-info bundling must group all components of a single dish (name, description, price, symbols, ingredients)
- **BR-003** Image optimization must preserve original menu layout and proportions
- **BR-004** Overlay controls must be accessible but not obtrusive (can be hidden)
- **BR-005** Processing must feel "instant" (< 2 seconds perceived time via lazy loading)

## Related Artifacts

- **Requirements:**
  - [REQ-F-001: Photo Capture](../requirements/functional.md#req-f-001)
  - [REQ-F-002: Image Optimization](../requirements/functional.md#req-f-002)
  - [REQ-F-003: OCR and Text Extraction](../requirements/functional.md#req-f-003)
  - [REQ-F-004: Symbol Recognition](../requirements/functional.md#req-f-004)
  - [REQ-F-005: Meta-Info Bundling](../requirements/functional.md#req-f-005)
  - [REQ-NF-001: Performance - Instant Feel](../requirements/non-functional.md#req-nf-001)
- **User Stories:** [US-001](../user-stories/stories.md#us-001), [US-002](../user-stories/stories.md#us-002)
- **Related Use Cases:**
  - [UC-003: View dish details](./UC-003-view-dish-details.md)
  - [UC-005: Retake poor quality photo](./UC-005-retake-poor-quality-photo.md)

## Notes

- Scanner guide lines should leverage iOS native document scanner APIs where possible
- Lazy loading strategy: Show optimized photo + hotspots first, process vegan/veggie classification in background
- Turquoise color for hotspots is brand guideline (to be confirmed in design phase)
- Multi-language detection may require language identification step before translation
