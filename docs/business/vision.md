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

## Strategic Scope

_For detailed features, see [Functional Requirements](./requirements/functional.md) - the Single Source of Truth for all features._

### What We're Building (High-Level)

An iOS-native app that transforms foreign-language menus into interactive, augmented experiences through:
1. **Visual preservation** - the original menu remains the center of interaction
2. **Intelligent augmentation** - translations, classifications, and insights overlaid on the original
3. **Vegan/vegetarian intelligence** - diet-specific classification with transparent reasoning
4. **Instant UX** - perceived response time < 2 seconds (lazy loading, progressive disclosure)

### What We're NOT Building (Strategic Boundaries)

**Out of scope for v1:**
- **Allergen tracking** beyond vegan/vegetarian (future v2+ consideration - complexity and liability)
- **Nutritional information** (calories, macros) - different value proposition
- **Recipe suggestions** or cooking instructions - not menu-focused
- **Web version** - iOS-only focus for v1 (leverage native capabilities)
- **Android app** - iOS-only focus for v1 (resource constraints)
- **Social sharing** with friends - privacy and complexity

**Strategic reasons:**
- **Focus on core value:** Vegan/vegetarian travelers need menu understanding, not nutritional tracking
- **Leverage iOS-native:** VisionKit, Core ML, SwiftUI capabilities maximize quality and minimize development time
- **Manage complexity:** Allergen tracking adds legal liability and requires different accuracy standards
- **Resource constraints:** Single platform initially allows faster iteration and learning

### Open Strategic Questions

_These are business/architecture decisions, not features. Features are documented in [Functional Requirements](./requirements/functional.md)._

- **Business model:** One-time purchase (€8) vs. subscription vs. freemium
  - Current assumption: €8 one-time purchase
  - Drives cost optimization requirements (REQ-NF-013: <€0.005 per page)

- **Offline capability:** Full offline vs. hybrid vs. cloud-only
  - Decision depends on: LLM cost optimization, on-device ML capabilities, cache hit rates
  - Impacts: Architecture (local ML models), storage (cache size), UX (connectivity requirements)

- **Community features:** How much to invest in shared/social aspects
  - Bonus features: Community-shared scans (REQ-F-027), user feedback (REQ-F-028)
  - Decision depends on: v1 adoption, privacy considerations, moderation costs

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
