# UC-004: Mark Favorites and Save Menu to History

> **ID:** UC-004
> **Status:** Draft
> **Created:** 2025-11-15
> **Last Updated:** 2025-11-15

## Actors

- **Primary:** [Sarah the Vegan Backpacker](../personas.md#sarah-vegan-backpacker), [Emma & Tom the Adventure Travelers](../personas.md#emma-tom-adventurers)
- **Secondary:** Any user wanting to remember dishes or restaurants

## Preconditions

1. User has scanned a menu (UC-001 or UC-002 completed)
2. User has viewed dish details (UC-003)
3. App has location permissions (optional, for GPS-based restaurant matching)

## Main Flow (Happy Path)

### Part A: Mark Dish as Favorite

1. User views dish detail panel (UC-003, step 3)
2. User finds a dish they want to remember/order
3. User taps "Favorite" icon (heart/star) in detail panel
4. App marks dish as favorite (icon fills in/changes color)
5. App saves favorite with: dish name, menu photo reference, restaurant context
6. → User can continue viewing other dishes

### Part B: Auto-Save Menu to History

7. User finishes viewing menu (closes app or navigates away)
8. App automatically saves menu scan to history with:
   - Menu photo(s) (optimized version + hotspot data)
   - Scan date/time
   - GPS location (if permission granted)
   - **Auto-detected restaurant name** (from menu OCR or GPS lookup)
   - All favorited dishes linked to this menu
9. If GPS is available:
   - App checks if location matches known restaurant (Google Places API)
   - App prompts: "Are you at [Restaurant Name]?"
   - User confirms or edits restaurant name
10. Menu is saved to history list
11. → Use case ends successfully

## Alternative Flows

### Alt-1: User Manually Names Menu

**Branches from:** Step 9 in Main Flow

1. User does not confirm auto-detected restaurant name
2. User taps "Edit Name"
3. User enters custom name (e.g., "Cozy ramen place near station")
4. App saves with user-provided name
5. → Returns to step 10

### Alt-2: Mark Multiple Dishes as Favorites

**Branches from:** Step 3 in Main Flow

1. User marks first dish as favorite
2. User closes detail panel, opens another dish
3. User marks second dish as favorite
4. Process repeats for 3rd, 4th dish, etc.
5. All favorites linked to this menu scan
6. → Returns to step 6

### Alt-3: Unfavorite Dish

**Branches from:** Step 3 in Main Flow

1. User has already favorited a dish
2. User opens that dish detail panel again
3. User taps filled favorite icon
4. App removes favorite status (icon becomes outline)
5. → Returns to step 6

### Alt-4: No GPS Permission (Manual Location)

**Branches from:** Step 8 in Main Flow

1. User has not granted GPS permission
2. App cannot auto-detect restaurant
3. App shows: "Add restaurant name?" (optional field)
4. User can:
   - Enter name manually
   - Skip (save as "Menu from [Date]")
5. → Returns to step 10

## Exception Flows

### Exc-1: Duplicate Restaurant Detected

**Occurs when:** GPS matches a restaurant user has scanned before (Step 9)

1. App detects same GPS location as previous scan
2. App prompts: "You scanned a menu here on [Previous Date]. Same restaurant?"
3. User confirms
4. App links both scans to same restaurant
5. User can now see "Previous scans" when viewing this menu in history
6. → Returns to step 10

### Exc-2: GPS Lookup Fails

**Occurs when:** Network error during Google Places API call (Step 9)

1. App cannot fetch restaurant name from GPS
2. App saves menu with GPS coordinates only
3. Restaurant name shows as "Unknown Location"
4. User can edit later from history
5. → Returns to step 10

## Postconditions

### Success
- Dish is marked as favorite (if user chose to)
- Menu scan is saved to history
- Menu is linked to restaurant (via GPS or manual name)
- User can access saved menus later
- Favorites are easily identifiable within saved menus

### Failure
- Menu may save without restaurant link (if GPS failed)
- Favorites still saved, but restaurant context may be missing

## Business Rules

- **BR-001** All menu scans are automatically saved to history (no explicit "Save" needed)
- **BR-002** Favorites are per-dish, not per-menu (same dish can be favorited in multiple restaurants)
- **BR-003** GPS matching uses ~50m radius to identify same restaurant
- **BR-004** History is stored locally on device (not cloud, for v1)
- **BR-005** Maximum 100 menus in history (configurable, oldest auto-deleted)
- **BR-006** Restaurant names are editable after initial save
- **BR-007** Favorited dishes should be visually prominent when viewing saved menus

## Related Artifacts

- **Requirements:**
  - [REQ-F-015: Favorite Marking](../requirements/functional.md#req-f-015)
  - [REQ-F-016: Auto-Save to History](../requirements/functional.md#req-f-016)
  - [REQ-F-017: GPS Restaurant Matching](../requirements/functional.md#req-f-017)
  - [REQ-F-018: History Management](../requirements/functional.md#req-f-018)
  - [REQ-NF-004: Local Storage](../requirements/non-functional.md#req-nf-004)
- **User Stories:** [US-006](../user-stories/stories.md#us-006), [US-007](../user-stories/stories.md#us-007)
- **Related Use Cases:**
  - [UC-003: View dish details](./UC-003-view-dish-details.md)
  - [UC-002: Multi-page menu](./UC-002-create-multi-page-menu-book.md)

## Notes

### Favorite Icon Design
- Unfavorited: Outline heart/star (⭐️ → ☆)
- Favorited: Filled heart/star (☆ → ⭐️)
- Subtle animation on tap (scale + color change)

### GPS Privacy
- Must respect user privacy settings
- Clear messaging: "GPS helps identify restaurants for history"
- Allow full functionality without GPS (manual naming)

### History UI
- Sorted by date (newest first)
- Group by restaurant (if multiple scans at same place)
- Show thumbnail of menu + restaurant name + date
- Tap to re-open interactive menu view

### Bonus Features (Future)
- Share favorited dishes with friends
- Export history (PDF, JSON)
- Cloud sync (cross-device history)
- Community: "Others scanned this restaurant too"
