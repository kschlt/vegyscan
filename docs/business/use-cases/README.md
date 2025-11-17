# Use Cases

Detailed descriptions of individual use cases for VegyScan.

## Purpose and Relationship to Requirements

**Use Cases are complementary to Requirements, NOT duplicates:**

- **Requirements (functional.md)** = WHAT the system must do (declarative, feature-level)
  - Example: "REQ-F-032: System shall support uploading photos from device library"

- **Use Cases** = HOW users interact with features (procedural, scenario-level)
  - Example: "UC-006: User opens app → taps Upload Photo → iOS Photo Picker opens → selects photo → system processes → interactive menu displayed"

**Value of Use Cases:**
1. **Interaction flows**: Step-by-step user journeys through features
2. **Error paths**: What happens when things go wrong (network errors, OCR failures, permission denials)
3. **Alternative flows**: Different ways to achieve the same goal
4. **Context**: Real-world scenarios that motivate requirements (Google Maps pre-visit planning)
5. **Exception handling**: References to error-handling.md message library

**Single Source of Truth Principle:**
- Requirements = authoritative WHAT
- Use Cases = authoritative HOW (procedural flows)
- Use cases always reference requirements (e.g., "see REQ-F-035"), never duplicate them

## Template

Use [_template.md](./_template.md) as basis for new use cases.

## Naming Convention

`UC-XXX-short-description.md`

**Example:** `UC-001-scan-single-page-menu.md`

## Use Cases

### Core Workflows

1. **[UC-001: Scan and Analyze Single-Page Menu](./UC-001-scan-single-page-menu.md)**
   - Photo capture with guide lines
   - Image optimization
   - OCR, symbol recognition, meta-info bundling
   - Interactive hotspots
   - Status: Draft

2. **[UC-002: Create Multi-Page Menu Book](./UC-002-create-multi-page-menu-book.md)**
   - Scan multiple menu pages
   - Navigate between pages
   - Unified menu book view
   - Status: Draft

3. **[UC-003: View Dish Details and Vegan/Vegetarian Classification](./UC-003-view-dish-details.md)**
   - Tap hotspot to open detail panel
   - View translation, ingredients, dish type
   - See vegan/vegetarian classification with confidence level and reasoning
   - Country/cuisine context
   - Status: Draft

4. **[UC-004: Mark Favorites and Save Menu to History](./UC-004-mark-favorites-and-save-history.md)**
   - Mark dishes as favorites
   - Auto-save menus to history
   - GPS-based restaurant matching
   - Status: Draft

5. **[UC-005: Retake Photo Due to Poor Quality](./UC-005-retake-poor-quality-photo.md)**
   - Automatic quality detection
   - Actionable feedback (blur, lighting, glare)
   - Scanner guide lines
   - Status: Draft

6. **[UC-006: Upload Menu Photo from Photo Library](./UC-006-upload-menu-photo.md)**
   - Upload single or multiple photos from device library
   - EXIF GPS extraction (never current GPS)
   - Same processing pipeline as camera capture
   - Pre-visit planning use case (Google Maps photos)
   - Permission graceful degradation
   - Status: Draft

7. **[UC-007: Share Menu Photo from Other App (iOS Share Extension)](./UC-007-share-from-other-app.md)**
   - iOS Share Sheet integration (Google Maps, Photos, Safari, Messages, etc.)
   - App Groups communication between extension and main app
   - EXIF GPS only (no current GPS for shared photos)
   - Killer feature for pre-visit restaurant planning
   - Duplicate menu detection
   - Status: Draft

### User Lifecycle & Data Management

8. **[UC-008: First-Time User Onboarding](./UC-008-first-time-onboarding.md)**
   - Optional 3-screen tutorial (skippable)
   - Privacy-first messaging
   - No account creation required
   - Graceful permission handling
   - Status: Draft

9. **[UC-009: View Scan History](./UC-009-view-scan-history.md)**
   - Browse all scanned menus chronologically
   - Search by restaurant or dish name
   - Filter by date, location, favorites
   - GPS-based restaurant matching
   - Empty state handling
   - Status: Draft

10. **[UC-010: Delete Menu from History](./UC-010-delete-menu-from-history.md)**
   - Long-press or swipe to delete individual menu
   - Confirmation dialog (prevent accidents)
   - Clear all history from settings
   - GDPR Right to Erasure compliance
   - Permanent deletion (photos + metadata)
   - Status: Draft

11. **[UC-011: Manage Settings & Preferences](./UC-011-manage-settings-preferences.md)**
   - Privacy settings (Camera, Photos, Location permissions)
   - Data management (Clear cache, Export data, Retention period)
   - User preferences (optional dietary preference)
   - About section (Version, Privacy Policy, Support)
   - Status: Draft

### Cultural Intelligence & Communication (NEW - Based on User Research)

12. **[UC-012: Access Cultural Context and Use Smart Vegan Passport](./UC-012-cultural-context-vegan-passport.md)** ⭐ KILLER FEATURE
   - Automatic cultural context display for detected country/cuisine
   - Hidden ingredients warnings specific to culture (dashi in Japan, ghee in India)
   - Local vegan dish suggestions
   - Smart Vegan Passport with culturally-adapted terminology
   - Auto-translation to detected language
   - Customizable dietary restrictions with visual icons
   - "Show to Waiter" full-screen mode
   - Status: Draft
   - **Priority:** CRITICAL - Top differentiator from competitors

13. **[UC-013: Build and Show Visual Order Basket](./UC-013-visual-order-basket.md)**
   - Add dishes with modifications to order basket
   - Professional restaurant slip-style formatting
   - Display in both local language and English
   - "Show Order to Waiter" full-screen mode
   - Edit/remove items before showing
   - Save order for future visits to same restaurant
   - Load previously saved orders
   - Status: Draft
   - **Priority:** Must Have - Solves communication pain point

14. **[UC-014: Switch Between Photo and Text View with Filtering](./UC-014-dual-view-filtering.md)**
   - Toggle between Photo View (original menu) and Text View (digital list)
   - Filter menu items: [All] [Vegan] [Vegetarian] [Can Modify]
   - Smart sorting: Safest First, Local Dishes, Favorites, Confidence Level
   - "View in Photo" button - highlights dish in original menu for pointing
   - Preserve menu item numbers for easy ordering
   - Search within menu
   - Seamless view switching with state preservation
   - Status: Draft
   - **Priority:** Must Have - Combines analysis + ordering workflow
