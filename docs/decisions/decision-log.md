# Decision Log

> **Last Updated:** 2025-11-15

Chronological record of significant decisions across all domains.

**Format:** Newest first (reverse chronological)

---

## 2025-11-15: Define Comprehensive Error Handling Strategy

**Type:** Product / UX / Technical

**Decision:** Created comprehensive error handling specification with reusable message library, retry logic strategies, and graceful degradation patterns.

**Problem/Opportunity:**
- Needed consistent error messages across all use cases (not random LLM-generated messages)
- Required clear retry strategies (automatic vs manual, exponential backoff)
- Permission denials should degrade gracefully (not block entire app)
- Multiple error categories need different handling (user errors vs transient failures)

**Solution Created:**

**1. Error Categories Defined:**
- Category 1: User Input Issues (no auto-retry: poor photo, permission denied)
- Category 2: Technical Failures (auto-retry 3x: network errors, API timeouts)
- Category 3: System Limitations (inform + workaround: handwritten menu, unsupported scenario)
- Category 4: Critical Errors (log + generic message: bugs, unexpected states)

**2. Retry Logic Strategy:**
```
Automatic Retries (Transient Errors):
Retry 1: Wait 1 second  → Retry
Retry 2: Wait 2 seconds → Retry
Retry 3: Wait 4 seconds → Retry
If all fail: Display error to user with manual retry option

No Automatic Retries (User Errors):
- Poor photo quality, permission denied, invalid input
- Immediate feedback with actionable guidance
```

**3. Message Library Created (MSG-XXX-YYY codes):**
- MSG-OCR-001: OCR Failed (No Text Recognized)
- MSG-NET-001: Network Error (General)
- MSG-PROC-001: Processing Error (Unexpected)
- MSG-QUALITY-001: Photo Quality Too Poor
- MSG-PERM-CAM-001: Camera Permission Denied
- MSG-PERM-PHOTO-001: Photos Permission Denied
- MSG-STORAGE-001: Device Storage Full
- Plus additional messages for edge cases

**4. Graceful Permission Degradation:**
- Camera denied → Upload + Share Extension still work
- Photos denied → Camera + Share Extension still work
- Location denied → Feature disabled silently (no error shown)

**5. OCR Failure Handling:**
- Complete failure: Inform user with actionable guidance
- Partial success: Show visual feedback (recognized text with hotspots, unrecognized areas grayed out)

**6. Network Failure Handling:**
- OCR succeeds (on-device) → LLM API fails → automatic retry
- All retries fail → cache locally → "Save for Later" option
- User can retry from history when connection restored

**Strategic Impact:**
- **Consistent UX:** Same messages for same errors across all flows
- **LLM agent friendly:** Pre-defined messages prevent random error text
- **User-friendly:** Actionable guidance (not technical jargon)
- **Resilient:** Automatic recovery from transient errors
- **Privacy:** Feature degradation allows app to work without all permissions

**Use Cases Updated:**
- UC-001 to UC-007: Exception flows reference MSG-XXX-YYY codes
- UC-006 and UC-007: Comprehensive permission handling documented

**Detailed Documentation:**
- [error-handling.md](../business/requirements/error-handling.md) - Complete error handling specification
- All use cases now reference error-handling.md for exception flows

**Status:** Active

---

## 2025-11-15: Document Photo Upload and Share Extension Use Cases

**Type:** Product / Documentation

**Decision:** Created UC-006 (Upload from Photo Library) and UC-007 (iOS Share Extension) with detailed flows, error handling, and strategic rationale.

**Artifacts Created:**

**1. UC-006: Upload Menu Photo from Photo Library**
- Main flow with EXIF GPS extraction (never current GPS)
- Alternative flows: Permission handling, Google Maps upload, adding pages to existing menu
- Exception flows: OCR failure (on-device VisionKit), network errors with retry logic, photo quality issues
- Business rules: Photos permission optional, EXIF GPS only, network auto-retry
- Pre-visit planning use case documented

**2. UC-007: Share Menu Photo from Other App (iOS Share Extension)**
- Google Maps pre-visit planning workflow (killer feature scenario)
- Friend sharing via Messages/WhatsApp
- Alternative flows: Share from Photos/Safari/Messages, multi-photo share, duplicate detection
- Exception flows: Extension crash, network errors, unsupported file type
- Technical implementation notes: App Groups, lightweight extension, Share Sheet integration

