# UC-006: Upload Menu Photo from Photo Library

> **ID:** UC-006
> **Status:** Draft
> **Created:** 2025-11-15
> **Last Updated:** 2025-11-15

## Actors

- **Primary:** All personas - particularly useful for trip planning before visiting restaurant
- **Secondary:** Users who took menu photos earlier

## Preconditions

1. User has VegyScan app installed on iOS device
2. User has granted Photos permission (OR will grant during flow)
3. User has menu photos in their photo library (from earlier, Google Maps, friends, etc.)
4. User has set preferred target language in app settings

## Main Flow (Happy Path)

1. User opens VegyScan app
2. App displays main screen with "Scan New Menu" and "Upload Photo" options
3. User taps "Upload Photo"
4. iOS Photo Picker opens (native system UI)
5. User selects single photo OR multiple photos (for multi-page menu)
6. User taps "Done" in Photo Picker
7. System extracts EXIF GPS data from photo(s) (see REQ-F-035)
   - If EXIF GPS found → tag menu with that location
   - If no EXIF GPS → save menu without location tag
   - **Never use current GPS location** for uploaded photos
8. System processes photo(s) identically to camera capture:
   - Image optimization (straightening, brightness, sharpening)
   - OCR (text extraction) - **on-device**
   - Symbol recognition
   - Meta-info bundling
9. If multiple photos selected → creates multi-page menu automatically
10. System displays processed menu in interactive view
11. System saves to history with source metadata ("Uploaded from library")
12. → Use case ends successfully

## Alternative Flows

### Alt-1: Photos Permission Not Granted (First Time)

**Branches from:** Step 4 in Main Flow

1. System checks Photos permission → not granted
2. iOS displays permission dialog: "VegyScan would like to access your photos"
3. User taps "Allow" (full access or selected photos - iOS 14+)
4. → Returns to step 4 (Photo Picker opens)

### Alt-2: User Denies Photos Permission

**Branches from:** Alt-1, Step 3

1. User taps "Don't Allow"
2. System displays message: "Photo upload requires Photos access. Enable in Settings?"
3. Options: "Open Settings" / "Use Camera Instead" / "Cancel"
4. If "Open Settings" → Opens iOS Settings app
5. If "Use Camera Instead" → Opens camera view (UC-001)
6. If "Cancel" → Returns to main screen
7. → Use case ends

### Alt-3: Upload Single Photo to Existing Menu (Add Page)

**Branches from:** Step 3 in Main Flow (user viewing existing menu)

1. User viewing existing menu, taps "Add Page"
2. User selects "Upload Photo"
3. Photo Picker opens
4. User selects single photo
5. System processes and adds as new page to existing menu
6. Page numbers update (Page 1 of 3, etc.)
7. → Returns to multi-page menu view (UC-002)

### Alt-4: Upload Photo from Google Maps (Pre-Visit Planning)

**Branches from:** Step 5 in Main Flow

1. User previously saved Google Maps restaurant photo to camera roll
2. User selects that photo from library
3. Photo has NO EXIF GPS (Google Maps screenshot)
4. System saves menu without location tag
5. System adds source metadata: "Uploaded from library, no location data"
6. User can still view history, just not GPS-matched
7. → Returns to step 8 in Main Flow

## Exception Flows

### Exc-1: Photo Quality Too Poor

**Occurs when:** Uploaded photo is too blurry/dark (Step 8)

1. System detects low quality score (same as UC-005)
2. System displays feedback: "Photo quality too low. Try a different photo or use camera."
3. User presented with options:
   - "Choose Different Photo" → Returns to step 3
   - "Use Camera" → Opens camera view (UC-001)
   - "Use Anyway" (user override) → Continues processing with warning
4. → Returns to step 8 OR step 3 based on user choice

### Exc-2: OCR Completely Fails (No Text Recognized)

**Occurs when:** OCR returns no usable text (Step 8)

**Technical Note:** OCR is on-device using iOS VisionKit

