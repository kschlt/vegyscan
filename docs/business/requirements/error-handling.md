# Error Handling & User Messages

> **Last Updated:** 2025-11-15
> **Status:** Draft
> **Purpose:** Single Source of Truth for error handling strategies, retry logic, and user-facing messages

_This document defines consistent error handling patterns and a reusable message library to ensure consistent UX and enable LLM agents to use pre-defined messages (not make up random ones)._

---

## Core Principles

### 1. **Fail Gracefully**
- Errors should be handled in the background when possible
- System should attempt automatic recovery (retries, fallbacks)
- User should only see errors when manual intervention is required

### 2. **Informative, Not Technical**
- Messages explain WHAT went wrong and WHAT to do next
- Avoid technical jargon ("API timeout" → "Unable to connect")
- Provide actionable guidance ("Check connection and retry")

### 3. **Consistent Tone**
- Friendly but concise
- Apologetic when app fails ("Unable to process")
- Helpful when user action needed ("Try a different photo")
- No blame ("Photo quality too low", NOT "You took a bad photo")

### 4. **Feature Degradation, Not Failure**
- Permission denied → Feature disabled, app continues
- Network unavailable → Cache locally, retry later
- OCR fails on part of menu → Show what was recognized, skip unrecognized parts

---

## Error Categories

### Category 1: User Input Issues (Recoverable)
**Cause:** User photo quality, permission denial, invalid input
**Handling:** Inform user, provide clear action (retake, grant permission, try different photo)

### Category 2: Technical Failures (Transient)
**Cause:** Network errors, API timeouts, rate limits
**Handling:** Automatic retry with exponential backoff, cache for later, inform user if persistent

### Category 3: System Limitations (Expected)
**Cause:** Unsupported scenario (handwritten menu, multiple menus in one photo)
**Handling:** Inform user of limitation, suggest workaround

### Category 4: Critical Errors (Unexpected)
**Cause:** Bugs, data corruption, unexpected states
**Handling:** Log error, display generic message, provide way to report

---

## Retry Logic Strategy

### Automatic Retries (Transient Errors)
**When:** Network errors, API timeouts, rate limits
**Strategy:** Exponential backoff

```
Retry 1: Wait 1 second  → Retry
Retry 2: Wait 2 seconds → Retry
Retry 3: Wait 4 seconds → Retry
If all fail: Display error to user with manual retry option
```

**Why:** Transient errors (network glitches, API overload) often resolve quickly
**Benefit:** 90%+ of transient errors resolve within 3 retries

### No Automatic Retries (User Errors)
**When:** Poor photo quality, permission denied, invalid input
**Why:** Automatic retry won't fix user input issues
**Handling:** Inform user immediately, provide action

### Manual Retry Available Always
**When:** Any error (automatic retries exhausted)
**Why:** User may want to retry after fixing issue (enabling WiFi, granting permission, etc.)
**UX:** "Retry" button always available in error states

---

## Permission Handling (Graceful Degradation)

### Camera Permission Denied

**Behavior:**
- ✅ Upload from Photo Library still works (UC-006)
- ✅ iOS Share Extension still works (UC-007)
- ❌ In-app camera disabled (UC-001)

**UX:**
- When user taps "Scan Menu" (camera):
  - Show message: "Camera access required. Enable in Settings?"
  - Options: "Open Settings" / "Upload Photo Instead" / "Cancel"
- Main screen shows "Upload Photo" prominently (not hidden)

**Technical:**
- Check `AVCaptureDevice.authorizationStatus(for: .video)` before camera use
- Never crash or fail silently
- Fallback: Upload-only mode works without camera permission

---

### Photos Permission Denied

**Behavior:**
- ✅ In-app camera still works (UC-001)
- ✅ iOS Share Extension still works (UC-007)
- ❌ Upload from Photo Library disabled (UC-006)

**UX:**
- When user taps "Upload Photo":
  - Show message: "Photo Library access required. Enable in Settings?"
  - Options: "Open Settings" / "Use Camera Instead" / "Cancel"
- Main screen shows "Scan Menu" (camera) prominently

**Technical:**
- Check `PHPhotoLibrary.authorizationStatus()` before photo picker
- iOS 14+ supports "Select Photos" (limited access) - app should work with this
- Never crash or fail silently

---

### Location Permission Denied

