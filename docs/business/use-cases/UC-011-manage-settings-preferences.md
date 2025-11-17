# UC-011: Manage Settings & Preferences

> **ID:** UC-011
> **Status:** Draft
> **Created:** 2025-11-16
> **Last Updated:** 2025-11-16

## Actors

- **Primary:** All users
- **Secondary:** N/A

## Preconditions

1. App is installed and running on iOS device
2. User has completed first-time onboarding (or skipped it)

## Postconditions

**Success:**
- User views and modifies app settings
- Changes saved immediately to local storage
- App behavior reflects new settings

**Failure:**
- N/A (viewing settings cannot fail)

## Main Flow (Happy Path)

1. User opens VegyScan app
2. User taps **Settings** icon in main navigation (gear icon)
3. System displays **Settings** screen with sections:

### Privacy Settings Section
4. System displays **Privacy** section:
   - **Camera Permission:** "Allowed" (green) or "Denied" (red)
     - Tap → Opens iOS Settings app (deep link to VegyScan permissions)
   - **Photos Permission:** "Allowed" or "Denied"
     - Tap → Opens iOS Settings app
   - **Location Permission:** "Allowed" / "While Using" / "Denied"
     - Tap → Opens iOS Settings app

### Data Management Section
5. System displays **Data Management** section:
   - **Storage Used:** "47.2 MB (23 menus)"
   - **Clear Cache:**
     - Tap → See Alt-1: Clear Cache
   - **Clear All Scan History:**
     - Tap → See UC-010 Alt-3 (Delete all menus)
   - **Data Retention Period:** "90 days" (dropdown)
     - Options: 30 / 60 / 90 / 180 days / Never
     - Tap → See Alt-2: Change Retention Period
   - **Export All Data:**
     - Tap → See Alt-3: Export Data (REQ-F-038)

### Preferences Section (Optional - only if affects behavior)
6. System displays **Preferences** section:
   - **Dietary Preference:** "All" (dropdown) - ONLY if this affects UI behavior
     - Options: Vegan / Vegetarian / Pescatarian / All
     - Note: In v1, this may NOT be shown if menus displayed same way for all users
   - **Language:** "English" (v1 only English, grayed out)
     - Future: Dropdown when i18n implemented

### About Section
7. System displays **About** section:
   - **Version:** "1.0.0 (Build 42)"
   - **Privacy Policy:**
     - Tap → Opens privacy policy (in-app web view or Safari)
   - **Terms of Service:**
     - Tap → Opens terms (in-app web view or Safari)
   - **Open Source Licenses:** (if any)
     - Tap → Shows list of third-party libraries and licenses
   - **Contact Support:**
     - Tap → Opens email composer (support@vegyscan.app)

8. User reviews settings
9. User taps [< Back] to return to main app
10. Flow ends

## Alternative Flows

### Alt-1: Clear Cache

**Trigger:** User wants to free storage without deleting menu history

1. User taps **Clear Cache** in Data Management
2. System displays confirmation:
   - Title: "Clear cache?"
   - Message: "This will free up X MB of storage. Your scan history and favorites will NOT be deleted. Menus will need to be re-processed if opened again."
   - Buttons: [Cancel] [Clear Cache]
3. User taps [Clear Cache]
4. System deletes:
   - LLM classification results cache (REQ-F-030)
   - Dish-level cache (REQ-F-030)
   - Perceptual hash cache (REQ-F-031)
   - Temporary files
5. System keeps:
   - Menu photos
   - Menu metadata (date, location, restaurant name)
   - Favorites
   - OCR text results
6. System updates display: "Storage Used: 12.3 MB (23 menus)" (reduced)
7. System shows toast: "Cache cleared" (2 seconds)
8. Flow ends

**Rationale:** Users may want to free storage without losing menu access. Menus can be re-opened (will re-process, hitting API again).

### Alt-2: Change Data Retention Period

**Trigger:** User wants to keep menus longer or delete sooner

1. User taps **Data Retention Period: 90 days**
2. System displays dropdown options:
   - 30 days
   - 60 days
   - **90 days** (selected, checkmark)
   - 180 days
   - Never
3. User selects **180 days**
4. System saves new setting immediately
5. System displays: "Data Retention Period: 180 days"
6. System shows explanation: "Menus older than 180 days will be automatically deleted. Favorites are never auto-deleted."
7. **Note:** Changed setting applies to FUTURE deletions only (not retroactive)
8. Flow ends

**Business Rule:** Changing retention period does NOT immediately delete menus. Auto-delete runs on next app launch (REQ-F-041).

### Alt-3: Export All Data (GDPR Data Portability)

**Trigger:** User wants to export data or comply with GDPR request

1. User taps **Export All Data**
2. System shows preparing message: "Preparing export..." (spinner)
3. System generates JSON file with all user data:
   - Menu metadata (dates, locations, restaurant names)
   - Favorited dishes
   - User preferences
   - NO photos (too large, already on device)
4. System displays iOS **Share Sheet:**
   - Options: Email, Save to Files, AirDrop, iCloud, etc.
5. User selects **Email**
6. iOS Mail composer opens with JSON file attached:
   - To: (blank)
   - Subject: "VegyScan Data Export - [Date]"
   - Body: "This file contains your VegyScan data in JSON format."
   - Attachment: vegyscan-export-2025-11-16.json (47 KB)
7. User enters recipient and sends email
8. Export complete, user returns to Settings
9. Flow ends

**Use Case:** User requesting their data per GDPR Article 20.

