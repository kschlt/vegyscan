# Non-Functional Requirements

> **Last Updated:** 2025-11-15

_This file is the Single Source of Truth for all non-functional requirements (quality attributes, constraints, cross-cutting concerns)._

---

## Performance

### REQ-NF-001: Instant UX - Perceived Response Time

**Description:** System must feel "instant" with perceived response time < 2 seconds for core interactions.

**Rationale:** Users expect mobile app responsiveness. Slow responses lead to abandonment. "Instant" feel is competitive differentiator vs. ChatGPT.

**Priority:** Must Have

**Status:** Draft

**Metric:** Perceived response time (time to first meaningful content)

**Target:** < 2 seconds from photo capture to interactive menu view with hotspots

**Related:**
- Vision: [Success Criteria - Instant feel](../vision.md#success-criteria)
- Vision: [Goals #3 - Faster than alternatives](../vision.md#goals)
- Use Case: [UC-001](../use-cases/UC-001-scan-single-page-menu.md)

---

### REQ-NF-002: Lazy Loading Strategy

**Description:** System must implement progressive loading to prioritize speed of first meaningful interaction.

**Rationale:** Full LLM classification may take 2-5 seconds. Users should see optimized menu and hotspots immediately while details load.

**Priority:** Must Have

**Status:** Draft

**Related:**
- REQ-NF-001: Instant UX
- Use Case: [UC-003](../use-cases/UC-003-view-dish-details.md)

---

### REQ-NF-003: Page Transition Performance

**Description:** Multi-page menu navigation must be smooth with page transitions < 0.3 seconds.

**Rationale:** Laggy page transitions break immersion. Users expect native iOS fluidity.

**Priority:** Must Have

**Status:** Draft

**Metric:** Page transition time

**Target:** < 0.3 seconds

**Related:**
- Use Case: [UC-002](../use-cases/UC-002-create-multi-page-menu-book.md)

---

## Usability / UX

### REQ-NF-004: Progressive Disclosure

**Description:** System must avoid information overload by revealing details progressively as user explores.

**Rationale:** Too much information at once is overwhelming. Users should see overview first, then drill down.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Vision: [Success Criteria - No information overload](../vision.md#success-criteria)

---

### REQ-NF-005: Visual Context Preservation

**Description:** System must preserve original menu photo as central navigation element throughout experience.

**Rationale:** Users need visual reference to point at dish when ordering. Replacing menu with text loses context.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Vision: [Goals #2 - Preserve visual context](../vision.md#goals)

---

### REQ-NF-006: Intuitive First-Time Use

**Description:** System must be usable without tutorial or onboarding for first-time users.

**Rationale:** Travel context = no time for learning. App must be immediately understandable.

**Priority:** Must Have

**Status:** Draft

---

## Accessibility

### REQ-NF-019: VoiceOver Support

**Description:** System must be fully navigable using iOS VoiceOver screen reader for blind and low-vision users.

**Rationale:** Blind and low-vision travelers also eat at restaurants and deserve equal access to menu information. Accessibility is both a legal requirement and ethical obligation.

**Priority:** Must Have

**Status:** Draft

**Acceptance Criteria:**
- [ ] All UI elements have descriptive accessibility labels
- [ ] All images have accessibility descriptions (menu photos describe cuisine type/layout)
- [ ] Dish classifications announced clearly by VoiceOver ("Pasta Carbonara, Contains Meat, High Confidence")
- [ ] All interactive elements (buttons, hotspots) have clear labels and hints
- [ ] Dish detail panel fully navigable with VoiceOver
- [ ] Multi-page menus: Page number announced when swiping
- [ ] Error messages announced by VoiceOver

**Related:**
- Vision: [Target Users - Inclusive design](../vision.md#target-users)

---

### REQ-NF-020: Dynamic Type Support

**Description:** System must respect user's iOS Dynamic Type text size preferences and scale all text appropriately.

**Rationale:** 30% of iPhone users increase default text size. Low-vision users, elderly users, and those with reading difficulties rely on larger text.

**Priority:** Must Have

**Status:** Draft

**Acceptance Criteria:**
- [ ] All text scales with iOS Dynamic Type settings
- [ ] Layout adapts gracefully to larger text sizes (no truncation)
- [ ] All text remains readable at largest accessibility size
- [ ] Interactive elements maintain minimum tap target size (44x44pt) at all sizes
- [ ] No horizontal scrolling required at larger text sizes

**Related:**
- REQ-NF-006: Intuitive First-Time Use (readability is part of usability)

---

### REQ-NF-021: Color Contrast & Color-Blind Accessibility

**Description:** System must meet WCAG 2.1 Level AA color contrast requirements and not rely solely on color to convey information.

**Rationale:** 8% of men and 0.5% of women have color vision deficiency. Legal requirement in many markets (ADA, EU accessibility laws). Benefits all users in bright sunlight or low-light conditions.

**Priority:** Must Have

**Status:** Draft

**Acceptance Criteria:**
- [ ] All text meets WCAG 2.1 Level AA contrast ratio (4.5:1 for normal text, 3:1 for large text)
- [ ] Vegan/vegetarian classifications use icons + text, not color alone
- [ ] Interactive elements clearly distinguishable from non-interactive (not just color)
- [ ] Error states use icons/text in addition to color
- [ ] All information conveyed by color is also conveyed another way (shape, icon, text)

**Examples:**
- ✅ Good: Green checkmark icon + "Vegan" text
- ❌ Bad: Green text only (color-blind users can't distinguish)

**Related:**
- REQ-NF-017: Icon-Based UI (icons help accessibility)
- Vision: [Success Criteria - No information overload](../vision.md#success-criteria)

---

## Platform & Compatibility

### REQ-NF-007: iOS-Only (v1)

**Description:** System must be iOS-only native app for initial release.

**Rationale:** Focus resources, leverage iOS-specific features, target primary persona demographic.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Vision: [What We're NOT Building](../vision.md#what-were-not-building-strategic-boundaries)

---

### REQ-NF-008: Native iOS Features Integration

**Description:** System must leverage native iOS frameworks and capabilities for best performance and UX.

**Rationale:** Native features provide better performance, UX consistency, and access to latest iOS capabilities.

**Priority:** Must Have

**Status:** Draft

---

## Reliability

### REQ-NF-009: Network Error Graceful Degradation

**Description:** System must handle network failures gracefully without crashing or losing user data.

**Rationale:** Travel context = unreliable networks. App must work with poor connectivity.

**Priority:** Must Have

**Status:** Draft

---

### REQ-NF-010: Data Persistence - Local Storage

**Description:** System must store all scanned menus and history locally on device (not cloud, for v1).

**Rationale:** Privacy, speed, offline access. Users retain data even without network.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Vision: [Strategic Decisions - Cost Optimization](../vision.md#strategic-decisions-and-constraints)

---

## Security & Privacy

### REQ-NF-011: GPS Privacy

**Description:** System must request GPS permission explicitly and function fully without it.

**Rationale:** Users may decline location access for privacy. App must not require it.

**Priority:** Must Have

**Status:** Draft

---

### REQ-NF-012: Photo Privacy

**Description:** System must handle menu photos with user privacy in mind (no cloud storage without consent).

**Rationale:** Menu photos may contain personal info. Privacy is trust signal.

**Priority:** Must Have

**Status:** Draft

---

## Legal & Compliance

### REQ-NF-022: GDPR Compliance

**Description:** System must comply with EU General Data Protection Regulation (GDPR) requirements for data collection, storage, and user rights.

**Rationale:** Legal requirement for operating in EU market. Non-compliance can result in fines up to 4% of revenue or €20 million. Builds user trust through transparent data practices.

**Priority:** Must Have (Legal Requirement)

**Status:** Draft

**Acceptance Criteria:**
- [ ] Privacy policy accessible from app (before first use and in settings)
- [ ] User can export all stored data in machine-readable format (JSON/CSV) - Data portability (Article 20)
- [ ] User can delete all stored data from device - Right to be forgotten (Article 17)
- [ ] User consent obtained before accessing location, photos, camera
- [ ] Data retention policy enforced: Menus auto-deleted after 90 days (configurable in settings)
- [ ] No data shared with third parties without explicit consent
- [ ] User can withdraw consent for location/photo access and delete associated data

**Data Collected (for GDPR transparency):**
- Menu photos (stored locally on device only)
- GPS coordinates (if user grants permission, stored with menu)
- Scan history (dates, restaurant names if GPS available)
- Favorited dishes
- User preferences (dietary preference, language)

**Data NOT Collected:**
- No user account information (no sign-in in v1)
- No data sent to cloud (except OCR text sent to LLM API for classification)
- LLM API does not retain user data (verify with provider)

**Related:**
- REQ-NF-010: Data Persistence - Local Storage
- REQ-NF-011: GPS Privacy
- Vision: [Strategic Decisions - Privacy-first](../vision.md#strategic-decisions-and-constraints)

---

### REQ-NF-023: App Store Privacy Labels & Requirements

**Description:** System must accurately declare data collection practices in Apple App Store privacy labels.

**Rationale:** Required by Apple App Store Review Guidelines. Inaccurate labels result in app rejection. Builds user trust through transparency.

**Priority:** Must Have (Legal Requirement)

**Status:** Draft

**Acceptance Criteria:**
- [ ] Privacy labels accurately reflect data collection:
  - **Data Used to Track You:** None
  - **Data Linked to You:** None (no user accounts in v1)
  - **Data Not Linked to You:** Photos (not sent to cloud), Precise Location (optional, stored locally)
- [ ] Privacy policy URL provided in App Store listing
- [ ] App description clearly states: "All data stored locally on your device. No cloud storage. No user accounts."

**App Store Privacy Label Declaration:**
```
Data Not Linked to You:
- Photos (menu photos stored locally on device)
- Precise Location (optional, stored with menus for restaurant matching)

Data Used for Analytics:
- None (or if analytics added: Usage data, anonymized, opt-in)
```

**Related:**
- REQ-NF-022: GDPR Compliance
- Vision: [Strategic Decisions - No user accounts for v1](../vision.md#strategic-decisions-and-constraints)

---

### REQ-NF-024: Privacy-First Analytics (Optional)

**Description:** If analytics are implemented, they must respect user privacy and comply with GDPR.

**Rationale:** Product metrics needed to improve app, but must not compromise user privacy or legal compliance.

**Priority:** Should Have

**Status:** Draft (Future - Not in v1 MVP)

**Acceptance Criteria (if implemented):**
- [ ] No third-party analytics services (no Google Analytics, Mixpanel, etc.)
- [ ] Custom analytics implementation or privacy-first service (e.g., TelemetryDeck)
- [ ] User can opt out in settings (default: opt-in required)
- [ ] All metrics anonymous (no user identification)
- [ ] Metrics tracked: Scans per session, error rates, cache hit rates, feature usage counts
- [ ] No personally identifiable information (PII) collected
- [ ] Analytics data retention: 12 months maximum

**Recommended Metrics (Privacy-Safe):**
- Count: Total scans, cache hits, OCR errors, network errors
- Averages: Scans per session, time to first scan
- Feature usage: Upload vs. Camera, Share Extension usage, favorites count
- NO: Location data, menu content, user behavior tracking, cross-session tracking

**Related:**
- REQ-NF-022: GDPR Compliance
- Vision: [Success Criteria - Need metrics to validate](../vision.md#success-criteria)

---

### REQ-NF-025: Trust-Building UX Patterns

**Description:** System must use UX patterns that build user trust through transparency, humility, and emphasis on verification assistance rather than false certainty.

**Rationale:** **RESEARCH-VALIDATED (Nov 2025):** Users do NOT trust absolute claims that a dish is vegan. They trust tools that help them verify intelligently. App must position as **verification assistant**, not guarantee machine. Trust comes from honesty about uncertainty and empowering users to verify themselves.

**Priority:** Must Have (CRITICAL for user trust and retention)

**Status:** Draft

**Related:**
- User Research: [Trust Mechanisms](../user-research-report.md#trust-mechanisms--verification-behaviors)
- User Research: [Trust-Building UX Recommendations](../user-research-report.md#trust-building-ux-recommendations)
- REQ-F-010: Classification Reasoning (language guidelines)
- Vision: [Positioning - Verification Assistant](../vision.md#positioning-based-on-deep-research-nov-2025)

**Design Principles:**

**1. Present Uncertainty as Normal and Expected**
- ✅ "Likely vegan, but please verify these points:"
- ✅ "This dish appears to be vegan based on description"
- ❌ "This IS vegan" (overly confident without qualification)
- **Rationale:** Users appreciate when staff admit they're not sure and go check - app should do same
- Evidence: *"I appreciate when they admit they aren't sure and go check – I trust that more than a quick yes"*

**2. Emphasize Assistive Role (Not Oracle)**
- Frame VegyScan as *"VegyScan Assistant"* persona throughout app
- Language patterns:
  - ✅ "VegyScan suggests asking:"
  - ✅ "Let's verify this together - ask about the broth"
  - ✅ "We recommend confirming:"
  - ❌ "VegyScan guarantees this is vegan"
  - ❌ "This is definitely safe"
- Collaborative, supportive tone (not authoritative declarations)

**3. Provide Explanations for Every Flag**
- Every warning/alert must have tappable "Why?" tooltip or explanation
- Examples:
  - "May contain oyster sauce. Why? Oyster sauce is commonly used in Chinese vegetable stir-fries"
  - "Fish sauce often added to this dish in Thai cuisine - verify with staff"
- **Benefit:** Educates user, shows app's reasoning, builds credibility through transparency

**4. Visual Cues for Community Data (When Available)**
- Green checkmark with count for community confirmations: *"✓ Confirmed vegan by 3 users (last: Jan 2025)"*
- Grey for no confirmations: *"No community confirmations yet – be the first!"*
- **Transparency:** User sees what's validated by community vs what's AI-only analysis
- Never hide the source of confidence (AI vs community vs both)

**5. Encourage At-the-Table Verification**
- After providing questions/analysis, include supportive verification message:
  - *"If the staff seems unsure, don't hesitate to ask them to double-check with the chef. Your peace of mind matters!"*
- Aligns app with community's cautious attitude (research shows users verify even with high confidence)
- **Benefit:** Shows app cares about outcomes, not just giving advice and disappearing

**6. Tone: Reassuring but Not Overconfident**
- Balance: Reduce anxiety WITHOUT creating false sense of security
- ✅ "It should be fine if you confirm no fish sauce"
- ✅ "Most restaurants will understand if you say this..."
- ✅ "This traditionally contains X - worth asking to be sure"
- ❌ "This will definitely be fine"
- ❌ "100% guaranteed vegan"
- Acknowledge social anxiety: *"It's okay to ask - restaurants handle dietary questions all the time"*

**Acceptance Criteria:**

- [ ] All classification results use qualifying language ("appears to", "likely", "traditionally")
- [ ] NEVER use absolute language ("IS vegan", "guaranteed") without heavy qualification
- [ ] Every flag/warning has tappable "Why?" explanation with cultural context
- [ ] UI copy frames app as "assistant" not "authority" (terminology audit)
- [ ] Community confirmation data (when available) displayed with transparency about source
- [ ] At least one verification encouragement message per dish detail view
- [ ] Tone is supportive and reassuring, acknowledging that asking questions is normal
- [ ] Error states/uncertainties explained rather than hidden
- [ ] No "100% Vegan" badges or similar absolute guarantees (forbidden by research)
- [ ] Visual distinction between AI classification vs community confirmation vs both

**UX Testing Validation:**

Test with users:
- [ ] "Does this app make you feel confident asking questions?" (target: 80%+ yes)
- [ ] "Do you trust the app's suggestions?" (target: 75%+ yes)
- [ ] "Would you still ask staff even with app's guidance?" (target: 60%+ yes = good! Means they're verifying)
- [ ] "Does the app feel honest about uncertainty?" (target: 85%+ yes)

**Examples of Good vs Bad UX:**

**Good Example (Verification Assistance):**
```
🟢 Appears vegan
ℹ️ No obvious animal products detected in description.

💬 We recommend confirming with staff:
   • "Is the broth vegetable-based?"
   • "Any butter or dairy in the sauce?"

[Show in Thai] [Copy questions]

ℹ️ Why these questions? Broths often contain fish stock
in Thai cuisine, and butter is a common hidden ingredient.

✓ 2 users confirmed this was vegan (last: 2 days ago)
```

**Bad Example (False Certainty):**
```
✅ VEGAN - 100% SAFE
This dish is guaranteed vegan.
No need to ask staff.

[Order Now]
```

**Related:**
- REQ-F-010: Classification Reasoning (implements this via language)
- REQ-F-053: Community Dish Confirmation (implements social proof aspect)
- REQ-NF-006: Intuitive First-Time Use (trust is part of usability)

---

## Cost Efficiency

### REQ-NF-013: LLM Cost Optimization

**Description:** System must minimize LLM API costs through aggressive caching, deduplication, smart result retrieval, and on-device processing to make business model viable.

**Rationale:** LLM costs directly impact business model viability. At €8 app price with 30% App Store fee, a user scanning 100 pages on holiday would cost €5 at €0.05/scan, making the business unprofitable. Cost must be dramatically lower.

**Priority:** CRITICAL - Must Have

**Status:** Draft

**Target:** < €0.01 per 2-page menu scan (€0.005 per page) in LLM costs

**Business Model Analysis:**
- App price: €8.00
- App Store fee (30%): -€2.40
- Available margin: €5.60
- Holiday scenario: 100 pages scanned
- Required cost per page: < €0.005 to remain profitable
- Target total cost for 100-page trip: ~€0.50 (9% of revenue)

**Cost Optimization Strategies (See Functional Requirements):**
- Menu duplicate detection (same restaurant, same menu) → REQ-F-029
- Dish-level caching (same dish across sessions) → REQ-F-030
- Smart result retrieval (image similarity matching) → REQ-F-031
- UX design to minimize re-scans
- On-device processing where possible → REQ-NF-014

**Related:**
- Vision: [Success Criteria - Cost-efficient LLM usage](../vision.md#success-criteria)
- REQ-F-029: Menu Duplicate Detection
- REQ-F-030: Dish-Level Caching
- REQ-F-031: Smart Result Retrieval

---

### REQ-NF-014: On-Device Processing Priority

**Description:** System must maximize on-device processing to reduce cloud API dependency and costs.

**Rationale:** On-device is faster, cheaper, more private. iOS has powerful ML capabilities.

**Priority:** Should Have

**Status:** Draft

---

## Maintainability

### REQ-NF-015: Code Maintainability

**Description:** System must be built with clean architecture and maintainable code for future enhancements.

**Rationale:** App will evolve. v1 architecture must support future features.

**Priority:** Should Have

**Status:** Draft

---

### REQ-NF-016: Future Feature Extensibility

**Description:** System architecture must accommodate planned future features without major refactoring.

**Rationale:** v2+ features (community, cloud sync) deferred from v1 but must be addable without rebuild.

**Priority:** Should Have

**Status:** Draft

**v1 Architectural Guidance:**
- **Community features deferred** (REQ-F-027, REQ-F-028) - OUT of v1 scope
- v1 uses local-only storage, no cloud backend
- **Critical:** Design v1 architecture to be extensible, not rebuildable
- Future cloud features should add new layer, not replace existing architecture
- Data models should accommodate future sync (e.g., local IDs + future cloud IDs)
- Authentication/account system should be addable without UI redesign

**Examples of Extensibility:**
- Local SQLite → Future: Add cloud sync layer on top
- Local-only menus → Future: Add optional cloud sharing
- No accounts → Future: Add optional sign-in for cloud features
- Core functionality works without cloud (offline-first preserved)

**Related:**
- Vision: [Strategic Decisions - Community features OUT of v1](../vision.md#strategic-decisions-and-constraints)
- REQ-F-027: Community-Shared Menu Scans (Future v2+)
- REQ-F-028: User Feedback on Classification (Future v2+)

---

### REQ-NF-017: Icon-Based UI (Minimal Text)

**Description:** System UI must rely primarily on icons, colors, and visual indicators rather than text labels.

**Rationale:** Minimize language barriers, reduce text to translate, create universal design that works across cultures.

**Priority:** Should Have

**Status:** Draft

**v1 Guidance:**
- Vegan/vegetarian classifications use icons (not just text labels)
- Navigation uses iconography where possible
- Color coding for dietary categories (green = vegan, etc.)
- Text only where absolutely necessary for clarity
- Enables easier translation to other languages later (less text = less translation work)

**Related:**
- Vision: [Strategic Decisions - Language/Internationalization](../vision.md#strategic-decisions-and-constraints)

---

### REQ-NF-018: Internationalization (i18n) Support

**Description:** System must use i18n framework for all user-facing text, enabling future translation without code changes.

**Rationale:** v1 launches in English, but architecture must support adding languages (German, French, etc.) without rebuild.

**Priority:** Should Have

**Status:** Draft

**v1 Implementation:**
- English language only for v1 launch
- All UI strings in i18n files (not hardcoded)
- String keys used in code (e.g., `i18n.t('vegan_label')` not `"Vegan"`)
- Date/number formatting locale-aware
- Future: Add German, French translations by updating i18n files only

**Related:**
- Vision: [Strategic Decisions - Language/Internationalization](../vision.md#strategic-decisions-and-constraints)

---

## Notes

**Performance Priorities:**
- Instant feel (REQ-NF-001) is critical differentiator
- Lazy loading (REQ-NF-002) enables instant UX

**Platform:**
- iOS-only (REQ-NF-007) focuses resources
- Native iOS (REQ-NF-008) maximizes performance

**Cost Management:**
- LLM optimization (REQ-NF-013) impacts unit economics
- On-device processing (REQ-NF-014) reduces costs

**Privacy:**
- Local storage (REQ-NF-010) is privacy-friendly
- GPS optional (REQ-NF-011) respects user privacy
