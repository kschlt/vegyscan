# Decision Log

> **Last Updated:** 2025-11-15

Chronological record of significant decisions across all domains.

**Format:** Newest first (reverse chronological)

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
