# UC-007: Share Menu Photo from Other App (iOS Share Extension)

> **ID:** UC-007
> **Status:** Draft
> **Created:** 2025-11-15
> **Last Updated:** 2025-11-15

## Actors

- **Primary:** All personas - especially users planning restaurant visits before traveling
- **Secondary:** Users receiving menu photos from friends

## Preconditions

1. User has VegyScan app installed on iOS device
2. User is in another app (Photos, Safari, Google Maps, Messages, WhatsApp, etc.)
3. User viewing a menu photo in that app
4. VegyScan iOS Share Extension is registered (appears in Share Sheet)

## Main Flow (Happy Path) - Google Maps Pre-Visit Planning

1. User browsing restaurants in Google Maps for upcoming trip
2. User opens restaurant page, taps "Photos" tab
3. User finds menu photo among restaurant photos
4. User taps menu photo to view full-screen
5. User taps Share icon (iOS share button)
6. iOS Share Sheet appears with app options
7. User scrolls and selects "VegyScan"
8. iOS Share Extension activates:
   - Extension receives photo data
   - Extension passes photo to main VegyScan app via App Groups
   - Main app launches (or comes to foreground)
9. VegyScan app opens with processing screen: "Analyzing menu..."
10. System extracts EXIF GPS from shared photo (see REQ-F-035)
    - If EXIF GPS found → tag menu with that location
    - If no EXIF GPS (Google Maps screenshot) → **no location tag** (NOT current GPS)
11. System processes photo:
    - Image optimization
    - OCR (on-device)
    - Symbol recognition
    - Sends OCR text to LLM for classification
12. System displays processed menu in interactive view
13. System saves to history with source metadata ("Shared from [app name]")
14. User sees vegan/vegetarian options BEFORE visiting restaurant
15. User makes informed decision: "Yes, this restaurant has 3 vegan dishes!"
16. → Use case ends successfully

## Alternative Flows

### Alt-1: Share from Photos App

**Branches from:** Step 4 in Main Flow

1. User in Photos app viewing menu photo (taken earlier or received from friend)
2. User taps Share button
3. User selects "VegyScan" from Share Sheet
4. → Returns to step 8 in Main Flow

### Alt-2: Share from Safari (Restaurant Website)

**Branches from:** Step 4 in Main Flow

1. User browsing restaurant website in Safari
2. User long-presses menu image on webpage
3. Context menu appears with "Share Image"
4. User taps "Share Image"
5. User selects "VegyScan" from Share Sheet
6. → Returns to step 8 in Main Flow

### Alt-3: Share from Messages/WhatsApp (Friend Shares Menu)

**Branches from:** Step 4 in Main Flow

1. Friend sends menu photo via Messages: "Is this restaurant vegan-friendly?"
2. User taps photo to view full-screen
3. User taps Share button
4. User selects "VegyScan" from Share Sheet
5. System processes menu
6. User replies: "Yes! 3 vegan options available: [dish names]"
7. → Returns to step 8 in Main Flow

### Alt-4: Share Multiple Photos (Multi-Page Menu)

**Branches from:** Step 7 in Main Flow

1. User in Photos app, selects multiple menu photos
2. User taps Share button
3. User selects "VegyScan"
4. Extension receives multiple photos
5. Main app opens, creates multi-page menu automatically
6. Page numbers displayed (Page 1 of 4, etc.)
7. → Returns to step 10 in Main Flow

### Alt-5: Duplicate Menu Detection (Already Scanned)

**Branches from:** Step 11 in Main Flow

1. System processes photo, computes perceptual hash
2. System finds matching hash in cache (REQ-F-029)
3. System displays prompt: "You scanned this menu 2 days ago. Use previous results?"
4. Options: "Use Previous" / "Scan Again"
5. If "Use Previous" → Retrieve cached translation/classification (€0.00 cost)
6. If "Scan Again" → Continue with new scan (menu may have changed)
7. → Returns to step 12 OR retrieves cached results

## Exception Flows

### Exc-1: VegyScan Not Appearing in Share Sheet

**Occurs when:** User doesn't see VegyScan in Share Sheet (Step 7)

**Troubleshooting (documented in app help, not runtime error):**
1. VegyScan Share Extension not registered (app not installed properly)
2. OR user needs to scroll in Share Sheet to find VegyScan
3. OR iOS cached Share Sheet doesn't show newly installed apps (restart device)

**User action:** Scroll in Share Sheet, or use "Edit Actions" to add VegyScan

### Exc-2: Share Extension Crashes or Fails to Launch

**Occurs when:** Extension fails to activate (Step 8)

1. Extension crashes or doesn't respond
2. iOS displays error: "Unable to share with VegyScan"
3. User returns to original app (Google Maps, Photos, etc.)
4. **Workaround:** User can save photo to library, then use Upload feature (UC-006)
5. → Use case ends (failure)

### Exc-3: Network Error During Processing

**Occurs when:** LLM API call fails after OCR completes (Step 11)