**Behavior:**
- ✅ All features work (camera, upload, share)
- ❌ GPS-based history matching disabled (REQ-F-019)
- ❌ Current location tagging disabled for camera captures
- ✅ EXIF GPS extraction still works (from uploaded/shared photos)

**UX:**
- **No error message shown** (feature degrades silently)
- Menus saved without location tag
- History shows "All Scans" (no GPS grouping by restaurant)
- Optional: Show subtle banner once: "Enable Location for restaurant matching" (dismissable)

**Technical:**
- Check `CLLocationManager.authorizationStatus()` before accessing location
- If denied:
  - Skip GPS tagging for camera captures
  - Skip GPS-based history matching
  - Still save menus (just without location)
  - No failure, no blocking user flow
- Feature-specific degradation, not app-wide failure

---

## OCR Failure Scenarios

### Scenario 1: OCR Completely Fails (No Text Recognized)

**Cause:**
- Handwritten menu (OCR can't read handwriting)
- Photo too blurry/dark
- Non-text image (menu photo contains only pictures)
- Unsupported script (rare - modern OCR is universal)

**Handling:**
1. OCR returns empty result or very low confidence
2. System detects: No usable text extracted
3. Display message to user

**Message:** (See Message Library MSG-OCR-001)
```
"Unable to read menu text. Please try:
• Better lighting and focus
• Clear photo of text-based menu
• Different menu page"

[Choose Different Photo]  [Retake with Camera]  [Cancel]
```

**Technical:**
- On-device OCR using iOS VisionKit (`VNRecognizeTextRequest`)
- Threshold: If < 10 characters recognized OR all confidence < 0.3 → fail
- No automatic retry (OCR is on-device, instant)

---

### Scenario 2: OCR Partially Succeeds (Some Text Recognized)

**Cause:**
- Part of menu is readable, part is blurry/obscured
- Mixed text and images
- Low confidence on some sections

**Handling:**
1. OCR returns partial results (some text, some failures)
2. System processes recognized text
3. System displays visual feedback of what was recognized

**Message:** (No error - show visual feedback)
```
Visual feedback on menu:
- Recognized text: Normal hotspots (blue outline)
- Unrecognized areas: Grayed out or no hotspot
- Optional banner: "Some menu items could not be recognized. Tap to retake."
```

**Technical:**
- Display hotspots only on recognized text
- Unrecognized areas: No hotspot, subtle gray overlay
- User can see visually what was skipped
- Optional: User can tap unrecognized area → "Unable to read this section. Retake photo?"

---

## Translation API Failures

### Scenario: Translation API Down or Unreachable

**Cause:**
- No internet connection
- Translation API service down
- API rate limit hit
- Network timeout

**Handling:**
1. OCR succeeds (on-device)
2. System attempts translation API call → fails
3. System retries automatically (3 attempts, exponential backoff: 1s, 2s, 4s)
4. If all retries fail:
   - Show error message
   - Cache OCR text locally
   - Allow manual retry later

**Message:** (See Message Library MSG-NET-001)
```
"Unable to translate menu. Check your connection and try again."

[Retry Now]  [Save for Later]  [Cancel]
```

**If user selects "Save for Later":**
- Menu saved to history with status "Translation pending"
- User can retry later from history view
- When network restored, user can tap "Retry Translation"

**Technical:**
- Retry logic: 3 attempts, exponential backoff (1s, 2s, 4s)
- Cache: Save photo + OCR text + metadata to local SQLite
- Retry later: User-initiated from history ("Retry" button on failed scans)

---

## LLM API Failures

### Scenario: LLM Classification API Down or Unreachable

**Cause:**
- No internet connection
- LLM API service down (OpenAI/Anthropic/Google outage)
- API rate limit hit
- Invalid API key (configuration error)

**Handling:**
1. OCR and translation succeed
2. System attempts LLM classification API call → fails
3. System retries automatically (3 attempts, exponential backoff: 1s, 2s, 4s)
4. If all retries fail:
   - Show error message
   - Cache OCR + translation locally
   - Allow manual retry later
   - Display menu WITHOUT classification (translation + hotspots only)

**Message:** (See Message Library MSG-NET-001 - same as translation)
```
"Unable to analyze menu. Check your connection and try again."

[Retry Now]  [Save for Later]  [Cancel]
```

**If user selects "Save for Later":**
- Menu saved with OCR + translation (partial success)
- Vegan/vegetarian classification marked "Pending"
- User can retry classification later

**Technical:**
- Graceful degradation: Show menu with translation, no classification badges
- Retry logic: 3 attempts, exponential backoff
- Cache: Save OCR + translation + photo
- Retry later: User-initiated from history

---

### Scenario: LLM Returns Invalid Response

**Cause:**
- LLM returns malformed JSON
- LLM refuses classification (content policy violation - rare)
- LLM returns empty/nonsensical response

**Handling:**
1. OCR and translation succeed
2. System sends request to LLM → receives invalid response
3. System validates JSON schema → validation fails
4. System retries (3 attempts - maybe LLM glitched)
5. If all retries return invalid:
   - Log error for debugging
   - Display menu without classification
   - Show generic error message

**Message:** (See Message Library MSG-PROC-001)
```
"Unable to analyze this menu. Please try again or contact support."

[Retry]  [Cancel]
```

**Technical:**
- JSON validation: Check schema before using LLM response
- If validation fails 3 times → likely systematic issue, not transient
- Log error with request/response for debugging
- Fallback: Show menu without classification (better than nothing)

---

## Storage Full (Rare Edge Case)

### Scenario: Device Storage Full

**Cause:**
- User's device storage is full
- Cannot save menu photo or data to local SQLite

**Handling:**
1. System attempts to save menu → storage write fails
2. System displays message to user

**Message:** (See Message Library MSG-STORAGE-001)
```
"Unable to save menu. Your device storage is full. Free up space and try again."

[OK]
```

**Technical:**
- iOS likely shows system-level alert before this happens
- App should check available storage before saving (if possible)
- Rare case - most users won't hit this
- No retry (user must free up storage manually)

---

## Unsupported Scenarios (Expected Limitations)

### Scenario: Handwritten Menu

**Cause:**
- User photographs handwritten menu (chalkboard, handwritten specials)
- OCR cannot read handwriting (expected limitation)

**Handling:**
- OCR fails (Scenario 1: No text recognized)
- Use MSG-OCR-001 (already covers this)

**Future:** Handwritten OCR is possible (specialized models) but not v1 scope

---

### Scenario: Multiple Menus in Same Photo

**Cause:**
- User photographs two menu pages side-by-side
- System detects multiple menu layouts in one photo

**Handling (Current - To Be Decided):**

**Option A: Inform User to Photograph Separately**
```
"Multiple menus detected. Please photograph each menu separately for best results."

[Retake]  [Cancel]
```

**Option B: Split into Two Pages Automatically (Future)**
- Detect menu boundaries
- Split photo into two pages
- Create 2-page menu book

**Decision:** Option A for v1 (simpler), Option B for future enhancement

---

### Scenario: Screenshot of Digital Menu

**Cause:**
- User shares screenshot of menu from restaurant website/app
- Photo is a screenshot (not original photo)

**Handling (Current):**
- Same processing as regular photo upload
- No special handling for v1

**Future Enhancement:**
- Detect screenshot (metadata analysis)
- Optimize for digital menu layout (different from physical menu photo)

---

## Message Library (Reusable Messages)

_Single Source of Truth for all user-facing error messages_

### MSG-OCR-001: OCR Failed (No Text Recognized)
```
Title: "Unable to Read Menu Text"
Message: "Please try:
• Better lighting and focus
• Clear photo of text-based menu
• Different menu page"

Actions: [Choose Different Photo] [Retake with Camera] [Cancel]
```
**Usage:** UC-006 Exc-2, UC-007 (if OCR fails after share)

---

### MSG-NET-001: Network Error (General)
```
Title: "Connection Error"
Message: "Unable to process menu. Check your connection and try again."

Actions: [Retry Now] [Save for Later] [Cancel]
```
**Usage:** UC-001 Exc-3, UC-006 Exc-3, UC-007 Exc-3 (translation/LLM API failures)

---

### MSG-PROC-001: Processing Error (Unexpected)
```
Title: "Processing Error"
Message: "Unable to analyze this menu. Please try again or contact support."

Actions: [Retry] [Cancel]
```
**Usage:** LLM returns invalid JSON, unexpected processing failures

---

### MSG-QUALITY-001: Photo Quality Too Poor
```
Title: "Photo Quality Too Low"
Message: "Please retake with:
• Better lighting
• Steady camera (avoid blur)
• Clear view of menu"

Actions: [Retake Photo] [Choose Different Photo] [Use Anyway]
```
**Usage:** UC-001 Exc-1, UC-005, UC-006 Exc-1 (quality detection)

---

### MSG-PERM-CAM-001: Camera Permission Denied
```
Title: "Camera Access Required"
Message: "VegyScan needs camera access to scan menus. Enable in Settings?"

Actions: [Open Settings] [Upload Photo Instead] [Cancel]
```
**Usage:** UC-001 (camera permission denied)

---

### MSG-PERM-PHOTO-001: Photos Permission Denied
```
Title: "Photo Library Access Required"
Message: "VegyScan needs access to your photos. Enable in Settings?"

Actions: [Open Settings] [Use Camera Instead] [Cancel]
```
**Usage:** UC-006 Alt-2 (photo library permission denied)

---

### MSG-STORAGE-001: Device Storage Full
```
Title: "Storage Full"
Message: "Unable to save menu. Your device storage is full. Free up space and try again."

Actions: [OK]
```
**Usage:** Rare edge case when device storage is full

---

### MSG-MULTI-MENU-001: Multiple Menus Detected (Future)
```
Title: "Multiple Menus Detected"
Message: "Please photograph each menu separately for best results."

Actions: [Retake] [Cancel]
```
**Usage:** Future feature (detecting multiple menus in one photo)

---

### MSG-RETRY-001: Generic Retry Prompt
```
Title: "Try Again?"
Message: "Something went wrong. Please try again."

Actions: [Retry] [Cancel]
```
**Usage:** Generic fallback for unexpected errors

---

## Error Logging & Monitoring

_What to log for debugging and monitoring (not shown to user)_

### Log Levels

**ERROR (Critical - Requires Investigation):**
- LLM API consistently returning invalid JSON
- Storage write failures (unexpected)
- App crashes
- Share Extension crashes

**WARNING (Monitor - May Indicate Issues):**
- OCR confidence consistently low (< 50%)
- Network retries exhausting (3+ failures)
- API rate limits hit frequently

**INFO (Normal Operation):**
- Network retry succeeded
- Cache hit/miss
- Feature degradation (permission denied)

### What to Log (Error Context)

For each error, log:
1. **Error type** (OCR failed, Network timeout, Invalid JSON, etc.)
2. **User action** (Camera capture, Upload, Share from Google Maps, etc.)
3. **Context** (Photo size, language detected, API endpoint called)
4. **Retry attempts** (How many retries before failure)
5. **Recovery** (Cached for later? User canceled? Retry succeeded?)

### Where to Send Logs

**Options (To Be Decided in Architecture Phase):**
- Firebase Crashlytics (free tier)
- Sentry (error tracking)
- Apple Analytics (built-in)
- Custom logging server

**Privacy:**
- Never log user photos
- Never log menu text (may contain private info)
- Log metadata only (error type, context, timestamp)

---

## Testing Error Scenarios

_How to test these error cases_

### Simulating Errors (Development/Testing)

**OCR Failure:**
- Upload photo with no text (pure image)
- Upload blurry/dark photo
- Upload handwritten text

**Network Failure:**
- Enable airplane mode before LLM call
- Use network simulator (Charles Proxy, etc.)
- Mock API returning errors

**Permission Denied:**
- Deny camera permission in Settings
- Deny photo library permission
- Deny location permission

**LLM Invalid Response:**
- Mock API returning malformed JSON
- Mock API returning empty response

---

## Related Artifacts

- **Use Cases:** UC-001 to UC-007 (exception flows reference these messages)
- **Requirements:** REQ-NF-012 (Network Resilience), REQ-NF-011 (Error Handling)
- **User Stories:** Error handling in acceptance criteria

---

## Notes for LLM Agent Implementation

_When building the app with an LLM agent, reference this document to ensure:_

1. **Use pre-defined messages** from Message Library (MSG-XXX-YYY)
   - Do NOT make up random error messages
   - Do NOT use technical jargon
   - Use exact wording from MSG-XXX-YYY codes

2. **Implement retry logic** as specified
   - 3 attempts, exponential backoff (1s, 2s, 4s)
   - Automatic retries for network errors
   - No automatic retries for user errors

3. **Graceful degradation** for permission denials
   - Camera denied → Upload still works
   - Photos denied → Camera still works
   - Location denied → Feature disabled silently (no error)

4. **Never crash on errors**
   - Always handle errors gracefully
   - Always provide user action (Retry, Cancel, etc.)
   - Always cache data for later retry when possible

5. **Consistent UX**
   - Friendly, concise tone
   - Actionable guidance
   - No blame language
