# UC-005: Retake Photo Due to Poor Quality

> **ID:** UC-005
> **Status:** Draft
> **Created:** 2025-11-15
> **Last Updated:** 2025-11-15

## Actors

- **Primary:** All users
- **Secondary:** System (automated quality detection)

## Preconditions

1. User is attempting to scan a menu (UC-001, step 5)
2. Camera has captured an image
3. App is performing image quality assessment

## Main Flow (Happy Path)

1. User captures menu photo (UC-001, step 5)
2. App performs automatic quality checks:
   - **Blur detection** (focus/motion blur)
   - **Brightness** (too dark or overexposed)
   - **Reflection/glare** (light reflecting off laminated menu)
   - **Text detectability** (can OCR find readable text?)
   - **Perspective** (extreme angle making menu unreadable)
3. App detects quality issue (e.g., too blurry)
4. App displays clear feedback message:
   - "Photo too blurry. Please hold camera steady."
   - "Menu too dark. Try better lighting or use flash."
   - "Glare detected. Adjust angle to avoid reflections."
5. App shows preview of problematic photo with issue highlighted
6. App provides actionable tips:
   - Icon indicators: 📸 Hold steady / 💡 More light / 🔄 Change angle
7. App offers two buttons: "Retake" (primary) or "Use Anyway" (secondary)
8. User taps "Retake"
9. App returns to camera view (UC-001, step 3)
10. User repositions camera based on feedback
11. User captures new photo
12. → App performs quality check again (returns to step 2)
13. If quality is acceptable → Continue to UC-001, step 6

## Alternative Flows

### Alt-1: User Proceeds Despite Warning

**Branches from:** Step 7 in Main Flow

1. User taps "Use Anyway"
2. App displays disclaimer: "Quality may affect accuracy. Proceed?"
3. User confirms
4. App attempts to process photo (UC-001, step 6)
5. If processing succeeds → Continue UC-001
6. If processing fails (no text detected) → Return to Exc-2 in UC-001

### Alt-2: Multiple Quality Issues

**Branches from:** Step 3 in Main Flow

1. App detects multiple issues (e.g., blurry AND too dark)
2. App prioritizes most critical issue in feedback message
3. App shows: "Photo too dark and blurry. Use more light and hold steady."
4. Tips shown for both issues
5. → Returns to step 7

### Alt-3: Scanner Guide Lines Help

**Branches from:** Step 1 in Main Flow (proactive)

1. User is in camera view BEFORE capturing
2. App shows real-time guide lines (document scanner style)
3. App detects menu edges and aligns guide box
4. If alignment good → Guide box turns green
5. If alignment poor (angle, distance) → Guide box stays yellow/red
6. User adjusts position based on visual feedback
7. User captures when guide box is green
8. → Significantly reduces quality issues (skip to UC-001, step 6)

## Exception Flows

### Exc-1: Persistent Quality Issues

**Occurs when:** User retakes 3+ times, quality still poor (Step 12)

1. App detects repeated retake attempts
2. App shows enhanced help: "Still having trouble?"
3. App offers:
   - Tutorial: "How to scan a menu" (short animation/video)
   - Manual mode: Disable auto-quality check, process anyway
   - Skip: Cancel scan, try different menu/lighting
4. User chooses option
5. → Depends on choice (tutorial, manual processing, or cancel)

### Exc-2: Environmental Issues (Unsolvable)

**Occurs when:** Menu is inherently unreadable (damaged, faded, extremely poor print)

1. App detects very low quality even with retakes
2. App cannot extract sufficient text
3. App shows: "Menu may be too faded/damaged to scan. Try asking for a different menu."
4. → Use case ends (failure, suggests alternative approach)

### Exc-3: Flash Recommendation

**Occurs when:** Lighting is consistently too dark (Step 4)

1. App detects low brightness across multiple attempts
2. App suggests: "Enable flash? This may help in low light."
3. User enables flash
4. → Returns to step 9 (retake with flash)

## Postconditions

### Success
- User captures acceptable quality photo
- Photo passes quality threshold
- App can proceed with OCR and processing (UC-001 continues)

### Failure
- User cancels scan
- Photo is not processed
- User must try again later or use alternative method

## Business Rules

- **BR-001** Quality check must complete within 0.5 seconds (instant feedback)
- **BR-002** Feedback messages must be actionable (not just "bad quality")
- **BR-003** Guide lines should use iOS VisionKit/Document Scanner APIs
- **BR-004** "Use Anyway" option allows user override (trust user judgment)
- **BR-005** After 3 failed attempts, offer tutorial/help
- **BR-006** Quality threshold should balance accuracy vs. frustration (not too strict)

## Related Artifacts

- **Requirements:**
  - [REQ-F-019: Photo Quality Detection](../requirements/functional.md#req-f-019)
  - [REQ-F-020: Scanner Guide Lines](../requirements/functional.md#req-f-020)
  - [REQ-F-021: Quality Feedback Messages](../requirements/functional.md#req-f-021)
  - [REQ-NF-005: Quality Check Performance](../requirements/non-functional.md#req-nf-005)
  - [REQ-NF-006: User Guidance UX](../requirements/non-functional.md#req-nf-006)
- **User Stories:** [US-008](../user-stories/stories.md#us-008)
- **Related Use Cases:**
  - [UC-001: Scan single page](./UC-001-scan-single-page-menu.md)

## Notes

### Quality Metrics (Technical)
- **Blur:** Laplacian variance < threshold
- **Brightness:** Histogram analysis (mean pixel value)
- **Glare:** Detect oversaturated regions (>95% white)
- **Text detectability:** OCR confidence score
- **Perspective:** Edge detection + skew angle

### iOS-Specific Features
- VisionKit document scanner provides auto-capture when quality is good
- Can leverage built-in edge detection and perspective correction
- Flash control via AVCaptureDevice API

### UX Best Practices
- Show preview with problem areas highlighted (e.g., red circle around glare)
- Animated tips (e.g., hand icon showing "move left" for better angle)
- Haptic feedback when guide lines align (iPhone vibration)
- Positive reinforcement: "Perfect alignment!" when guide box turns green

### Future Enhancement
- Machine learning model trained on "good" vs. "bad" menu photos
- Adaptive thresholds based on menu type (laminated vs. paper vs. chalkboard)
