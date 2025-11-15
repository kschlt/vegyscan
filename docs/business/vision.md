# Product Vision

> **Status:** Draft
> **Last Updated:** 2025-11-15
> **Working Names:** VegyScan / Veggie Lens / Menu Vision / GreenScan

## Vision Statement

**Transform any foreign-language menu into an interactive, digitally-enriched, vegan/vegetarian-friendly super-menu that looks exactly like the original but explains, translates, and evaluates everything.**

Take a photo of a foreign menu → instantly get an interactive, augmented version that preserves the original layout but adds intelligent overlays, translations, hotspots, and vegan/vegetarian insights.

## Problem Statement

### Who
Travelers (especially vegans, vegetarians, and people with dietary restrictions) visiting foreign countries with unfamiliar languages and food cultures.

### What Problems

**1. Language Barriers**
- Unfamiliar writing systems (Japanese, Korean, Thai, Arabic, etc.)
- Mixed-language menus with poor translations
- Translations alone don't explain what the dish actually is
- Complex menu layouts with scattered information

**2. Dietary Uncertainty**
- Hidden animal ingredients in traditional dishes
- Cooking methods (e.g., Belgian fries fried in animal fat)
- Broths made with bones/fish (Dashi, Tonkotsu)
- Local standards and traditions unknown to travelers
- Symbols and allergen info not understood

**3. Current Tools Are Inadequate**

**Google Translate Camera:**
- Doesn't recognize which texts belong together
- No menu context understanding
- No dish explanations
- No vegan/vegetarian intelligence
- No country/cultural context
- No interactivity
- Can't handle multi-page menus

**ChatGPT with Photo:**
- Delivers unstructured text output
- Loses menu visual structure
- No interactive UX
- Often slow
- Uncertain classifications without context
- Hard to use for actual ordering (you still point at the original)

## Goals

1. **Enable confident ordering** for vegans/vegetarians in any foreign restaurant
2. **Preserve visual context** while adding digital intelligence (augmented, not replaced)
3. **Be faster and more accurate** than Google Translate or ChatGPT for menu understanding
4. **Provide transparent reasoning** for vegan/vegetarian classifications
5. **Create intuitive, instant UX** that feels native to mobile dining experiences

## Scope

### In Scope

**Core Features:**
- Photo capture with image optimization (straightening, brightness, sharpening)
- Multi-page menu book (scan multiple pages, navigate like a digital menu)
- Interactive hotspots over each menu item
- **Symbol recognition** (🌱, V, allergen icons - CRITICAL)
- Meta-information bundling (group all info belonging to one dish)
- Translation to user's selected target language (ANY language, not just foreign scripts)
- Vegan/vegetarian classification with reasoning
- Confidence levels (simple 1-3 scale with legend)
- Overlay system (show/hide translations, icons, badges)
- Dish type recognition (Tonkotsu, Frikandel, Pho, etc.)
- Country/cuisine context awareness
- Favorites/marking system (mark dishes as if ordering)
- History with GPS-based restaurant matching
- Detail panel per dish (name, translation, description, ingredients, adaptations)
- Photo quality feedback ("please retake photo")
- Scanner guide lines during photo capture (iOS camera features)

**Bonus Features (Future Enhancement):**
- Order phrase generation in local language ("without fish sauce" in Japanese)
- Community-shared scans (restaurant-based menu sharing)
- Ratings/reviews (Happy Cow style)
- User feedback on vegan/vegetarian accuracy
- Named saved menus
- Restaurant suggestions based on location

### Out of Scope (for now)

- Allergen tracking beyond vegan/vegetarian (future consideration)
- Recipe suggestions or cooking instructions
- Nutritional information (calories, macros)
- Social features (sharing with friends) - bonus feature only
- Web version (iOS-only initially)
- Android app (iOS-only initially)
- Offline mode (to be decided based on technical feasibility)

### Open Questions / To Be Decided

- **Business model:** One-time purchase (€8-10) vs. time-based premium (14-day pass) vs. freemium
- **Offline capability:** Depends on LLM cost optimization and on-device processing
- **Community features:** How much to invest in shared/social aspects
- **RAG/Database strategy:** Balance between LLM queries and cached dish knowledge

## Success Criteria

**User Experience:**
- Feels "instant" (< 2 seconds perceived response time)
- User can confidently order vegan/vegetarian food in foreign restaurant
- Original menu remains center of interaction (not replaced)
- No information overload (progressive disclosure)

**Technical:**
- High accuracy symbol recognition (>95%)
- Correct meta-info bundling (all dish components grouped)
- Reliable vegan/vegetarian classification with transparent reasoning
- Cost-efficient LLM usage (maximize on-device processing)

**Business:**
- Users willing to pay for app (validates value proposition)
- Better than free alternatives (Google Translate, ChatGPT)
- Positive reviews highlighting speed, accuracy, and trust

## Target Users

_[Detailed personas in [personas.md](./personas.md)]_

**Primary:**
- Vegans and vegetarians traveling abroad
- Travelers in countries with unfamiliar writing systems
- Digital nomads and backpackers

**Secondary:**
- Flexitarians
- People with food allergies
- Anyone seeking to understand foreign menus better

**Context:**
- Active travelers (not daily use)
- Likely use case: 1-3 weeks per trip, several trips per year
- High willingness to pay during travel (part of trip budget)
