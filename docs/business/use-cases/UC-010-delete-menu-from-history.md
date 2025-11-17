# UC-010: Delete Menu from History

> **ID:** UC-010
> **Status:** Draft
> **Created:** 2025-11-16
> **Last Updated:** 2025-11-16

## Actors

- **Primary:** All users with scan history
- **Secondary:** N/A

## Preconditions

1. User has at least one scanned menu in history
2. User is viewing Scan History screen (UC-009)

## Postconditions

**Success:**
- Selected menu permanently deleted from device storage
- Menu removed from history list
- Associated photos deleted from local storage
- Cache entries removed
- Storage space freed

**Failure:**
- Deletion cancelled (user chose "Cancel" in confirmation)
- System error during deletion (rare - file system error)

## Main Flow (Happy Path) - Delete Individual Menu

1. User is on Scan History screen (UC-009)
2. User sees list of scanned menus
3. User **long-presses** on a menu entry (e.g., "Trattoria Roma, Nov 14")
4. System displays context menu with options:
   - **[Delete Menu]**
   - [Cancel]
5. User taps [Delete Menu]
6. System displays confirmation dialog:
   - Title: "Delete this menu?"
   - Message: "This will permanently delete the menu and all associated data. This cannot be undone."
   - Buttons: [Cancel] [Delete]
7. User taps [Delete]
8. System performs deletion:
   - Remove menu metadata from local database (SQLite)
   - Delete menu photo files from device storage
   - Remove OCR text data
   - Remove classification results
   - Remove cache entries for this menu
   - Update favorites list (if menu had favorited dishes)
9. System removes menu from history list (fade-out animation)
10. System displays brief confirmation: "Menu deleted" (toast message, 2 seconds)
11. History list updates to show remaining menus
12. Flow ends

**Use Case: Managing Storage**
- User has scanned 50+ menus
- Device storage low
- User reviews history and deletes old/irrelevant menus
- Storage freed, app remains performant

## Alternative Flows

### Alt-1: Swipe to Delete (iOS Pattern)

**Trigger:** User familiar with iOS swipe-to-delete pattern

1. User is on Scan History screen
2. User **swipes left** on a menu entry
3. System reveals [Delete] button in red
4. User taps [Delete]
5. System displays same confirmation dialog (Step 6 from main flow)
6. User confirms → menu deleted
7. Flow continues as main flow from Step 8

**Rationale:** Follows iOS platform conventions (Mail, Messages, etc.).

### Alt-2: Delete from Menu Detail View

**Trigger:** User viewing menu in full screen, decides to delete

1. User has opened menu from history (full interactive view)
2. User taps **menu icon** (⋮) in top-right corner
3. System displays menu with options:
   - [Share Menu]
   - [Rename Restaurant] (future)
   - **[Delete Menu]**
4. User taps [Delete Menu]
5. System displays confirmation dialog (same as Step 6 main flow)
6. User confirms → menu deleted
7. System navigates back to Scan History screen
8. Menu no longer appears in list
9. Flow ends

### Alt-3: Clear All History (Bulk Delete)

**Trigger:** User wants to delete ALL scanned menus at once

1. User opens **Settings** screen (UC-011)
2. User navigates to **Data Management** section
3. User taps [Clear All Scan History]
4. System displays confirmation dialog:
   - Title: "Delete all scanned menus?"
   - Message: "This will permanently delete all X menus and free up Y MB of storage. Favorites will also be deleted. This cannot be undone."
   - Buttons: [Cancel] [Delete All]
5. User taps [Delete All]
6. System shows progress indicator (if many menus): "Deleting menus... 23/47"
7. System performs bulk deletion:
   - Delete all menu metadata from database
   - Delete all menu photo files
   - Clear all cache
   - Clear all favorites
   - Reset history
8. System displays confirmation: "All menus deleted"
9. User navigates to History → sees empty state
10. Flow ends

**Use Case: Fresh Start**
- User returning from long trip (100+ scans)
- Wants to clear history before next trip
- Uses "Clear All" for quick reset

### Alt-4: User Cancels Deletion

**Trigger:** User taps [Delete] but changes mind

1. User long-presses menu
2. User taps [Delete Menu]
3. System displays confirmation dialog
4. User taps [Cancel]
5. Dialog dismissed, no changes made
6. Menu remains in history
7. Flow ends

