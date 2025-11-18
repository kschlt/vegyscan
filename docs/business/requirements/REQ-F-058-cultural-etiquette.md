# REQ-F-058: Cultural Etiquette & Communication Intelligence

**Status:** NEW - Must Have for v1
**Priority:** Must Have (CRITICAL for user success)
**Created:** 2025-11-18
**Research Foundation:** Global Vegan Menu Scanning Challenges Research + Cultural Database YAMLs

---

## Description

System must provide culturally-appropriate communication guidance for each country/cuisine, including how to approach staff, expected language proficiency, appropriate tone/etiquette, and what responses to expect. This intelligence is stored in the Cultural Context Database and surfaced contextually throughout the app.

---

## Rationale

**User's Vision:** "Store knowledge once, use everywhere - user doesn't have to think or research."

Research shows that **HOW you ask** is as important as **WHAT you ask** for:
- **Japan:** Modifications seen as disrespectful in traditional settings - need apologetic, humble tone
- **Thailand:** Direct but friendly approach works - street vendors flexible
- **France:** Expect resistance, be persistent but polite
- **China:** Buddhist vegetarian restaurants are best - regular restaurants have limitations

**Without this intelligence:**
- Users make cultural faux pas (pushing for modifications in Japan = awkward/unsuccessful)
- Users don't know if staff will understand English
- Users don't know what responses mean ("muzukashii desu" in Japanese = polite "no")
- Users waste time asking for impossible modifications

**With this intelligence:**
- Users approach appropriately for each culture
- Realistic expectations set (Japan: find vegan restaurant vs. modify)
- Know when to use local phrases vs. English
- Understand staff responses and next steps

---

## Scope

### What This Covers

1. **How to Approach Staff**
   - Tone (polite, apologetic, direct, humble)
   - Strategy (ask for modifications vs. find vegan restaurant)
   - When to push vs. when to accept "no"

2. **Language Expectations**
   - Staff English proficiency by region (tourist areas vs. rural)
   - When translation cards are essential
   - When visual communication (pointing, gestures) helps

3. **Cultural Modification Norms**
   - Which cultures accept modifications (Thailand: high, Japan: very low)
   - Success rates by restaurant type
   - When modifications are seen as rude

