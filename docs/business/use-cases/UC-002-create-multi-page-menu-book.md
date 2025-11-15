# UC-002: Create Multi-Page Menu Book

> **ID:** UC-002
> **Status:** Draft
> **Created:** 2025-11-15
> **Last Updated:** 2025-11-15

## Actors

- **Primary:** [Emma & Tom the Adventure Travelers](../personas.md#emma-tom-adventurers)
- **Secondary:** Any user with multi-page physical menus

## Preconditions

1. User has successfully completed at least one menu scan (UC-001)
2. Restaurant menu has multiple pages (e.g., appetizers, mains, drinks, desserts)
3. User wants to capture entire menu for comprehensive view

## Main Flow (Happy Path)

1. User completes first page scan (UC-001)
2. App displays scanned page with "Add Page" button visible
3. User flips to next physical menu page
4. User taps "Add Page" button
5. App returns to camera view
6. User captures second page (same process as UC-001, steps 3-11)
7. App processes second page and adds it to menu book
8. App shows page indicator: "Page 2 of 2" (or thumbnail strip)
9. User repeats steps 3-7 for additional pages (drinks, desserts, etc.)
10. When done, user taps "Finish" or navigates away
11. App saves complete multi-page menu book to history
12. User can swipe/navigate between pages in unified menu book view
13. → Use case ends successfully

## Alternative Flows

### Alt-1: Navigate Between Pages While Scanning

**Branches from:** Step 8 in Main Flow

1. User wants to review previously scanned page
2. User swipes left/right or taps page indicator
3. App shows selected page with all hotspots and overlays
4. User can return to camera to add more pages
5. → Returns to step 4 in Main Flow

### Alt-2: Reorder Pages

**Branches from:** Step 10 in Main Flow

1. User realizes pages are in wrong order (e.g., scanned desserts before mains)
2. User enters "Edit Menu Book" mode
3. User drags page thumbnails to reorder
4. App updates page sequence
5. → Returns to step 11 in Main Flow

### Alt-3: Delete Page

**Branches from:** Step 8 in Main Flow

1. User realizes a page was scanned incorrectly or is duplicate
2. User taps "..." menu on page thumbnail
3. User selects "Delete Page"
4. App prompts: "Remove this page from menu book?"
5. User confirms
6. App removes page and updates page numbering
7. → Returns to step 8 in Main Flow

## Exception Flows

### Exc-1: Inconsistent Menu Detected

**Occurs when:** New page doesn't match restaurant context (Step 7)

1. System detects inconsistency (e.g., different restaurant name, different language, different menu style)
2. System displays warning: "This page looks different. Is it from the same menu?"
3. User can choose:
   - "Yes, same menu" → Continue processing
   - "No, start new menu" → Create separate menu book
4. → Returns to appropriate flow based on choice

### Exc-2: Maximum Pages Exceeded

**Occurs when:** User tries to add more than reasonable page limit (Step 4)

1. System detects user has scanned 10+ pages (configurable limit)
2. System displays message: "Menu book is getting large. Consider creating a new one."
3. User can choose:
   - "Continue" → Allow more pages (up to hard limit of 20)
   - "Finish" → Save current menu book
4. → Flow ends or returns to step 11

## Postconditions

### Success
- Multi-page menu book is created with all scanned pages
- Pages are in correct order (or user-reordered)
- User can navigate between pages seamlessly
- Each page has independent hotspots and overlays
- Menu book is saved to history with restaurant info
- Menu book has unified metadata (restaurant name, location, date)

### Failure
- Partial menu book may exist
- User can retry or delete incomplete book

## Business Rules

- **BR-001** All pages in a menu book must be associated with same restaurant/session
- **BR-002** Pages retain individual processing (hotspots per page, not merged)
- **BR-003** Maximum 20 pages per menu book (performance consideration)
- **BR-004** Page navigation must be smooth (< 0.3s transition)
- **BR-005** Menu book is atomic unit in history (deleted/shared together)

## Related Artifacts

- **Requirements:**
  - [REQ-F-006: Multi-Page Menu Support](../requirements/functional.md#req-f-006)
  - [REQ-F-007: Page Navigation](../requirements/functional.md#req-f-007)
  - [REQ-F-008: Menu Book Management](../requirements/functional.md#req-f-008)
  - [REQ-NF-002: Page Transition Performance](../requirements/non-functional.md#req-nf-002)
- **User Stories:** [US-003](../user-stories/stories.md#us-003)
- **Related Use Cases:**
  - [UC-001: Scan single page](./UC-001-scan-single-page-menu.md)
  - [UC-004: Save to history](./UC-004-mark-favorites-and-save-history.md)

## Notes

- Page thumbnails should show miniature version of optimized menu photo
- Swiping is primary navigation (familiar mobile gesture)
- Consider page labels: "Appetizers", "Mains", "Drinks" (auto-detected or user-labeled)
- Menu book metadata should include: restaurant name (auto-detected or manual), GPS location, date/time
- "Finish" button vs. automatic detection of end (e.g., user leaves camera view)
