# UC-009: View Scan History

> **ID:** UC-009
> **Status:** Draft
> **Created:** 2025-11-16
> **Last Updated:** 2025-11-16

## Actors

- **Primary:** [Anna (Strict Vegan)](../personas.md#strict-vegan-anna), [Emma (Pescatarian)](../personas.md#pescatarian-emma)
- **Secondary:** All users who have scanned menus

## Preconditions

1. User has previously scanned at least one menu (or none - empty state)
2. App is installed and running on iOS device

## Postconditions

**Success:**
- User views list of previously scanned menus
- User can tap any menu to reopen it in full interactive view
- User can search/filter history to find specific menus

**Failure:**
- N/A (viewing history is non-destructive, cannot fail)

## Main Flow (Happy Path)

1. User opens VegyScan app
2. User taps "History" tab/icon in main navigation
3. System displays **Scan History** screen showing all menus in reverse chronological order (newest first)
4. For each menu, system displays:
   - **Thumbnail:** First page of menu (or placeholder if multi-page)
   - **Restaurant name:** From GPS matching (REQ-F-019) or "Unknown Restaurant" if no GPS
   - **Location:** City, Country (if GPS available) or "No location"
   - **Date scanned:** "Today 2:30 PM", "Yesterday", "Nov 14", "Oct 3, 2024", etc.
   - **Page count:** "3 pages" (if multi-page) or hidden (if single page)
   - **Favorite indicator:** Star icon (if menu contains favorited dishes)
5. User scrolls through history
6. User taps on a menu entry
7. System reopens menu in full interactive view (same as UC-001 result)
   - Menu photo displayed with hotspots
   - User can tap dishes to see details (UC-003)
   - User can swipe between pages if multi-page (UC-002)
8. User navigates back to history (back button)
9. User is back on Scan History screen

**Use Case: User Revisits Restaurant**
- Anna scanned Trattoria Roma menu last week
- Today, she's planning dinner
- Opens History → sees Trattoria Roma → taps to view
- Remembers the Pasta Pomodoro was vegan → decides to return

## Alternative Flows

### Alt-1: Empty History (No Scans Yet)

**Trigger:** User has never scanned a menu

1. User taps "History" tab
2. System displays empty state screen:
   - Icon: Empty folder/menu icon
   - Heading: "No scanned menus yet"
   - Body: "Scan your first menu to see it here"
   - Button: [Scan Menu Now]
3. User taps [Scan Menu Now]
4. System navigates to camera (UC-001)
5. Flow ends

### Alt-2: Search History by Restaurant Name

**Trigger:** User wants to find specific restaurant

1. User is on Scan History screen
2. User taps search bar at top
3. User types "Roma"
4. System filters list in real-time:
   - Shows only menus matching "Roma" in restaurant name
   - "Trattoria Roma" appears
   - "Roma Pizza" appears
   - Other menus hidden
5. User taps "Trattoria Roma"
6. System reopens that menu
7. Flow ends

### Alt-3: Search History by Dish Name

**Trigger:** User remembers dish but not restaurant

1. User types "Carbonara" in search bar
2. System searches:
   - All scanned menus
   - All recognized dish names within menus
3. System displays results:
   - "Trattoria Roma - Pasta Carbonara" (Nov 14)
   - "Osteria Napoli - Spaghetti Carbonara" (Oct 20)
4. User taps result
5. System opens menu and highlights/scrolls to that dish
6. Flow ends

**Strategic Value:** Helps users remember "I had something great but can't remember where"

### Alt-4: Filter History by Date Range

**Trigger:** User wants to see menus from recent trip

1. User taps "Filter" icon on Scan History screen
2. System displays filter options:
   - **Date Range:** Last Week / Last Month / Last 3 Months / All Time
   - **Location:** (List of cities with scans)
   - **Favorites Only:** Toggle
3. User selects "Last Month"
4. System filters to show only menus from last 30 days
5. User sees filtered list
6. User can clear filter to see all again

### Alt-5: Filter by Location (GPS-Based)

**Trigger:** User wants to see all menus from Paris trip

1. User taps "Filter" → Location
2. System displays cities where menus were scanned (from GPS data):
   - "Paris, France (12 menus)"
   - "Rome, Italy (8 menus)"
   - "Berlin, Germany (5 menus)"
   - "No location (3 menus)"
3. User selects "Paris, France"
4. System shows only 12 menus scanned in Paris
5. User can browse Paris menus
6. Flow ends

### Alt-6: View Favorites Only

**Trigger:** User wants to see menus with saved favorites

1. User taps "Filter" → toggle "Favorites Only"
2. System shows only menus containing at least one favorited dish
3. User sees subset of history (only menus with favorites)
4. User can toggle off to see all menus again

## Exception Flows

### Exc-1: Data Corruption (Menu Unreadable)

**Trigger:** Menu data corrupted or photo file deleted

1. User taps corrupted menu in history
2. System detects missing photo or corrupted data
3. System displays error: "This menu cannot be displayed (data corrupted)"
   - Options: [Delete This Menu] [Cancel]
4. User can delete corrupted entry or cancel
5. Flow ends

**Rationale:** Rare but possible (storage corruption, manual file deletion).

### Exc-2: Search Returns No Results

**Trigger:** User searches for non-existent restaurant/dish

1. User searches "Sushi"
2. System finds no matches
3. System displays:
   - "No menus found for 'Sushi'"
   - "Try a different search term"
4. User clears search or tries new term
5. Flow ends

## Business Rules

1. **Reverse chronological order:** Newest scans always at top (most recent are most relevant)
2. **GPS matching determines restaurant name:** Uses REQ-F-019 logic
3. **Menus without GPS shown in history:** Appear with "Unknown Restaurant" label
4. **Auto-delete old scans:** Menus older than retention period (default 90 days) automatically removed (REQ-F-041)
5. **Favorited dishes indicator:** Star icon if menu contains ≥1 favorited dish
6. **Search real-time:** Results update as user types (no "Search" button needed)

## UI/UX Notes

**List View Design:**
- Each menu entry is a card (tappable)
- Thumbnail on left (square, ~80x80pt)
- Restaurant name prominent (bold, larger font)
- Location and date secondary (smaller, gray text)
- Page count badge on thumbnail (if multi-page)
- Favorite star in top-right of card (if has favorites)

**Performance:**
- Lazy loading: Load 20 menus initially, load more on scroll
- Thumbnail caching: Fast scroll performance
- Search debounced: Wait 300ms after typing before searching

**Accessibility:**
- VoiceOver announces: "Trattoria Roma, Paris France, scanned November 14, 3 pages, has favorites"
- Large tap targets (minimum 44x44pt per iOS HIG)
- High contrast between text and background (REQ-NF-021)

## Performance Criteria

- History screen loads in < 0.5s (even with 100+ menus)
- Scroll performance: 60fps
- Search results appear within 200ms of last keystroke
- Thumbnails load progressively (no blank placeholders for >1s)

## Related

- **Requirements:**
  - REQ-F-040: View Scan History
  - REQ-F-020: Local History Storage
  - REQ-F-019: GPS-Based History Matching
  - REQ-F-021: Favorite Dishes
  - REQ-F-041: Auto-Delete Old Scans

- **Use Cases:**
  - UC-001: Scan Single-Page Menu (creates history entries)
  - UC-002: Create Multi-Page Menu Book (creates history entries)
  - UC-004: Mark Favorites and Save to History (favorited dishes)
  - UC-010: Delete Menu from History (user can remove entries)

- **Personas:**
  - Anna: Uses history to remember vegan-friendly restaurants for return visits
  - Emma: Uses search to find "that great fish dish I had somewhere"

## Notes

**Future Enhancements (v2+):**
- **Sort options:** By date, by location, by restaurant name, by favorites
- **Manual restaurant naming:** User can rename "Unknown Restaurant" entries
- **Photo editing:** User can crop/rotate menu photos in history
- **Share menu:** Share menu photo + classifications with friends
- **Statistics:** "You've scanned 47 menus across 8 cities!"

**Why GPS matching matters:**
- Without GPS: All menus show as "Unknown Restaurant" (poor UX)
- With GPS: Automatic restaurant detection via REQ-F-019 (excellent UX)
- EXIF GPS from photos critical for upload/share use cases (REQ-F-035)