4. **Communication Patterns**
   - Common positive responses ("daijōbu desu" = okay)
   - Common negative responses ("muzukashii desu" = difficult/no)
   - Uncertain responses ("kakunin shimasu" = I'll check)
   - What to do for each response

5. **Fallback Strategies**
   - What to do if staff doesn't understand
   - What to do if modifications rejected
   - Alternative dishes to try
   - When to leave and find different restaurant

---

## Data Structure (in Cultural Context Database)

Each cuisine's YAML includes:

```yaml
cultural_context:
  modification_culture:
    overall_acceptance: "VERY_LOW" | "LOW" | "MODERATE" | "HIGH" | "VERY_HIGH"

    by_restaurant_type:
      - type: "Traditional Japanese"
        acceptance_rate: 20  # 15-25%
        success_factors:
          - "High-end with English staff may try"
        limitations:
          - "Modifications seen as disrespectful"
        approach: |
          AVOID requesting modifications. Instead: Ask if they
          have dishes without dashi. Choose obviously vegan items.

  etiquette:
    how_to_ask:
      approach: "VERY POLITE, APOLOGETIC"  # or DIRECT, FRIENDLY, etc.
      tone: "Humble, apologetic for inconvenience"
      staff_english_level: "LOW_TO_MEDIUM"
      tips:
        - "Use maximum politeness: です/ます form"
        - "Apologize: 'すみません' (excuse me)"
        - "Don't demand - ask if possible"
        - "If resistant, DON'T PUSH"

    language_expectations:
      tokyo_osaka_kyoto:
        english_proficiency: "MEDIUM"
        notes: "Tourist areas: Hotels have English. Outside: very limited."

      rural_areas:
        english_proficiency: "VERY_LOW"
        notes: "Almost no English. Essential to have Japanese phrases."

    common_responses:
      positive:
        - phrase: "大丈夫です"
          transliteration: "daijōbu desu"
          meaning: "It's okay / We can do that"

      negative:
        - phrase: "難しいです"
          transliteration: "muzukashii desu"
          meaning: "It's difficult (polite no)"

      uncertain:
        - phrase: "確認します"
          transliteration: "kakunin shimasu"
          meaning: "I'll check"
```

---

## How System Uses This Intelligence

### 1. Contextual Guidance in Modification Suggestions

When user views a dish that can be modified:

**Thailand (Street Food):**
```
🍛 Pad Thai - Can Be Modified

⚠️ MODERATE Success Rate: ~70%

💡 In Thailand:
   Street vendors cook to order and are usually
   flexible with modifications. Be direct but friendly.

   Staff English: Medium in tourist areas
   Approach: Smile and ask politely

[Show Modification Questions]
```

**Japan (Traditional):**
```
🍜 Miso Soup - Contains Dashi

❌ CANNOT BE VEGANIZED

🚫 Cultural Note:
   Traditional Japanese restaurants rarely modify
   dishes. Asking is seen as disrespectful to the
   chef's intent.

   Recommendation: Find a vegan restaurant or order
   obviously vegan items (edamame, plain rice).

[Find Vegan Restaurant Nearby]
```

### 2. Communication Tips Panel

Tappable "💬 How to Ask" button on each cuisine:

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ 💬 Ordering in Japan       ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                            ┃
┃ 🎯 Approach:               ┃
┃    Be very polite and      ┃
┃    apologetic              ┃
┃                            ┃
┃ 🗣️ Staff English:         ┃
┃    LOW outside Tokyo       ┃
┃    Use Japanese phrases    ┃
┃                            ┃
┃ ✅ If they say:           ┃
┃   "大丈夫です"            ┃
┃   (daijōbu desu)          ┃
┃   → They can do it!       ┃
┃                            ┃
┃ ❌ If they say:           ┃
┃   "難しいです"            ┃
┃   (muzukashii desu)       ┃
┃   → Polite "no"           ┃
┃   Don't push further      ┃
┃                            ┃
┃ ❓ If they say:           ┃
┃   "確認します"            ┃
┃   (kakunin shimasu)       ┃
┃   → They're checking      ┃
┃   Wait patiently          ┃
┃                            ┃
┃ 💡 Pro Tip:               ┃
┃   Don't request           ┃
┃   modifications at        ┃
┃   traditional restaurants ┃
┃   → Find vegan restaurant ┃
┃   instead                 ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

### 3. Success Rate Estimates

Display realistic success rates based on:
- Country modification culture
- Restaurant type (street food vs. traditional)
- Modification difficulty (easy vs. impossible)

**Example:**
```
✅ Success Rate: ~75%
   (Thai street food usually accommodates)

⚠️ Success Rate: ~20%
   (Japanese traditional rarely modifies)
```

### 4. Smart Fallback Suggestions

If modification has low success rate or cultural barriers:

```
❌ Low Success Rate (~20%)

💡 Better Strategies:
   1. Find vegan restaurant (search "shojin ryori")
   2. Order naturally vegan items:
      • Edamame (枝豆)
      • Plain rice (白ご飯)
      • Natto (納豆)
   3. Visit temple restaurant (serves vegan food)

[Find Vegan Restaurant] [Safe Dishes]
```

### 5. Language Proficiency Indicators

Show expected staff English level for each region:

```
📍 Location: Rural Japan

🗣️ Staff English: VERY LOW
   Translation cards essential
   Use Japanese phrases
   Visual communication helps (pointing)

[View Japanese Phrases]
```

```
📍 Location: Bangkok Tourist Area

🗣️ Staff English: MEDIUM-HIGH
   Most staff understand basic English
   Thai phrases still appreciated
   "Gin jay" (เจ) widely known

[View Thai Phrases]
```

---

## Acceptance Criteria

- [ ] Each cuisine in Cultural Context Database includes complete etiquette section:
  - [ ] How to approach (approach, tone, strategy)
  - [ ] Staff English proficiency (by region)
  - [ ] Tips for asking (3-5 culturally-specific tips)
  - [ ] Common responses (positive, negative, uncertain)
  - [ ] Language expectations (tourist areas vs. rural)

- [ ] System surfaces etiquette intelligence contextually:
  - [ ] When showing modification suggestions (include cultural notes)
  - [ ] When displaying success rates (factor in cultural acceptance)
  - [ ] Via tappable "💬 How to Ask" panel

- [ ] Communication tips panel accessible for each cuisine:
  - [ ] Approach guidance
  - [ ] Staff English level
  - [ ] Common responses with translations
  - [ ] What to do for each response
  - [ ] Pro tips specific to culture

- [ ] Success rate estimates factor in:
  - [ ] Modification difficulty (Easy/Moderate/Impossible)
  - [ ] Country modification culture
  - [ ] Restaurant type
  - [ ] Display as percentage with context

- [ ] Smart fallback strategies suggested when:
  - [ ] Success rate < 40%
  - [ ] Cultural barriers exist (Japan traditional)
  - [ ] Staff doesn't understand
  - [ ] User provides alternative dishes, vegan restaurant search

- [ ] Language proficiency indicators shown:
  - [ ] Based on detected location (if available)
  - [ ] Tourist areas vs. rural distinction
  - [ ] Recommend translation cards when English very low

- [ ] All content sourced from research and cultural databases:
  - [ ] No assumed etiquette - all data-driven
  - [ ] Citations in YAML files
  - [ ] Can be updated without app update (JSON config)

---

## UX Examples

### Example 1: High Acceptance Culture (Thailand)

**Context:** User viewing Pad Thai with modifications

```
🍛 Pad Thai
❌ Contains: Egg, Fish sauce

🟡 CAN BE MODIFIED
Success Rate: ~70% ✅

💬 How to ask in Thailand:
   Be friendly and direct. Street vendors
   usually understand "gin jay" (vegan).

💡 Cultural Tip:
   Thai culture is flexible - most vendors
   cook to order and will accommodate.

[Show Thai Phrases] [Modify This Dish]
```

### Example 2: Low Acceptance Culture (Japan)

**Context:** User viewing Miso Soup

```
🍜 Miso Soup
❌ Contains: Dashi (fish stock)

🔴 CANNOT BE MODIFIED
Success Rate: ~15% ❌

🚫 Cultural Warning:
   Traditional Japanese restaurants rarely
   modify dishes. Requesting changes may
   be seen as disrespectful to the chef.

💡 Better Strategy:
   Find a vegan restaurant or order
   shojin ryori (Buddhist temple food).

[Find Vegan Restaurant] [Safe Japanese Dishes]
```

### Example 3: Staff English Guidance

**Context:** User in rural Japan

```
📍 Detected: Rural area, Japan

🗣️ Staff English: VERY LOW

💡 Communication Tips:
   • Bring translation card (essential)
   • Use Japanese phrases from VegyScan
   • Point at menu + make X gesture
   • If confused, say:
     "精進料理はありますか？"
     (Shōjin ryōri wa arimasu ka?)
     → Asking for Buddhist vegan food

[View All Japanese Phrases]
```

### Example 4: Response Interpretation

**Context:** User asked modification question, staff responded

```
💬 Staff said: "難しいです"
   (muzukashii desu)

Translation: "It's difficult"

Meaning: ❌ Polite "no"

What to do:
✅ Thank them politely
✅ Order different dish or
✅ Find vegan restaurant

❌ DON'T: Push further (culturally rude)

[Safe Dishes] [Nearby Vegan Restaurants]
```

---

## Integration with Other Requirements

**Works with:**
- **REQ-F-042:** Cultural Context Database (stores all etiquette data)
- **REQ-F-044:** Modification Question Generator (uses etiquette to format questions)
- **REQ-F-054:** Modification Feasibility (combines difficulty + cultural acceptance for success rate)
- **REQ-F-055:** Country Modification Culture (this is WHERE the etiquette is defined)

**This requirement (REQ-F-058) focuses on:**
- Making etiquette intelligence EXPLICIT in UX
- Surfacing it contextually (not hidden in database)
- Helping users communicate effectively
- Setting cultural expectations

---

## Priority Rationale

**Must Have for v1:**

1. **Prevents cultural faux pas** - Users won't unknowingly offend (Japan modifications)
2. **Increases success rate** - Knowing how to ask properly improves outcomes
3. **Reduces frustration** - Realistic expectations (don't waste time on impossible requests)
4. **Builds trust** - Shows app understands culture, not just language
5. **Differentiation** - NO competitor provides this level of cultural intelligence

**User's philosophy:** "All the tooling on hand, all the information - they don't have to do any thinking or research."

This requirement embodies that philosophy by providing **communication intelligence** alongside **ingredient intelligence**.

---

## Data Sources

All etiquette intelligence comes from:
- Global Vegan Menu Scanning Challenges Research (31 pages)
- Cultural database YAMLs (thai-cuisine.yaml, japanese-cuisine.yaml, chinese-cuisine.yaml)
- User testimonials and travel blogs
- Cultural norms research

---

## Questions for User

1. Should we show etiquette tips proactively (first scan) or only when user taps "How to Ask"?
2. Should success rates be shown as percentages (~70%) or qualitative (High/Moderate/Low)?
3. When success rate < 30%, should we HIDE the modification option entirely and only show fallbacks?

---

## Success Metrics

**How we measure if this works:**
- User feedback: "The cultural tips helped me order successfully"
- Users don't report awkward interactions (especially in Japan)
- Users understand when to find vegan restaurant vs. attempt modification
- Reduced support questions about "Why didn't the restaurant accommodate?"

---

**Related Requirements:**
- REQ-F-042: Cultural Context Database
- REQ-F-044: Modification Question Generator
- REQ-F-054: Modification Feasibility Classification
- REQ-F-055: Country Modification Culture Database

---

**Last Updated:** 2025-11-18
**Status:** NEW - Pending integration into main requirements doc
