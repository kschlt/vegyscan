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

## Platform & Compatibility

### REQ-NF-007: iOS-Only (v1)

**Description:** System must be iOS-only native app for initial release.

**Rationale:** Focus resources, leverage iOS-specific features, target primary persona demographic.

**Priority:** Must Have

**Status:** Draft

**Related:**
- Vision: [Out of Scope - Android](../vision.md#out-of-scope-for-now)

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
- Vision: [Out of Scope - Offline mode TBD](../vision.md#out-of-scope-for-now)

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

## Cost Efficiency

### REQ-NF-013: LLM Cost Optimization

**Description:** System must minimize LLM API costs through efficient prompting, caching, and on-device processing.

**Rationale:** LLM costs directly impact business model viability.

**Priority:** Must Have

**Status:** Draft

**Target:** < €0.05 per menu scan in LLM costs

**Related:**
- Vision: [Success Criteria - Cost-efficient LLM usage](../vision.md#success-criteria)

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

**Rationale:** Bonus features may be added post-v1.

**Priority:** Should Have

**Status:** Draft

**Related:**
- Vision: [Bonus Features](../vision.md#bonus-features-future-enhancement)

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