1. System attempts OCR → no text detected
2. System displays message: "No menu text detected. Please try a different photo."
3. Visual feedback: Shows photo with no hotspots/overlays
4. User presented with options:
   - "Choose Different Photo" → Returns to step 3
   - "Retake with Camera" → Opens camera view (UC-001)
   - "Cancel" → Returns to main screen
5. → Use case ends (failure)

### Exc-3: Network Error During LLM Processing

**Occurs when:** Translation or classification API call fails (Step 8)

**Technical Note:** Only OCR text (JSON) is sent to LLM, not photos

1. System completes OCR successfully (on-device)
2. System attempts to send OCR text to LLM API → network error
3. System automatically retries (3 attempts with exponential backoff: 1s, 2s, 4s)
4. If retry succeeds → Continue processing
5. If all retries fail:
   - System displays message: "Unable to process menu. Check connection and try again."
   - Photo and OCR text cached locally
   - Options: "Retry Now" / "Save for Later" / "Cancel"
6. If "Retry Now" → Returns to step 8 (retry LLM call)
7. If "Save for Later" → Menu saved to history as "Processing failed - retry later"
8. If "Cancel" → Returns to main screen
9. → Use case ends (partial failure)

## Postconditions

### Success
- Menu photo(s) uploaded and processed
- Menu saved to history (with or without location tag)
- Interactive menu view displayed
- Source metadata recorded ("Uploaded from library")
- EXIF GPS extracted and used if available (REQ-F-035)

### Partial Success (OCR OK, LLM failed)
- Menu photo and OCR text cached locally
- Menu in history marked "Processing failed - retry later"
- User can retry later when connection available

### Failure
- Photo not processed
- No data saved
- User returns to main screen or Photo Picker

## Business Rules

- **BR-006-1:** Photos permission is OPTIONAL (user can use camera-only mode if denied)
- **BR-006-2:** Uploaded photos use EXIF GPS ONLY, never current GPS location (REQ-F-035)
- **BR-006-3:** Menus without location tags are still saved (accessible in "All Scans" history)
- **BR-006-4:** OCR is performed on-device (iOS VisionKit) - no photo sent to cloud
- **BR-006-5:** Only OCR text (JSON) is sent to LLM API - photo never leaves device
- **BR-006-6:** Multi-photo upload creates multi-page menu automatically
- **BR-006-7:** Network errors trigger automatic retries (3 attempts, exponential backoff)

## Related Artifacts

- **Requirements:**
  - [REQ-F-032: Upload from Photo Library](../requirements/functional.md#req-f-032)
  - [REQ-F-033: Add Page to Existing Menu](../requirements/functional.md#req-f-033)
  - [REQ-F-035: Smart Location Tagging](../requirements/functional.md#req-f-035)
  - [REQ-F-003: OCR on-device](../requirements/functional.md#req-f-003)
  - [REQ-NF-012: Network Resilience](../requirements/non-functional.md#req-nf-012)
- **User Stories:** [US-032](../user-stories/stories.md#us-032)
- **Related Use Cases:**
  - [UC-001: Scan single-page menu](./UC-001-scan-single-page-menu.md) (camera alternative)
  - [UC-002: Multi-page menu book](./UC-002-create-multi-page-menu-book.md) (if multiple photos)
  - [UC-005: Retake poor quality photo](./UC-005-retake-poor-quality-photo.md) (quality issues)

## Notes

- **Pre-visit planning use case:** User browses Google Maps at home, saves menu photo, uploads to VegyScan, analyzes before visiting restaurant
- **iOS Photos permission:** iOS 14+ allows "Select Photos" (limited access) or "Full Access"
  - App should work with either permission level
  - User can grant access to specific photos only
- **EXIF GPS extraction:** Use iOS ImageIO framework to read GPSLatitude, GPSLongitude from photo metadata
- **OCR on-device:** iOS VisionKit (VNRecognizeTextRequest) processes image locally - faster, more private, no API cost
- **LLM API optimization:** Only send OCR text + metadata (not photos) to reduce cost and increase privacy
- **Retry strategy:** Exponential backoff (1s, 2s, 4s) prevents API hammering, gives transient errors time to resolve
