# UC-014: Switch Between Photo and Text View with Filtering

> **ID:** UC-014
> **Status:** Draft
> **Created:** 2025-11-17
> **Last Updated:** 2025-11-17
> **Priority:** Must Have

## Actors

- **Primary:** All vegan/vegetarian travelers
- **Secondary:** Restaurant waitstaff (when user points at menu)

## Preconditions

1. User has scanned a menu
2. Menu has been analyzed (OCR, translation, classification complete)
3. App has detected multiple menu items (at least 5)

## Business Value

**User Research Validated:** Users have different preferences - some want clean text lists for quick scanning, others need to point at original menu for waiter. Providing both views with seamless switching maximizes usability.

**Quote from Research:** *"I use Google Lens to translate, but then I need to point at the actual dish on the menu to show the waiter."*

**Benefit:** Combines best of both worlds - fast digital filtering PLUS visual reference for ordering.

## Main Flow (Happy Path)

1. User has scanned Thai restaurant menu with 30 items
2. App completes analysis and displays Photo View (default)
3. Photo View shows:
   - Original menu photo (optimized)
   - Interactive hotspots on each dish
   - Color-coded badges (green/yellow/red)
   - Toggle button: [📄 Text View]
4. User wants to quickly see only vegan options
5. User taps [📄 Text View] toggle at top
6. App transitions to Text View (<300ms smooth animation)
7. Text View displays:
   ```
   ════════════════════════════════
   MENU - Thai Kitchen
   ════════════════════════════════

   Filter: [All (30)] [Vegan (8)] [Vegetarian (12)]
           [Can Modify (5)]

   Sort: [Menu Order ▼]

   ────────────────────────────────
   🟢 #12 Mango Sticky Rice
      ข้าวเหนียวมะม่วง
      ฿120 | ⚫⚫⚫ High Confidence
      [View Details →]

   🟡 #24 Pad Thai
      ผัดไทย
      ฿180 | ⚫⚫◯ Moderate
      ⚙️ Can be modified
      [View Details →]

   🟢 #15 Som Tam Jay
      ส้มตำเจ
      ฿90 | ⚫⚫⚫ High Confidence
      🌍 Local Specialty
      [View Details →]

   [... 27 more items ...]
   ────────────────────────────────
   ```
8. User taps [Vegan (8)] filter
9. App filters list in real-time
10. Text View now shows only 8 vegan items
11. User scrolls through vegan-filtered list
12. User sees "Som Tam Jay" (local specialty) and wants to order it
13. User taps on "Som Tam Jay" item
14. Dish detail panel opens (over Text View):
    ```
    🟢 Som Tam Jay (#15)
    ส้มตำเจ
    ฿90

    🌍 THAI LOCAL SPECIALTY

    Traditional vegan papaya salad
    Shredded papaya, tomatoes, peanuts,
    lime dressing

    ✓ This is the vegan version ("Jay")
    No fish sauce, no dried shrimp

    Confidence: ⚫⚫⚫ High

    [Add to Order Basket]
    [View in Photo →]
    ```
15. User wants to show this dish to waiter on original menu
16. User taps [View in Photo →] button
17. App switches to Photo View
18. Photo View automatically:
    - Centers on Som Tam Jay item
    - Highlights/zooms the item (spotlight effect)
    - Dims surrounding items slightly
19. User points phone at waiter showing highlighted menu item
20. Waiter sees: "Oh, Som Tam Jay, number 15!" and writes it down
21. User taps [📋 Text View] to return
22. App returns to filtered Text View (Vegan filter still active)
23. App maintains scroll position
24. User continues browsing filtered vegan options
25. → Use case ends successfully

## Alternative Flows

### Alt-1: Sort Options in Text View

**Branches from:** Step 7 in Main Flow

1. User in Text View with all items shown
2. User taps [Sort: Menu Order ▼] dropdown
3. App shows sorting options:
   ```
   Sort by:
   • Menu Order (default)
   • Safest First ⭐
   • Local Dishes First
   • Your Favorites
   • By Confidence Level
   • Price: Low to High
   • Price: High to Low
   ```
4. User selects "Safest First"
5. App re-sorts list:
   ```
   🟢 SAFEST OPTIONS (95%+ confidence)
   ├─ #12 Mango Sticky Rice
   ├─ #15 Som Tam Jay
   └─ #28 Vegetable Spring Rolls

   🟡 LIKELY VEGAN (can be modified)
   ├─ #24 Pad Thai
   └─ #33 Green Curry

   🔴 CONTAINS ANIMAL PRODUCTS
   ├─ #18 Tom Yum Soup
   └─ ...
   ```
6. User quickly scans safest options first
7. → Returns to step 11 in Main Flow

### Alt-2: Multiple Filters Combined

**Branches from:** Step 8 in Main Flow

1. User has applied [Vegan] filter (8 items shown)
2. User wants to see only local vegan dishes
3. User taps additional filter: [Local Dishes Only]
4. App applies both filters
5. Text View shows: "Showing 3 items: Vegan + Local"
6. Only local vegan dishes displayed:
   - Som Tam Jay
   - Mango Sticky Rice
   - Khao Niao (Sticky Rice with vegetables)
7. → Continues to step 11

### Alt-3: Quick Toggle Without Transition

**Branches from:** Step 16 in Main Flow

1. User in Text View detail panel
2. User taps [View in Photo →]
3. App instantly shows Photo View with highlighted dish
4. User shows to waiter
5. User wants to return to text filtering
6. User taps [📋 Text View] toggle
7. App instantly returns to Text View (filtered state preserved)
8. No re-loading, seamless switching
9. → Returns to step 22

### Alt-4: Search Within Menu