1. System completes OCR successfully (on-device)
2. System attempts to send OCR text to LLM → network error
3. System automatically retries (3 attempts, exponential backoff)
4. If retry fails:
   - System displays: "Unable to process menu. Check connection and try again."
   - Photo cached locally with OCR text
   - Options: "Retry Now" / "Save for Later" / "Cancel"
5. If "Retry Now" → Retry LLM call
6. If "Save for Later" → Menu saved to history as "Processing failed - retry later"
7. If "Cancel" → Returns to original app (Share flow canceled)
8. → Use case ends (partial failure)

### Exc-4: Unsupported File Type (Not a Photo)

**Occurs when:** User tries to share non-image file (Step 8)

1. Extension receives non-image data (PDF, text file, etc.)
2. Extension validates content type → not supported
3. System displays: "VegyScan only supports photo files."
4. User returns to original app
5. → Use case ends (failure)

## Postconditions

### Success
- Menu photo processed from external app
- Menu saved to history with source app metadata ("Shared from Google Maps")
- Interactive menu view displayed in VegyScan
- **No location tag** if EXIF GPS not present (REQ-F-035 - shared photos never use current GPS)
- User can analyze menu before visiting restaurant (pre-visit planning)

### Partial Success
- Photo and OCR text cached locally
- Menu in history marked "Processing failed - retry later"
- User can retry later

### Failure
- Photo not processed
- User returns to original app
- No data saved in VegyScan

## Business Rules

- **BR-007-1:** Share Extension is lightweight - hands off photo to main app immediately (no heavy processing in extension)
- **BR-007-2:** Shared photos **NEVER** use current GPS location (REQ-F-035)
  - EXIF GPS from photo = OK
  - No EXIF GPS = No location tag (not current GPS)
  - Prevents tagging home GPS to restaurant menu when browsing from home
- **BR-007-3:** Share Extension works WITHOUT location permission (REQ-F-035)
- **BR-007-4:** Share Extension uses App Groups to communicate with main app
- **BR-007-5:** Source app metadata is saved ("Shared from Google Maps", "Shared from Photos", etc.)
- **BR-007-6:** Duplicate detection runs same as camera/upload (REQ-F-029)
- **BR-007-7:** Network errors trigger automatic retries (3 attempts, exponential backoff)

## Related Artifacts

- **Requirements:**
  - [REQ-F-034: iOS Share Extension](../requirements/functional.md#req-f-034)
  - [REQ-F-035: Smart Location Tagging](../requirements/functional.md#req-f-035)
  - [REQ-F-029: Menu Duplicate Detection](../requirements/functional.md#req-f-029)
  - [REQ-NF-012: Network Resilience](../requirements/non-functional.md#req-nf-012)
- **User Stories:** [US-034](../user-stories/stories.md#us-034)
- **Related Use Cases:**
  - [UC-006: Upload from Photo Library](./UC-006-upload-menu-photo.md) (fallback if share fails)
  - [UC-001: Scan single-page menu](./UC-001-scan-single-page-menu.md) (alternative at restaurant)

## Notes

### Strategic Value (Google Maps Integration)
This use case is a **killer feature** for pre-visit planning:
- User browsing Google Maps for restaurants (planning trip)
- Sees menu photo in restaurant photos
- Shares to VegyScan
- Instantly sees vegan/vegetarian options
- Makes informed decision BEFORE leaving home
- **Competitive advantage:** Google Translate and ChatGPT don't have this integration

### Technical Implementation
- **iOS Share Extension:** Separate extension target in Xcode
- **App Groups:** Container for shared data between extension and main app
  - Extension writes photo data to shared container
  - Main app reads from shared container
- **Extension lifecycle:** Must be lightweight (< 100ms ideally)
  - Extension receives photo → writes to App Groups → launches main app → exits
  - Main app does all heavy processing (OCR, LLM, etc.)
- **Supported apps:** Any app that supports iOS Share Sheet with image sharing
  - Photos, Safari, Google Maps, Messages, WhatsApp, Instagram, etc.

### Location Privacy (Critical)
- **Scenario:** User at home browsing Google Maps
- **Wrong behavior:** Tag menu with current GPS (home address) ❌
- **Correct behavior:** Check EXIF GPS from photo, if none → no location tag ✅
- **Privacy benefit:** No location permission required for Share Extension

### Viral Potential
- **Friend sharing:** "Is this restaurant vegan-friendly?" → Share menu → VegyScan analyzes → Reply with answer
- **Group planning:** Multiple friends share menus from different restaurants → Compare options → Choose best one
- **Social proof:** Users see app in Share Sheet on friends' devices → Organic discovery

### Cost Optimization
- **Duplicate detection:** If user shares same menu multiple times (e.g., comparing restaurants), cache hit prevents redundant LLM calls
- **OCR on-device:** No API cost for text extraction
- **LLM optimization:** Only send OCR text (not photo) - reduces payload and cost