**Strategic Value Documented:**
- **Google Maps integration:** View menu photo → Share to VegyScan → Analyze options → Decide where to eat (competitive advantage)
- **Viral potential:** Friends share menus asking "Is this vegan-friendly?"
- **Use case expansion:** From "at restaurant" to "pre-visit trip planning"
- **Privacy-friendly:** No location permission needed for Share Extension

**Use Cases README Updated:**
- Added explanation of Requirements vs Use Cases (SoT clarity)
- Use Cases = HOW (procedural flows), Requirements = WHAT (declarative features)
- Clarified complementary nature (not duplicates)

**Detailed Documentation:**
- [UC-006-upload-menu-photo.md](../business/use-cases/UC-006-upload-menu-photo.md)
- [UC-007-share-from-other-app.md](../business/use-cases/UC-007-share-from-other-app.md)
- [use-cases/README.md](../business/use-cases/README.md) - Updated with UC-006, UC-007

**Status:** Active

---

## 2025-11-15: Add Photo Upload & iOS Share Extension Integration

**Type:** Feature / Product

**Decision:** Added photo upload from library and iOS Share Extension integration as core features, dramatically expanding use case from "at restaurant" to "pre-visit trip planning."

**Problem/Opportunity:**
- Original design only supported in-app camera capture
- User may have already taken menu photos, or found them online (Google Maps, restaurant websites)
- iOS Share Sheet integration enables seamless workflow from other apps
- **Game changer:** User can analyze menus BEFORE visiting restaurant (trip planning use case)

**New Features Added:**

1. **REQ-F-032: Upload from Photo Library** (Must Have)
   - Upload single or multiple photos from device library
   - Same processing pipeline as camera capture
   - Enables pre-visit planning, friend sharing, offline preparation
   - Location from EXIF data only (see REQ-F-035)

2. **REQ-F-033: Add Page to Existing Menu** (Must Have)
   - Clear UX: "Scan New Menu" vs "Add Page to This Menu"
   - Add pages via camera OR upload
   - Prevents user confusion, flexible workflow

3. **REQ-F-034: iOS Share Extension** (Should Have - Killer Feature)
   - VegyScan appears in iOS Share Sheet for photos
   - Works from Photos, Safari, Google Maps, Messages, WhatsApp, etc.
   - Tapping "Share → VegyScan" opens app and processes photo instantly
   - **CRITICAL:** Enables Google Maps integration (view menu photo → share → analyze → decide where to eat)
   - No location tagging for shared photos (see REQ-F-035)

4. **REQ-F-035: Smart Location Tagging** (Must Have - CRITICAL)
   - Camera capture: Use EXIF GPS if available, fallback to current GPS
   - Upload/Share: Use EXIF GPS ONLY, never current GPS
   - Prevents false location tagging (e.g., home GPS for Google Maps shares)
   - Privacy-friendly: No location permission needed for upload/share
   - Menus without location still saved (just not GPS-matched)

**Use Case Expansion:**

**Before:** User at restaurant → take photo → analyze menu → order
**After:** User planning trip → browse Google Maps → find menu photo → share to VegyScan → see vegan options → decide which restaurant to visit → arrive prepared

**Strategic Impact:**
- **Expands TAM:** From "people currently at restaurants" to "people planning restaurant visits"
- **Viral potential:** Friends share menus ("Is this place vegan-friendly?")
- **Competitive moat:** Google Translate and ChatGPT don't have Share Extension integration
- **Increased engagement:** Users interact with app during trip planning (days/weeks before trip), not just during meals
- **Pre-visit confidence:** Users know vegan options exist before walking into restaurant

**User Stories:**
- US-032: Upload Menu Photos
- US-033: Add Pages Flexibly
- US-034: Share from Any App (Google Maps integration)

**Technical Notes:**
- Share Extension requires separate iOS extension target
- Uses App Groups for communication between extension and main app
- Photo library access requires PhotoKit framework
- Extension should be lightweight (hand off to main app quickly)
- **Location tagging:** iOS ImageIO framework extracts EXIF GPS data
- Current GPS via Core Location (camera only, not upload/share)