**Example Export File:**
```json
{
  "export_date": "2025-11-16T14:30:00Z",
  "app_version": "1.0.0",
  "menus": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "date_scanned": "2025-11-15T19:00:00Z",
      "restaurant_name": "Trattoria Roma",
      "location": {"lat": 41.9028, "lng": 12.4964, "city": "Rome", "country": "Italy"},
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

### Alt-4: Open Privacy Policy

**Trigger:** User wants to review privacy practices

1. User taps **Privacy Policy** in About section
2. System opens privacy policy:
   - **Option A:** In-app web view (Safari View Controller)
   - **Option B:** External Safari browser
3. User reads privacy policy (hosted at https://vegyscan.app/privacy)
4. User closes web view
5. Returns to Settings
6. Flow ends

**Note:** Privacy policy MUST be accessible before first use (GDPR requirement). Link also shown in onboarding.

### Alt-5: Contact Support

**Trigger:** User needs help or wants to report bug

1. User taps **Contact Support**
2. System opens iOS Mail composer pre-filled:
   - To: support@vegyscan.app
   - Subject: "VegyScan Support Request"
   - Body:
     ```
     Please describe your issue:

     [User types here]

     ---
     Device: iPhone 14 Pro
     iOS Version: 17.2
     App Version: 1.0.0 (Build 42)
     ```
3. User types issue description
4. User taps Send
5. Email sent, user returns to Settings
6. Flow ends

**Rationale:** Pre-filled device info helps support team diagnose issues.

### Alt-6: Permission Denied → Link to iOS Settings

**Trigger:** User sees "Camera: Denied" and wants to enable it

1. User taps **Camera Permission** row (shows "Denied")
2. System displays iOS alert:
   - "VegyScan does not have permission to access your camera"
   - Buttons: [Cancel] [Open Settings]
3. User taps [Open Settings]
4. iOS Settings app opens, deep-linked to **VegyScan → Permissions → Camera**
5. User toggles Camera permission ON
6. User returns to VegyScan app
7. Settings screen refreshes, shows "Camera: Allowed" (green)
8. Flow ends

**Rationale:** Apple does not allow apps to directly request permissions again if denied. Must link to Settings.

## Exception Flows

### Exc-1: Export Fails (Low Storage)

**Trigger:** Device has insufficient storage to create export file

1. User taps Export All Data
2. System attempts to create JSON file
3. iOS returns "Insufficient storage" error
4. System displays error:
   - Title: "Export Failed"
   - Message: "Not enough storage space. Free up space and try again."
   - Button: [OK]
5. User taps [OK]
6. Export cancelled, no file created
7. Flow ends

### Exc-2: Email Not Configured (Contact Support)

**Trigger:** User taps Contact Support but hasn't set up Mail app

1. User taps Contact Support
2. System tries to open Mail composer
3. iOS returns "No mail account configured"
4. System displays alternative:
   - Title: "Email Not Set Up"
   - Message: "Please email support@vegyscan.app or configure Mail app in iOS Settings."
   - Buttons: [Copy Email] [OK]
5. User taps [Copy Email]
6. System copies "support@vegyscan.app" to clipboard
7. User can paste in other email app
8. Flow ends

## Business Rules

1. **Settings saved immediately:** No "Save" button needed (iOS convention)
2. **Permission changes require iOS Settings:** App cannot directly change permissions
3. **Data retention changes apply to future:** Not retroactive
4. **Export excludes photos:** Only metadata exported (photos too large)
5. **Privacy policy must be accessible:** GDPR requirement
6. **Dietary preference optional:** Only shown if it affects app behavior (v1 may not show)
7. **Version number always visible:** Helps user report bugs with context

## UI/UX Notes

**Visual Design:**
- Grouped table view (iOS standard Settings style)
- Sections with headers: Privacy / Data Management / Preferences / About
- Right-aligned values: "90 days," "Allowed," etc.
- Disclosure arrows (›) for tappable items
- Green/red color for permission status

**Accessibility:**
- VoiceOver announces: "Camera permission: Allowed" or "Denied, tap to open Settings"
- All rows have clear labels and hints
- High contrast (REQ-NF-021)

## Performance Criteria

- Settings screen loads instantly (<  0.3s)
- Storage calculation < 0.5s (scan local DB for sizes)
- Permission status checks instant (iOS provides cached values)

## Related

- **Requirements:**
  - REQ-F-037: User Settings & Preferences (main requirement)
  - REQ-F-038: Data Export (GDPR Data Portability)
  - REQ-F-039: Delete Scan History (accessed from Data Management)
  - REQ-F-041: Auto-Delete Old Scans (retention period configured here)
  - REQ-NF-022: GDPR Compliance
  - REQ-NF-023: App Store Privacy Labels

- **Use Cases:**
  - UC-010: Delete Menu from History ("Clear All" accessed from Settings)
  - UC-008: First-Time User Onboarding ("Show Tutorial Again" future option)

- **Personas:**
  - All personas use settings
  - Anna (Strict Vegan): Most likely to review privacy policy
  - Clara (Allergy-Aware): Most likely to contact support if issues

## Notes

**Why NO "Sign Out" button:**
- v1 has no user accounts (no sign-in)
- No cloud sync
- All data local
- If v2 adds accounts, add Sign Out here

**Why dietary preference may NOT be shown in v1:**
- Currently, menus displayed same way for all users
- No filtering by dietary type in v1
- Asking for preference wastes time if not used
- Can add in v2 if we implement filtering/personalization

**Future Enhancements (v2+):**
- **App appearance:** Light / Dark / Auto (theme support)
- **Notification settings:** If we add notifications (e.g., "Menu analysis complete")
- **Default scan mode:** Camera vs Upload (if we add choice)
- **Advanced:** Cache size limit, image quality settings
- **Account management:** If v2 adds user accounts
- **Subscription management:** If v2 uses subscription model
