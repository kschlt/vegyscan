# UC-012: Access Cultural Context and Use Smart Vegan Passport

> **ID:** UC-012
> **Status:** Draft
> **Created:** 2025-11-17
> **Last Updated:** 2025-11-17
> **Priority:** CRITICAL (Killer Feature)

## Actors

- **Primary:** [Anna (Strict Vegan)](../personas.md#strict-vegan-anna), All vegan/vegetarian travelers
- **Secondary:** First-time travelers to foreign countries

## Preconditions

1. User has installed VegyScan app
2. User has scanned a menu OR opened app in new location
3. App has detected country/cuisine context from menu language or GPS
4. Cultural Context Database downloaded for detected region

## Business Value

**User Research Validated:** This addresses Pain Point #1 (Hidden Ingredients) and #2 (Cultural Gaps), the most severe pain points identified in user research.

**Quote from Research:** *"I tried 'no egg, no dairy, no meat' at each meal but typically found myself surprised by an unwanted ingredient I hadn't thought of."*

**Competitive Advantage:** NO competitor offers country/cuisine-specific dietary intelligence. This is the primary differentiator.

## Main Flow (Happy Path)

1. User scans Thai restaurant menu
2. App detects language: Thai
3. App identifies cuisine: Thai
4. App automatically displays "Cultural Context" panel with expand/collapse button
5. User taps to expand Cultural Context panel
6. App displays Thai-specific information (based on deep research Nov 2025):
   ```
   💡 You're in Thailand

   ⚠️ Watch out for (research-validated):
   • Fish sauce (น้ำปลา / nam pla) - in MOST dishes, even "vegetarian"
   • Shrimp paste (กะปิ / kapi) - in curry pastes and sauces
   • Oyster sauce (น้ำมันหอย / sot hoi nang rom) - common in stir-fries

   ℹ️ Research insight: "I asked if the curry was vegetarian and they said yes,
   but it had fish sauce. I didn't know I needed to specifically ask."

   🌱 Look for these local dishes:
   • Mango Sticky Rice (ข้าวเหนียวมะม่วง) - usually vegan
   • Som Tam Jay (ส้มตำเจ) - vegan papaya salad (ask: no fish sauce)
   • Pad Pak Ruam (ผัดผักรวม) - mixed veg stir-fry (verify oil, no oyster sauce)

   💬 Useful phrases (research-validated):
   "กินเจ ไม่ใส่น้ำปลา ไม่ใส่หอยนางรม"
   (Gin jay, mai sai nam pla, mai sai sot hoi nang rom)
   = I eat vegan (jay), no fish sauce, no oyster sauce

   "ไม่ใส่ไข่" (Mai sai khai) = No egg

   💡 Tip: In Thailand, "เจ" (Jay) means Buddhist vegan
   food. During Thai Vegetarian Festival (Tesagan Gin Jay),
   many places serve truly vegan food marked with a special symbol.

   📚 Source: Deep research analysis of 50+ vegan traveler stories (Nov 2025)
   ```
7. User reads context information
8. User decides to use Smart Vegan Passport
9. User taps "Vegan Passport" button in navigation
10. App displays Vegan Passport screen
11. App shows pre-configured settings:
    - Dietary profile: Vegan (all boxes checked except honey - user's preference)
    - Auto-detected language: Thai
    - Culturally-adapted message generated
12. User reviews generated message in both Thai and English
13. User taps "Show to Waiter" button
14. App displays full-screen vegan passport:
    ```
    ┌─────────────────────────────┐
    │   🌱 VEGAN PASSPORT          │
    ├─────────────────────────────┤
    │                              │
    │ 🇹🇭 ดิฉัน/ผมทานอาหารเจ      │
    │  ไม่ทานเนื้อสัตว์ ทุกชนิด   │
    │  ไม่ทานไข่ นม ปลา และ       │
    │  อาหารทะเล                   │
    │                              │
    │  คุณช่วยแนะนำอาหารที่        │
    │  ฉันทานได้ไหมคะ/ครับ        │
    │                              │
    │ 🇬🇧 I eat vegan food.        │
    │  I don't eat:                │
    │  🥩 Meat                     │
    │  🐟 Fish & Seafood           │
    │  🥚 Eggs                     │
    │  🥛 Dairy products           │
    │                              │
    │  Can you help me find        │
    │  something I can eat?        │
    │                              │
    │   ขอบคุณครับ/ค่ะ 🙏         │
    │   (Thank you)                │
    │                              │
    └─────────────────────────────┘
    ```
15. User shows phone to waiter
16. Waiter reads message, understands "เจ" (Jay) concept
17. Waiter suggests dishes from "Jay" section of kitchen
18. → Use case ends successfully

## Alternative Flows

### Alt-1: User Customizes Vegan Passport

**Branches from:** Step 11 in Main Flow

1. User taps "Edit Dietary Restrictions"
2. App shows customization screen
3. User unchecks "Honey" (follows beekeeping ethics, eats honey)
4. User checks custom item: "Onion/Garlic" (Jain dietary restriction)
5. App updates generated message to exclude honey, add alliums
6. → Returns to step 12 in Main Flow

### Alt-2: Different Cultural Context (Japan)

**Branches from:** Step 4 in Main Flow

1. App detects Japanese menu
2. App displays Japan-specific context:
   ```
   💡 You're in Japan

   ⚠️ Watch out for:
   • Dashi (だし) - fish stock in EVERYTHING
   • Katsuobushi (かつお節) - bonito flakes
   • Mirin (みりん) - may contain fish

   🌱 Look for these:
   • Edamame (枝豆) - steamed soybeans
   • Natto (納豆) - fermented soybeans
   • Shojin Ryori (精進料理) - Buddhist vegan cuisine

   💬 Useful phrase:
   "Dashi wa haitte imasuka?" = Does this have dashi?

   💡 Tip: "Vegan" is NOT widely understood.
   Explain what you DON'T eat instead of using
   the word "vegan".
   ```
3. Smart Vegan Passport adapts:
   - Uses FULL explanation instead of just "vegan"
   - Adds specific items: "no dashi, no katsuobushi"
   - Message format adjusted for Japanese cultural norms
4. → Continues to step 7

### Alt-3: User Accesses Context Without Scanning

**Branches from:** Preconditions

1. User opens app in new city (Bangkok)
2. User hasn't scanned menu yet
3. User taps "Cultural Tips" in main menu
4. App detects location via GPS
5. App shows country selector: "You appear to be in Thailand. Is this correct?"
6. User confirms
7. → Returns to step 6 in Main Flow (displays Thai context)

### Alt-4: Multi-Cuisine Restaurant

**Branches from:** Step 3 in Main Flow

1. Menu contains both Thai and Japanese dishes
2. App detects mixed cuisine
3. App displays both cultural contexts with tabs:
   - [Thai Context] [Japanese Context]
4. User can switch between tabs to see relevant info
5. → Continues to step 7

## Exception Flows

### Exc-1: Cultural Context Not Available

**Occurs when:** Database doesn't have info for detected country (Step 4)

1. App detects menu in Mongolian language
2. Cultural Context Database doesn't include Mongolia
3. App displays generic message:
   ```
   💡 Cultural Context

   ⚠️ Common hidden ingredients to ask about:
   • Meat broths or stocks
   • Animal fats (butter, lard, ghee)
   • Fish sauce or fish-based seasonings
   • Eggs (in batters, breads, pasta)
   • Dairy (milk, cream, cheese)

   💬 Tip: Show your Vegan Passport to explain
   your dietary needs clearly.
   ```
4. Smart Vegan Passport still works (uses generic template)
5. → Use case continues (user can still use passport)

### Exc-2: Offline Mode - Context DB Not Downloaded

**Occurs when:** User is offline and hasn't pre-downloaded regional pack (Step 4)

1. App cannot access Cultural Context Database (no internet, no cached data)
2. App displays notification:
   ```
   📡 Offline Mode

   Cultural context for this region isn't
   downloaded yet.

   [Download Thailand Pack] (when online)

   Your Vegan Passport still works!
   ```
3. App shows basic Vegan Passport functionality
4. Cultural context features disabled until download
5. → Use case ends (partial success - passport works, no cultural tips)

### Exc-3: Wrong Country Detected

**Occurs when:** GPS or language detection incorrect (Step 3)

1. User is in Thai restaurant in New York
2. App detects Thai language, assumes user is in Thailand
3. App shows Thai context (which is still relevant for Thai food)
4. User notices GPS shows New York
5. User can manually override: "I'm actually in: [Country selector]"
6. App asks: "Keep Thai cultural context for this menu?"
7. User confirms (yes, Thai restaurant context is relevant)
8. → Returns to step 6 (Thai context shown, but location corrected)

## Postconditions

**Success:**
- User has accessed relevant cultural dietary information
- User understands hidden ingredients to watch for in this cuisine
- User knows local vegan dishes to ask about
- User has culturally-appropriate vegan explanation ready to show staff
- User's anxiety reduced (has actionable information and tools)

**Failure (Exc-2):**
- Cultural context unavailable (offline, no download)
- But Vegan Passport still functions
- User can use generic dietary communication

## Related Requirements

- [REQ-F-042: Cultural Context Database](../requirements/functional.md#req-f-042-cultural-context-database)
- [REQ-F-043: Smart Vegan Passport](../requirements/functional.md#req-f-043-smart-vegan-passport)

## User Research Evidence

**Pain Point Addressed:**
- Hidden Ingredients (Critical): *"Strictly 'vegetable' soups usually had egg throughout them"*
- Language/Cultural Gap (Critical): *"If you say you're vegan, lots of people won't understand"*

**User Quotes:**
- *"I spent a few hours Googling 'vegan in [Country X]'... figure out the most common non-vegan ingredients"* - This feature eliminates hours of research
- *"I recommend getting a vegan passport... you can show your waiters so they understand"* - Digital version is smarter and always available

**Behavioral Pattern:** Multi-Tool Workflow - This feature consolidates research, phrasebooks, and Vegan Passport into one tool.

## Success Metrics

- 80%+ of users access Cultural Context panel when traveling
- 60%+ use Smart Vegan Passport at least once per trip
- User feedback: "This feature alone is worth it"
- Reduction in reported "surprise animal ingredients" incidents
- Increase in users trying local dishes (vs defaulting to fries)

## Notes

**Critical for MVP:** YES - This is the #1 differentiator from competitors. Without this, VegyScan is just another translation app.

**Database Requirements:** Must cover top 20 vegan travel destinations before launch.

**Offline Priority:** Cultural Context must work offline (pre-downloaded regional packs).

**Extensibility:** Community should be able to contribute context updates in future versions.