**Detailed Documentation:**
- [REQ-F-032](../business/requirements/functional.md#req-f-032) - Upload from Photo Library
- [REQ-F-033](../business/requirements/functional.md#req-f-033) - Add Page to Existing Menu
- [REQ-F-034](../business/requirements/functional.md#req-f-034) - iOS Share Extension
- [REQ-F-035](../business/requirements/functional.md#req-f-035) - Smart Location Tagging
- [US-032 to US-034](../business/user-stories/stories.md) - User stories for iOS integration

**Status:** Active

---

## 2025-11-15: Enforce Single Source of Truth - Remove Feature Lists from Vision

**Type:** Process / Documentation

**Decision:** Removed detailed feature lists from vision.md and enforced strict Single Source of Truth (SoT) principle across all documentation.

**Problem Identified:**
- vision.md contained "Core Features" and "Bonus Features" lists (lines 60-89)
- Adding a new feature required updating vision.md + functional.md + possibly use-cases/user-stories
- This violated SoT principle - same information in multiple places
- User feedback: "If I add a new feature, I have to update it in many places"

**Changes Made:**

1. **vision.md refactored:**
   - ❌ Removed: "Core Features" list (detailed features)
   - ❌ Removed: "Bonus Features" list
   - ✅ Kept: High-level "What We're Building" (strategic, not detailed)
   - ✅ Kept: "What We're NOT Building" (strategic boundaries with WHY)
   - ✅ Kept: "Open Strategic Questions" (business decisions, not features)
   - ✅ Added: Clear reference to functional.md as SoT for features

2. **Root .claude.md updated:**
   - Fixed ownership table (vision.md is SoT for WHY, not WHAT features)
   - Added CRITICAL note: "vision.md is NOT the SoT for features!"
   - Clarified: functional.md is SoT for ALL features

3. **business/.claude.md updated:**
   - Clarified vision.md responsibilities (WHY, not feature lists)
   - Added CRITICAL note: "If you add a new feature, update functional.md ONLY"
   - Separated functional.md and non-functional.md responsibilities

**New Information Ownership:**

| Information Type | SoT Location | Update When Adding Feature |
|-----------------|--------------|----------------------------|
| WHY (problem, vision, goals) | vision.md | ❌ No change |
| WHAT features | functional.md | ✅ Add REQ-F-XXX |
| HOW users interact | use-cases/ | ✅ Add/update UC-XXX (if needed) |
| WHY users need it | user-stories/ | ✅ Add US-XXX (if needed) |

**Impact:**
- **Adding a feature now requires updating ONLY functional.md** (plus optional use-case/user-story)
- vision.md remains stable (only updates when strategic direction changes)
- Eliminates documentation drift and duplication
- Reinforces SoT principle across all domains

**Detailed Changes:**
- [vision.md](../business/vision.md) - Removed feature lists, kept strategic scope
- [.claude.md](../.claude.md) - Fixed ownership table
- [business/.claude.md](../business/.claude.md) - Clarified responsibilities

**Status:** Active

---

## 2025-11-15: Refine Personas - Purpose-Driven Structure

**Type:** Business / UX

**Decision:** Refined persona set from 8 to 7 personas with explicit "Purpose in Design" structure, clearer literacy levels, and actionable UX implications.

**Key Changes:**
1. **Added:** Sarah (Social/Flexible Vegetarian) - tests lowest-detail UI, "don't overwhelm" constraints
2. **Enhanced:** Ben (now "Health-Oriented Vegan") - added health metadata needs (fried/fresh tags)
3. **Enhanced:** Clara (merged with Grace) - now comprehensive allergy + vegan persona
4. **Removed:** Fabian (Flexitarian) - replaced by Sarah (clearer vegetarian focus)
5. **Removed:** Grace (Allergy-Only) - merged into Clara (allergen testing + vegan use case)
6. **Kept:** Emma (Pescatarian) - valuable for fish vs. meat distinction, future icon system

**New Structure for Each Persona:**
- **Purpose in Design:** What this persona tests (accuracy, information layering, classification nuance, safety)
- **Profile:** Demographics, motivation, literacy level, confidence threshold
- **Domain Knowledge:** What they know vs. don't know (tests edge case detection)
- **Implications for Requirements:** Functional + Non-functional requirements driven by this persona
- **UX Needs:** Default view, warning style, progressive disclosure, tolerance for uncertainty
- **Test Cases:** Specific dishes that test this persona's boundaries

**Literacy Levels Defined:**
- **Expert:** Anna, Clara (deep knowledge, zero tolerance for uncertainty)
- **High:** David (knows hidden fish/meat in broths, sauces)
- **Intermediate:** Ben (knows obvious issues, not edge cases)
- **Medium:** Eric, Emma (surface-level awareness, doesn't research deeply)
- **Low:** Sarah (knows obvious meat only, easily overwhelmed)

**Information Layering Guidance:**
- **Anna, Clara:** Default expanded view (show all details upfront)
- **Ben, David, Emma:** Default collapsed, expandable on demand
- **Eric:** Simple overview (won't expand details)
- **Sarah:** Minimal view (hide everything except yes/no/maybe)

**Impact:** Personas are now directly actionable for requirements definition, architecture design, and UX patterns. Each persona has clear "test purpose" - no mode switching, personas test requirements.

**Detailed Documentation:**
- [personas.md](../business/personas.md) - Complete rewrite with 7 optimized personas

**Status:** Active

---

## 2025-11-15: Critical Cost Constraint - Aggressive Caching Required

**Type:** Business / Architecture

**Decision:** Refined LLM cost target from €0.05 per scan to €0.005 per page (10x reduction) based on business model analysis. Added three CRITICAL functional requirements for cost optimization: menu duplicate detection, dish-level caching, and smart result retrieval.

**Business Model Analysis:**
- App price: €8.00, App Store fee (30%): €2.40, Available margin: €5.60
- Holiday scenario: User scans 100 pages
- At €0.05/page: €5.00 in LLM costs → **Business unprofitable**
- At €0.005/page: €0.50 in LLM costs → **Business viable** (9% of revenue)

**Key Architectural Implications:**
1. **REQ-F-029:** Menu duplicate detection (perceptual hashing, GPS context)
2. **REQ-F-030:** Dish-level caching (normalized matching, fuzzy text matching)
3. **REQ-F-031:** Smart result retrieval (multi-level cache hierarchy: L1-L4)
4. **Target:** 70%+ cache hit rate for returning users
5. **UX Impact:** "You scanned this menu 2 days ago. Use previous results?" prompts

**Cost Optimization Strategies:**
- First scan at restaurant: €0.01 cost (full processing)
- Subsequent scans: €0.00 cost (cache hit)
- 100-page trip with 50% revisits: €0.50 instead of €1.00

**Detailed Documentation:**
- [REQ-NF-013](../business/requirements/non-functional.md#req-nf-013) - Updated cost target
- [REQ-F-029](../business/requirements/functional.md#req-f-029) - Menu duplicate detection
- [REQ-F-030](../business/requirements/functional.md#req-f-030) - Dish-level caching
- [REQ-F-031](../business/requirements/functional.md#req-f-031) - Smart result retrieval
- [US-029 to US-031](../business/user-stories/stories.md) - Cost optimization user stories

**Impact:** Cost optimization is now CRITICAL for v1. Without aggressive caching, business model is not viable. Architecture must prioritize local cache storage, image hashing, and intelligent result retrieval.

**Status:** Active

---

## 2025-11-15: Complete Comprehensive Business Analysis

**Type:** Business

**Decision:** Documented complete business analysis including vision, 8 dietary-focused personas (with domain knowledge sections), 5 use cases, 28 functional requirements, 16 non-functional requirements, and 28 user stories organized into 8 epics.

**Key Insights:**
- Personas organized by dietary strictness (not travel context) to properly test classification requirements
- Domain knowledge sections capture what strict vegans know vs. flexible users (gelatin, rennet, etc.)
- Symbol recognition is CRITICAL (>95% accuracy) - symbols override LLM classification
- Lazy loading strategy: photo/hotspots immediate, translation 1-2s, classification background
- Cuisine context awareness essential (Dashi in Japanese, Belgian fries with animal fat)

**Detailed Documentation:**
- [vision.md](../business/vision.md)
- [personas.md](../business/personas.md)
- [use-cases/](../business/use-cases/)
- [requirements/functional.md](../business/requirements/functional.md)
- [requirements/non-functional.md](../business/requirements/non-functional.md)
- [user-stories/stories.md](../business/user-stories/stories.md)

**Impact:** Provides complete foundation for architecture phase. All requirements documented without prioritization (prioritization comes in architecture phase).

**Status:** Active

---

## 2025-11-15: Establish Documentation Structure

**Type:** Process

**Decision:** Created structured documentation with business/ and architecture/ domains, using ADRs for technical decisions.

**Detailed Documentation:** [docs/README.md](../README.md), [architecture/adr/](../architecture/adr/)

**Impact:** Enables systematic capture of requirements, decisions, and architecture. Establishes Single Source of Truth principle.

**Status:** Active

---

_[Future decisions will be added above this line]_