**Branches from:** Step 7 in Main Flow

1. User in Text View with 30 items
2. User taps search icon
3. Search bar appears at top
4. User types "rice"
5. App filters to items containing "rice" in name/description:
   - Mango Sticky Rice
   - Fried Rice
   - Rice Noodles
   - Sticky Rice
6. User clears search
7. Full list returns
8. → Continues to step 8

### Alt-5: Direct Open Detail from Photo View

**Branches from:** Step 2 in Main Flow

1. User in Photo View (default)
2. User taps hotspot on "Som Tam Jay" directly in photo
3. Detail panel opens (same as step 14)
4. User taps [View in Photo →] in detail panel
5. App highlights the exact item user just tapped (confirmation)
6. → Use case continues

## Exception Flows

### Exc-1: No Items Match Filter

**Occurs when:** User applies filter with zero results (Step 8)

1. User taps [Vegan] filter
2. Menu has zero vegan items detected
3. App shows empty state in Text View:
   ```
   🌱 No vegan items detected

   Here are some options:
   • Check [Can Modify] filter for dishes
     that can be made vegan
   • Use your Vegan Passport to ask staff
   • Tap Cultural Tips for local vegan dishes
     to request

   [Can Modify (5)] [Cultural Tips] [Clear Filter]
   ```
4. User taps [Can Modify (5)]
5. App shows 5 modifiable items
6. → Use case continues

### Exc-2: Menu Items Have No Numbers

**Occurs when:** Menu doesn't use item numbers (Step 7)

1. Menu is analyzed but no item numbers detected
2. Text View displays without numbers:
   ```
   🟢 Mango Sticky Rice
      ข้าวเหนียวมะม่วง
      ฿120
   ```
3. When user taps [View in Photo →]:
   - App highlights item by position/name
   - No number to reference, but visual highlight still works
4. User points at highlighted area
5. Waiter can see highlighted dish
6. → Use case continues (slightly less precise but functional)

### Exc-3: Photo View Zoom/Highlight Fails

**Occurs when:** Technical issue prevents zoom effect (Step 18)

1. User taps [View in Photo →]
2. App switches to Photo View but zoom/highlight fails
3. App shows entire menu without highlight
4. App displays tooltip:
   ```
   📍 Som Tam Jay is in the Salads section,
   middle of the page.

   [OK]
   ```
5. User manually locates item on menu
6. Still better than having no reference
7. → Use case ends (degraded but functional)

### Exc-4: Very Large Menu (100+ items)

**Occurs when:** Menu has excessive items (Step 7)

1. Menu has 120 items (multi-page menu)
2. Text View implements pagination:
   ```
   Showing 1-20 of 120 items

   [Filter] [Sort]

   [... items ...]

   [Load More (100 remaining)]
   ```
3. User applies [Vegan] filter
4. Filtered to 15 items (all loaded at once)
5. Performance remains smooth
6. → Use case continues

## Postconditions

**Success:**
- User successfully filtered menu to relevant items
- User quickly found desired dish in Text View
- User showed exact dish to waiter in Photo View
- Ordering completed accurately and efficiently
- User experience was seamless between both views

**Partial Success:**
- Filters worked but zoom/highlight failed (Exc-3)
- User still able to order but less precise visual reference

## Related Requirements

- [REQ-F-013: Interactive Hotspots](../requirements/functional.md#req-f-013-interactive-hotspots)
- [REQ-F-046: Digitalized Menu View with Smart Filtering](../requirements/functional.md#req-f-046-digitalized-menu-view-with-smart-filtering)
- [REQ-F-047: Prioritized Safe Sorting](../requirements/functional.md#req-f-047-prioritized-safe-sorting)
- [REQ-F-048: Local Dish Highlighting](../requirements/functional.md#req-f-048-local-dish-highlighting)

## User Research Evidence

**Pain Point Addressed:**
- Multi-Tool Workflow (High): Users juggle Google Translate + pointing at menu. This combines both.
- Decision Fatigue (High): Filtering reduces cognitive load. User doesn't scan 30 items mentally.

**User Quotes:**
- *"I use Google Translate camera but then need to show the physical menu to order"* - Dual view solves this
- *"By the time I translated everything I forgot which ones were safe"* - Filtering shows only safe items

**Behavioral Pattern:** Safety Bubble - Users default to "safe foods". Filtering enables this mental categorization visually.

## Success Metrics

- 70%+ users toggle to Text View at least once per menu scan
- 40%+ use filtering feature
- 50%+ use "View in Photo" to show waiter
- Average decision time reduced from 5 min to <2 min
- User feedback: "Filtering is game-changer"

## User Experience Notes

**Visual Design:**
- Smooth transitions (<300ms) between views
- Filter pills with counts: [Vegan (8)] shows how many items
- Active filter highlighted (green background)
- Scroll position maintained when switching views
- Detail panel works in both views identically

**Interaction Design:**
- Filters toggle (tap again to deselect)
- Multiple filters combine (AND logic)
- Sort maintains filter state
- Search works with filters
- Clear visual feedback for all actions

**Performance:**
- Text View loads instantly (no network calls)
- Filtering is client-side (immediate)
- Photo View caches highlighted positions
- No lag when switching views (pre-rendered)

## Notes

**Critical for MVP:** YES - This addresses core user need to both analyze AND order from menu.

**Technical Challenge:** Highlight/zoom accuracy depends on OCR bounding box precision. Must be tested extensively.

**Accessibility:** Ensure text size is adjustable for low vision users. VoiceOver support for iOS.

**Future Enhancement:**
- Split-screen mode (Photo + Text simultaneously)
- Picture-in-picture (text overlay on photo)
- AR mode (point camera, see live vegan overlay)
