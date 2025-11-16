# UC-008: First-Time User Onboarding

> **ID:** UC-008
> **Status:** Draft
> **Created:** 2025-11-16
> **Last Updated:** 2025-11-16

## Actors

- **Primary:** All new users (first-time app launch)
- **Secondary:** N/A

## Preconditions

1. User has installed VegyScan app on iOS device
2. User opens app for the first time
3. App detects no previous launch (first-time flag not set)

## Postconditions

**Success:**
- User completes or skips onboarding tutorial
- First-time flag set to prevent tutorial from showing again
- User lands on main app screen (camera ready to scan)
- User understands core app functionality

**Failure:**
- User force-quits app during onboarding
- Next launch shows onboarding again (first-time flag not yet set)

## Main Flow (Happy Path)

1. User taps VegyScan app icon on home screen
2. App launches and detects first-time use
3. System displays **Onboarding Screen 1: Scan Any Menu**
   - Heading: "Scan any menu in any language"
   - Visual: Animated illustration of camera scanning menu
   - Body text: "Point your camera at a restaurant menu and we'll translate it instantly"
   - Buttons: [Skip] (top-right) | [Next →] (bottom)
4. User taps [Next →]
5. System displays **Onboarding Screen 2: See Vegan/Vegetarian Options**
   - Heading: "See vegan & vegetarian options instantly"
   - Visual: Menu with green checkmarks on vegan dishes
   - Body text: "Tap any dish to see ingredients, classifications, and confidence levels"
   - Buttons: [Skip] (top-right) | [← Back] [Next →] (bottom)
6. User taps [Next →]
7. System displays **Onboarding Screen 3: Privacy First**
   - Heading: "All data stays on your device"
   - Visual: Shield icon with "No Cloud" symbol
   - Body text: "Your scans are stored locally. No account needed. No data uploaded."
   - Buttons: [Skip] (top-right) | [← Back] [Get Started] (bottom)
8. User taps [Get Started]
9. System sets first-time flag to prevent future tutorial
10. System navigates to main app screen (camera ready to scan)
11. **Optional:** System requests camera permission (iOS system dialog)
12. User is ready to scan first menu

**Duration:** 30-60 seconds (if not skipped)

## Alternative Flows

### Alt-1: User Skips Tutorial

**Trigger:** User taps [Skip] on any onboarding screen

1. System displays confirmation: "Skip tutorial?"
   - "You can always restart the tutorial from Settings"
   - Buttons: [Cancel] [Skip Tutorial]
2. User taps [Skip Tutorial]
3. System sets first-time flag
4. System navigates to main app screen
5. Flow ends → User ready to scan

**Rationale:** Respects power users who don't want tutorial. Confirmation prevents accidental skips.

### Alt-2: User Taps [← Back]

**Trigger:** User taps back button on Screen 2 or Screen 3

1. System navigates to previous onboarding screen
2. User can continue forward or skip
3. Flow continues normally

### Alt-3: User Re-Opens Tutorial from Settings (Future)

**Trigger:** User taps "Show Tutorial Again" in Settings

1. System displays onboarding Screen 1 (same as first-time flow)
2. User can complete or skip tutorial
3. First-time flag remains set (doesn't reset)
4. Flow ends normally

## Exception Flows

### Exc-1: User Force-Quits App During Onboarding

**Trigger:** User swipes up to force-quit app before completing/skipping onboarding

1. App terminates
2. First-time flag NOT set (tutorial incomplete)
3. Next app launch: Onboarding restarts from Screen 1
4. User sees tutorial again

**Rationale:** Cannot assume user saw tutorial if they quit early. Ensures all users are onboarded.

### Exc-2: iOS Permission Denied (Camera)

**Trigger:** User denies camera permission after completing onboarding

1. System shows message: "Camera access required to scan menus"
2. System displays options:
   - "Open Settings" → takes user to iOS Settings to grant permission
   - "Use Photo Library Instead" → navigates to upload flow (UC-006)
3. User can still use app (upload, share extension work without camera)

**Rationale:** Graceful degradation (REQ-NF-009) - app functional without camera permission.

## Business Rules

1. **Tutorial shown exactly once** on first app launch (unless force-quit early)
2. **Always skippable** - user can skip at any point (respects user autonomy)
3. **No account creation** - onboarding does NOT ask for sign-up/login
4. **No permission requests** during tutorial - permissions requested when needed (camera on first scan)
5. **Maximum 3 screens** - keep tutorial brief (users want to start scanning)
6. **Focus on value, not features** - communicate "why use this" not "how to use buttons"

## UI/UX Notes

**Visual Design:**
- Clean, minimal illustrations (not screenshots - future-proof)
- Large, readable text (accessibility - REQ-NF-020)
- High contrast (accessibility - REQ-NF-021)
- Animated transitions between screens (smooth, not jarring)

**Copy Tone:**
- Friendly, not corporate
- Concise (5-10 words per headline, 15-20 words per body)
- Emphasize benefits: "Scan any menu" not "Tap the scan button"
- Privacy messaging: "All data stays on your device" builds trust

**Accessibility:**
- VoiceOver support (REQ-NF-019): Announce screen number "Screen 1 of 3"
- Skip button accessible via VoiceOver
- Swipe gestures for next/previous (in addition to buttons)

## Performance Criteria

- Onboarding screens load instantly (< 0.3s per transition)
- Animations smooth (60fps)
- "Get Started" navigates to main screen in < 0.5s

## Related

- **Requirements:**
  - REQ-F-036: First-Time User Onboarding
  - REQ-NF-006: Intuitive First-Time Use
  - REQ-NF-019: VoiceOver Support
  - REQ-NF-020: Dynamic Type Support
  - REQ-NF-021: Color Contrast

- **User Stories:**
  - US-001: Capture Menu Photo with Guide Lines (first action after onboarding)

- **Personas:**
  - All personas benefit from onboarding
  - Sarah (Low literacy): Most benefits from tutorial
  - Ben (High literacy): Most likely to skip

## Notes

**Optional Future Enhancement:**
- Interactive tutorial (user actually scans sample menu during onboarding)
- Personalization: "What's your dietary preference?" (Vegan/Vegetarian/Pescatarian)
  - Only ask if it affects UI behavior (currently menus shown same way regardless)

**Why NOT ask for dietary preference in onboarding:**
- v1: Menu display same for all users (show all dishes with classifications)
- No filtering in v1 (all dishes visible)
- Asking wastes user time if not used
- Can add in v2 if we add filtering/personalization features
