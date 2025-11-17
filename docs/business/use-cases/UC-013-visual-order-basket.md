# UC-013: Build and Show Visual Order Basket

> **ID:** UC-013
> **Status:** Draft
> **Created:** 2025-11-17
> **Last Updated:** 2025-11-17
> **Priority:** Must Have

## Actors

- **Primary:** All vegan/vegetarian travelers
- **Secondary:** Restaurant waitstaff (indirect - receives visual order)

## Preconditions

1. User has scanned a menu and analyzed dishes
2. User has reviewed dish details
3. User has identified dishes they want to order (with or without modifications)

## Business Value

**User Research Validated:** Addresses communication pain point and time-intensive workflow. Users currently piece together orders verbally across language barriers, leading to errors and anxiety.

**Quote from Research:** *"By the time I explained my needs, my friends had often finished their first drink"* - Visual order basket streamlines this entire process.

**Benefit:** One-screen order display eliminates back-and-forth, reduces mistakes, provides clear communication across language barriers.

## Main Flow (Happy Path)

1. User is viewing analyzed Thai menu
2. User opens detail panel for "Pad Thai"
3. App shows:
   ```
   🟡 Pad Thai (#24)
   ผัดไทย

   Usually contains:
   ❌ Egg
   ❌ Fish sauce

   💬 Suggested modification:
   "Can you make this without egg and fish sauce?
   Use soy sauce instead."
   ```
4. User reviews modification question
5. User taps "Add to Order Basket" button
6. App adds Pad Thai with modifications to basket
7. App shows confirmation: "✓ Added to order basket"
8. User continues browsing menu
9. User opens detail panel for "Som Tam" (Papaya Salad)
10. App shows:
    ```
    🟡 Som Tam (#15)
    ส้มตำ

    Usually contains:
    ❌ Fish sauce
    ❌ Dried shrimp

    💬 Suggested modification:
    "Can you make this without fish sauce and dried shrimp?"
    ```
11. User taps "Add to Order Basket"
12. User opens detail panel for "Mango Sticky Rice"
13. App shows:
    ```
    🟢 Mango Sticky Rice (#28)
    ข้าวเหนียวมะม่วง

    ✓ Usually vegan
    ⚠️ Confirm coconut milk has no dairy added

    Confidence: ⚫⚫⚫ High
    ```
14. User taps "Add to Order Basket"
15. User taps "Order Basket" icon in navigation (shows badge: "3")
16. App displays Order Basket screen showing all 3 dishes with modifications
17. User reviews order, sees it's complete
18. User taps "Show Order to Waiter" button
19. App enters full-screen mode
20. App displays professionally-formatted order slip in both Thai and English:
    ```
    ┏━━━━━━━━━━━━━━━━━━━━━━━━━┓
    ┃    📋 MY ORDER           ┃
    ┃    คำสั่งของฉัน          ┃
    ┣━━━━━━━━━━━━━━━━━━━━━━━━━┫
    ┃                          ┃
    ┃  ① #24 ผัดไทย             ┃
    ┃     (Pad Thai)           ┃
    ┃     🚫 ไม่ใส่ไข่          ┃
    ┃        (No egg)          ┃
    ┃     🚫 ไม่ใส่น้ำปลา       ┃
    ┃        (No fish sauce)   ┃
    ┃     ✅ ใส่ซีอิ๊ว          ┃
    ┃        (Use soy sauce)   ┃
    ┃                          ┃
    ┃  ② #15 ส้มตำ             ┃
    ┃     (Papaya Salad)       ┃
    ┃     🚫 ไม่ใส่กุ้งแห้ง     ┃
    ┃        (No dried shrimp) ┃
    ┃     🚫 ไม่ใส่น้ำปลา       ┃
    ┃        (No fish sauce)   ┃
    ┃                          ┃
    ┃  ③ #28 ข้าวเหนียวมะม่วง  ┃
    ┃     (Mango Sticky Rice)  ┃
    ┃     ✅ เจ (Vegan)         ┃
    ┃     ⚠️ ตรวจสอบกะทิไม่มี  ┃
    ┃        นมโค              ┃
    ┃     (Confirm coconut milk┃
    ┃      has no dairy)       ┃
    ┃                          ┃
    ┣━━━━━━━━━━━━━━━━━━━━━━━━━┫
    ┃   ขอบคุณมากครับ/ค่ะ 🙏  ┃
    ┃   (Thank you very much)  ┃
    ┗━━━━━━━━━━━━━━━━━━━━━━━━━┛
    ```