**Rationale:** Prevents accidental deletion. Confirmation dialog is critical safety net.

## Exception Flows

### Exc-1: Deletion Fails (File System Error)

**Trigger:** System unable to delete files (rare - storage corruption, iOS error)

1. User confirms deletion
2. System attempts to delete menu
3. File system returns error (e.g., "Permission denied," "File not found")
4. System displays error message:
   - Title: "Deletion Failed"
   - Message: "Unable to delete menu. Please try again."
   - Button: [OK]
5. User taps [OK]
6. Menu remains in history (not deleted)
7. User can try again or contact support

**Rationale:** Rare but possible (device issues). Transparent error messaging.

### Exc-2: Menu Already Deleted (Race Condition)

**Trigger:** Auto-delete (REQ-F-041) removes menu while user viewing history

1. User is viewing history
2. Auto-delete runs in background (menu exceeded retention period)
3. User tries to delete same menu manually
4. System detects menu no longer exists
5. System silently removes from UI (no error shown)
6. History list updates
7. Flow ends

**Rationale:** Handle gracefully without confusing user.

### Exc-3: Last Remaining Menu Deleted

**Trigger:** User deletes only menu in history

1. User has exactly 1 menu in history
2. User deletes it (following main flow)
3. System deletes menu successfully
4. History list now empty
5. System displays **empty state** (see UC-009 Alt-1):
   - "No scanned menus yet"
   - "Scan your first menu to see it here"
6. Flow ends

## Business Rules

1. **Deletion is permanent:** No "undo" or "recycle bin" - deleted menus cannot be recovered
2. **Confirmation required:** Always show confirmation dialog (prevent accidents)
3. **Favorited dishes deleted with menu:** Favorites tied to menu, not global
4. **Auto-delete after retention period:** REQ-F-041 automatically deletes old menus (default: 90 days)
5. **User preferences NOT deleted:** Clearing history does NOT delete app settings (dietary preference, retention period, etc.)
6. **GDPR compliance:** Deletion fulfills "Right to Erasure" (REQ-NF-022, REQ-F-039)

## UI/UX Notes

**Confirmation Dialog Design:**
- **Clear, prominent warning:** "This cannot be undone"
- **Destructive action in red:** [Delete] button red color (iOS convention)
- **Safe action emphasized:** [Cancel] button bold/blue
- **Storage info (for Clear All):** Show space to be freed ("Y MB")

**Feedback:**
- Brief toast message: "Menu deleted" (2 seconds)
- Smooth animation: Fade out deleted entry
- No loading spinner for single delete (instant feel)
- Progress indicator for bulk delete (if >20 menus)

**Accessibility:**
- VoiceOver announces: "Menu deleted" after successful deletion
- Confirmation dialog fully accessible
- High contrast on destructive buttons (REQ-NF-021)

## Performance Criteria

- Single menu deletion completes in < 0.5s
- Bulk deletion (100 menus): < 5s with progress indicator
- UI remains responsive during deletion
- No lag when returning to history list

## Related

- **Requirements:**
  - REQ-F-039: Delete Scan History (main requirement)
  - REQ-NF-022: GDPR Compliance (Right to Erasure - Article 17)
  - REQ-F-041: Auto-Delete Old Scans (automated version of this UC)
  - REQ-F-020: Local History Storage

- **Use Cases:**
  - UC-009: View Scan History (where deletion is accessed)
  - UC-011: Manage Settings & Preferences ("Clear All" accessed from here)

- **Personas:**
  - All personas use this feature to manage storage and privacy

## Notes

**Why Confirmation Dialog is Critical:**
- Deletion is permanent (no cloud backup in v1)
- Photos may have sentimental value (travel memories)
- Prevents accidental deletion from swipe gesture

**Future Enhancements (v2+):**
- **Archive instead of delete:** Move to "Archived" folder instead of deleting
- **Export before delete:** Offer to export data before deletion
- **Selective deletion:** Delete photos but keep metadata/favorites
- **Undo with timeout:** "Menu deleted. Undo?" with 5-second window

**Privacy Considerations:**
- Deletion removes ALL traces of menu from device
- Important for users who scanned menus at sensitive locations
- GDPR "Right to Erasure" legally required