20. User holds phone to show waiter
21. Waiter reads order clearly, understands all modifications
22. Waiter repeats order to confirm
23. User taps outside full-screen to exit, or taps "Done" button
24. → Use case ends successfully

## Alternative Flows

### Alt-1: Edit Order Before Showing

**Branches from:** Step 16 in Main Flow

1. User reviews order basket
2. User decides to remove Som Tam
3. User swipes left on Som Tam item
4. App shows "Delete" button
5. User taps delete
6. App removes Som Tam from basket
7. Basket now shows 2 items (Pad Thai + Mango Sticky Rice)
8. → Returns to step 17 in Main Flow

### Alt-2: Modify Modification Before Showing

**Branches from:** Step 16 in Main Flow

1. User reviews order basket
2. User taps on "Pad Thai" item to edit
3. App returns to Pad Thai detail panel
4. User adjusts modifications (decides to keep egg but still no fish sauce)
5. User taps "Update in Order Basket"
6. App updates Pad Thai in basket with new modifications
7. → Returns to step 16 in Main Flow

### Alt-3: Add Dish Without Modifications

**Branches from:** Step 13 in Main Flow

1. Mango Sticky Rice is already vegan (green status)
2. User taps "Add to Order Basket"
3. App adds dish WITHOUT modification questions
4. Order basket shows:
   ```
   ③ #28 Mango Sticky Rice
      ✅ Vegan
      ⚠️ Confirm coconut milk (no dairy)
   ```
5. → Continues to step 15

### Alt-4: Save Order for Future Visit

**Branches from:** Step 17 in Main Flow

1. User is satisfied with order
2. User taps "Save Order for This Restaurant"
3. App prompts: "Save this order for [Restaurant Name]?"
4. User confirms
5. App saves order with:
   - Restaurant location (GPS)
   - Ordered dishes
   - All modifications
   - Date saved
6. App shows confirmation: "Order saved! Next time you're here, you can reuse it."
7. → Returns to step 18 in Main Flow

### Alt-5: Load Saved Order

**Precondition:** User previously saved an order at this restaurant

**Branches from:** Step 1 in Main Flow

1. User scans menu at previously-visited restaurant
2. App detects GPS match with saved location
3. App shows notification:
   ```
   💚 You visited this restaurant before!

   Last time you ordered:
   • Pad Thai (no egg, no fish sauce)
   • Mango Sticky Rice

   [Load Previous Order] [Start Fresh]
   ```
4. User taps "Load Previous Order"
5. App pre-populates Order Basket with saved items
6. → Jumps to step 15 in Main Flow (user can review/edit loaded order)

### Alt-6: Copy Order Text

**Branches from:** Step 19 in Main Flow (full-screen order display)

1. User wants to paste order into another app (e.g., message to friend)
2. User long-presses on order display
3. App shows "Copy Order Text" option
4. User taps "Copy"
5. App copies formatted order to clipboard
6. User can paste in Messages, Notes, etc.
7. → Use case ends

### Alt-7: Share Order with Travel Companion

**Branches from:** Step 16 in Main Flow

1. User traveling with friend
2. User taps "Share" button in Order Basket
3. App shows iOS Share Sheet
4. User selects "Messages" and friend's contact
5. App shares order as text:
   ```
   My order at [Restaurant]:
   1. Pad Thai (no egg, no fish sauce, use soy sauce)
   2. Som Tam (no dried shrimp, no fish sauce)
   3. Mango Sticky Rice (vegan, confirm coconut milk)
   ```
6. Friend receives order, can add their own items
7. → Use case ends

## Exception Flows

### Exc-1: Empty Order Basket

**Occurs when:** User taps "Order Basket" without adding any items (Step 15)

1. Order basket is empty
2. App displays empty state:
   ```
   📋 Order Basket

   Your order basket is empty.

   Browse the menu and tap "Add to Order Basket"
   on dishes you want to order.

   [Back to Menu]
   ```
3. User taps "Back to Menu"
4. → Use case ends (user needs to add items first)

### Exc-2: Network Error While Loading Saved Order

**Occurs when:** App tries to load saved order but local database fails (Alt-5, Step 5)

1. App encounters error retrieving saved order
2. App shows error message:
   ```
   ⚠️ Couldn't load saved order

   Please start fresh this time.

   [OK]
   ```
3. User taps OK
4. Order Basket remains empty
5. → Returns to step 2 in Main Flow (user builds order manually)

### Exc-3: Waiter Can't Read Display (Too Bright/Dark)

**Occurs when:** Lighting conditions make screen hard to read (Step 20)

1. Restaurant is very dark
2. Waiter squints at bright screen
3. User taps "Adjust Brightness" button (in full-screen mode)
4. App toggles between:
   - High contrast (white background, black text)
   - Night mode (dark background, large white text)
5. User selects night mode
6. Waiter can now read easily
7. → Returns to step 21 in Main Flow

## Postconditions

**Success:**
- Order basket contains user's selected dishes with all modifications
- Visual order displayed in both local language and English
- Waiter clearly understands complete order
- User avoided lengthy verbal explanation
- Communication error risk minimized
- Time to order reduced from 10+ minutes to <2 minutes

**Partial Success (Alt-5):**
- Saved order loaded and reused
- User didn't need to rebuild order from scratch
- Return visit experience streamlined

## Related Requirements

- [REQ-F-044: Dish Modification Question Generator](../requirements/functional.md#req-f-044-dish-modification-question-generator)
- [REQ-F-045: Visual Order Basket](../requirements/functional.md#req-f-045-visual-order-basket)
- [REQ-F-052: Celebratory Messaging](../requirements/functional.md#req-f-052-celebratory-messaging--positive-ux)

## User Research Evidence

**Pain Point Addressed:**
- Time-Intensive Workflow (High): *"By the time I explained my needs, my friends had often finished their first drink"*
- Language Barrier (Critical): *"It was difficult to convey what I was trying to avoid"*

**User Quotes:**
- *"I tried 'no egg, no dairy, no meat' at each meal but typically found myself surprised"* - Visual order ensures nothing is forgotten
- *"Other times I had to resign to eating my surprise-dairy meal because... the chef was becoming unhappy with me"* - Clear visual order prevents chef frustration

**Behavioral Pattern:** Multi-Tool Workflow - Consolidates communication into one visual display instead of juggling translation apps + phrasebooks.

## Success Metrics

- 60%+ of users use Order Basket when ordering at restaurants
- Average ordering time reduced from 10 min to <3 min
- User reports: "Waiter understood immediately"
- Reduction in "food arrived wrong" incidents
- Increase in user confidence when ordering

## User Experience Notes

**Visual Design Principles:**
- Restaurant slip aesthetic (professional, familiar to waitstaff)
- Large, readable text (waiter viewing from arm's length)
- Clear hierarchy (numbered list, visual separation)
- Both languages visible (waiter can read native, user can verify English)
- Icons (🚫, ✅, ⚠️) transcend language barriers
- Polite closing message (cultural respect)

**Accessibility:**
- Brightness adjustment for different lighting conditions
- High contrast mode for visibility
- Large touch targets for editing
- Clear feedback for all actions

## Notes

**Critical for MVP:** YES - This is a core communication tool that directly addresses user pain.

**Localization:** Message formatting must adapt to language (right-to-left for Arabic, etc.)

**Future Enhancement:** Voice dictation to add custom modifications not suggested by app.

**Testing Priority:** Must test with real waitstaff in target countries to ensure visual format is intuitive and professional.
