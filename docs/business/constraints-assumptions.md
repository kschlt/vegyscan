# Constraints and Assumptions

VegyScan App - Project Constraints and Key Assumptions

**Last Updated:** 2025-11-16
**Status:** Active

---

## Project Constraints

Constraints are limitations that CANNOT be changed. These are fixed boundaries for the project.

### Budget Constraints

**Development Budget:**
- **Status:** TBD
- **Constraint:** Single developer or small team (resource-constrained)
- **Impact:** Must prioritize ruthlessly, focus on MVP features only

**Marketing Budget:**
- **Status:** TBD
- **Constraint:** Likely minimal marketing budget for v1
- **Impact:** Must rely on organic growth, viral features (Share Extension), community marketing

**Ongoing Costs:**
- **LLM API costs:** Must stay < €0.005 per page (CRITICAL business model constraint)
- **Target:** < €0.50 total cost for 100-page trip
- **Impact:** Aggressive caching required (70%+ hit rate), cost monitoring from Day 1

### Timeline Constraints

**Target Launch:**
- **Status:** TBD (Q2 2026?)
- **Constraint:** Solo or small team development = longer timeline
- **Impact:** 6-9 months for MVP realistic

**Development Phases:**
- **Phase 1 (MVP):** Core scanning, classification, history - 3-4 months
- **Phase 2 (Polish):** iOS Share Extension, onboarding, error handling - 2-3 months
- **Phase 3 (Launch Prep):** Testing, App Store submission, bug fixes - 1-2 months

### Team Constraints

**Team Size:**
- **Constraint:** 1-2 developers (assumption)
- **Skills Required:**
  - iOS development (Swift, SwiftUI)
  - LLM integration and prompt engineering
  - Computer vision / OCR
  - Backend API development (minimal - mostly LLM API calls)
- **Impact:** Cannot build complex features simultaneously, must sequence work

**Skills Gaps:**
- Legal compliance (GDPR, privacy): May need lawyer consultation
- UI/UX design: May need designer or use Apple HIG templates
- Marketing: Community-driven or hire freelancer

### Technology Constraints

**Platform:**
- **iOS 16+ required** (VisionKit OCR framework)
- **Constraint:** Cannot support iOS 15 or earlier
- **Impact:** ~15% of iPhone users excluded (acceptable tradeoff for VisionKit)

**Device Requirements:**
- iPhone with camera (not iPad-only users)
- Internet connection required for LLM classification (OCR works offline)
- Reasonable storage (photos consume 2-5 MB each)

**Dependencies:**
- **External LLM API:** OpenAI, Anthropic, or similar (critical dependency)
  - Risk: Provider outage, price increase, API changes
  - Mitigation: Design for provider-agnostic integration
- **iOS VisionKit:** OCR accuracy dependent on Apple's framework
  - Risk: API changes, deprecation
  - Mitigation: Follow Apple updates, test on beta iOS

**Architecture Constraints:**
- **v1: Local-only storage** (no cloud backend)
  - Constraint: Simplifies development but limits features
  - Impact: No cross-device sync, no community features in v1
- **v2+: Must be extensible** for cloud features
  - Constraint: Architecture cannot require complete rebuild for v2
  - Impact: Design data models with future cloud sync in mind

### Legal & Regulatory Constraints

**GDPR Compliance (EU):**
- **Constraint:** MUST comply to operate in EU market
- **Requirements:**
  - Privacy policy accessible
  - Data export (Article 20 - Data Portability)
  - Right to erasure (Article 17)
  - User consent for data collection
- **Impact:** Legal requirements = Must Have (REQ-NF-022)

**App Store Requirements:**
- **Constraint:** Must pass Apple App Store Review
- **Requirements:**
  - Privacy labels accurate (REQ-NF-023)
  - No prohibited content
  - Functional app (no placeholders)
  - Complies with App Store Review Guidelines
- **Impact:** App Store rejection delays launch

**Accessibility Laws:**
- **Constraint:** ADA (US), EU accessibility laws require accessible apps
- **Requirements:**
  - VoiceOver support (REQ-NF-019)
  - Color contrast (REQ-NF-021)
  - Dynamic Type (REQ-NF-020)
- **Impact:** Accessibility = Must Have, not optional

### Market Constraints

**Target Market:**
- **Primary:** Vegan/vegetarian travelers (English-speaking for v1)
- **Constraint:** Niche market (smaller TAM than general translation apps)
- **Impact:** Must dominate niche before expanding

**Pricing Constraints:**
- **Constraint:** Users expect low-cost or free travel apps
- **Benchmark:** Google Translate (free), ChatGPT (free tier)
- **Impact:** €8 one-time may be upper limit, must demonstrate 10x value

---

## Key Assumptions

Assumptions are beliefs we're operating on but have NOT validated. These SHOULD be tested.

### User Assumptions

**Assumption 1: Users Have iPhones (iOS 16+)**
- **Assumption:** Target users primarily use iPhones, not Android
- **Validation Needed:** Survey vegan/vegetarian travelers on device usage
- **Risk if Wrong:** Excluding 50%+ of potential market (Android users)
- **Mitigation:** If demand high, consider Android app in v2

**Assumption 2: Users Willing to Pay €8 Upfront**
- **Assumption:** Users will pay one-time €8 for app (no subscription)
- **Validation Needed:**
  - User interviews: "Would you pay €8 for this?"
  - Competitor pricing analysis
  - Beta pricing test (A/B test €5 vs €8 vs €12)
- **Risk if Wrong:** Low conversion, poor revenue
- **Mitigation:** Test freemium model (10 free scans, then pay) if needed

**Assumption 3: Users Have Internet in Restaurants**
- **Assumption:** Most restaurants have WiFi or users have data roaming
- **Validation Needed:** Survey: "Do you typically have internet when dining abroad?"
- **Risk if Wrong:** App doesn't work when most needed
- **Mitigation:**
  - OCR works offline (good first step)
  - v2: On-device LLM for offline classification
  - "Save for Later" when network unavailable

**Assumption 4: Users Trust AI for Dietary Decisions**
- **Assumption:** Users will trust LLM classifications for vegan/vegetarian status
- **Validation Needed:** User testing with real menus, measure trust levels
- **Risk if Wrong:** Users don't use classification feature, stick to Google Translate
- **Mitigation:** Transparency (show reasoning), confidence levels, disclaimers

**Assumption 5: Vegan/Vegetarian Travelers is Large Enough Market**
- **Assumption:** 10,000+ potential users exist (enough for viable business)
- **Validation Needed:**
  - Market research: Size of vegan/vegetarian traveler market
  - Reddit/Facebook group member counts (r/vegan: 1M+ members)
  - Survey: "How often do you travel internationally?"
- **Risk if Wrong:** Market too small, can't reach profitability
- **Mitigation:** Expand to allergen tracking (broader market) in v2

### Product Assumptions

**Assumption 6: LLM Classification Can Achieve >90% Accuracy**
- **Assumption:** Current LLMs (GPT-4, Claude) can accurately classify dishes as vegan/vegetarian
- **Validation Needed:** Test 100+ real menus, measure accuracy
- **Risk if Wrong:** Core value proposition fails
- **Mitigation:** If <85%, pivot to translation-only or hybrid (symbols + manual verification)

**Assumption 7: iOS VisionKit OCR is "Good Enough"**
- **Assumption:** VisionKit can extract text from 80%+ of real-world menus
- **Validation Needed:** Test on diverse menus (handwritten, decorative fonts, poor lighting)
- **Risk if Wrong:** High failure rate frustrates users
- **Mitigation:** Fallback to Google Cloud Vision or manual text entry

**Assumption 8: Users Will Scan 5-10 Pages Per Trip**
- **Assumption:** Average user scans 5-10 menu pages during typical trip
- **Validation Needed:** Beta testing, usage analytics
- **Risk if Wrong:**
  - If MORE (20+ pages): Costs higher than expected
  - If LESS (1-2 pages): Less value, lower willingness to pay
- **Impact on Business Model:** €8 price based on 10-page trip at €0.005/page = €0.05 cost

**Assumption 9: 70% Cache Hit Rate Achievable**
- **Assumption:** Aggressive caching will achieve 70%+ hit rate (reduce LLM costs)
- **Validation Needed:** Beta test cache effectiveness with real users
- **Risk if Wrong:** Costs too high, business model fails
- **Mitigation:** If <50%, must increase price or switch to subscription

### Market Assumptions

**Assumption 10: Competitors Won't Enter Space Immediately**
- **Assumption:** 6-12 months to build user base before Google/competitors respond
- **Validation Needed:** Monitor Google Lens, Apple Live Text for new features
- **Risk if Wrong:** Competitor launches before we do, or shortly after
- **Mitigation:** Focus on execution excellence, niche domination, community building

**Assumption 11: Users Dissatisfied with Current Solutions**
- **Assumption:** Google Translate, ChatGPT inadequate for vegan/vegetarian travel
- **Validation Needed:**
  - User interviews: "What problems do you have with current tools?"
  - Competitor analysis: What do they do poorly?
- **Risk if Wrong:** No demand for new solution
- **Evidence Supporting:** ChatGPT requires manual copy-paste (slow), Google Translate doesn't classify dietary status

**Assumption 12: Organic Growth Sufficient (Low CAC Achievable)**
- **Assumption:** Can acquire users organically for <€3 CAC (via viral features, community)
- **Validation Needed:** Track CAC from Day 1, measure viral coefficient
- **Risk if Wrong:** CAC €10-20, unprofitable at €8 price
- **Mitigation:** iOS Share Extension for viral growth, target niche communities

### Technical Assumptions

**Assumption 13: LLM API Costs Will Remain Stable**
- **Assumption:** OpenAI/Anthropic pricing won't increase significantly in next 12 months
- **Validation Needed:** Monitor provider announcements
- **Risk if Wrong:** Costs double, business model fails
- **Mitigation:** Multi-provider strategy, cost alerts, pricing flexibility

**Assumption 14: Internet Latency <2s for LLM Response**
- **Assumption:** LLM API responds in <1.5s (allows <2s total perceived response time)
- **Validation Needed:** Test API latency from various geographies
- **Risk if Wrong:** App feels slow, users frustrated
- **Mitigation:** Loading states, caching, background processing

**Assumption 15: iOS Share Extension Works Reliably**
- **Assumption:** Share Extension can receive photos from Google Maps, Safari, Photos
- **Validation Needed:** Test on iOS 16, 17 with various apps
- **Risk if Wrong:** Killer feature doesn't work, reputation damage
- **Mitigation:** Thorough testing, fallback to manual upload

---

## Assumptions Requiring Immediate Validation

**BEFORE Development Starts:**
1. ✅ **Test LLM classification accuracy** (100+ real menus) - CRITICAL
2. ✅ **Test iOS VisionKit OCR** (50+ diverse menus) - CRITICAL
3. ✅ **User interviews** (20-30 vegan/vegetarian travelers) - Validate pain points, willingness to pay

**DURING Development:**
4. **Beta test with real users** (20+ users, measure usage patterns)
5. **Measure actual LLM costs** (track per-scan costs, cache hit rates)
6. **Test Share Extension** (across multiple iOS apps, versions)

**BEFORE Launch:**
7. **Pricing test** (A/B test €5 vs €8 vs €12 if possible)
8. **CAC measurement** (test 2-3 acquisition channels, measure cost)

---

## Assumption Tracking

For each assumption, track:
- **Validation method:** How will we test this?
- **Validation date:** When will we know?
- **Result:** Confirmed / Rejected / Partially True
- **Action:** What do we do based on result?

**Example:**

| Assumption | Validation Method | Target Date | Status | Action if Rejected |
|------------|-------------------|-------------|--------|-------------------|
| Users willing to pay €8 | 30 user interviews | Before dev | Pending | Test €5 or freemium model |
| 70% cache hit rate | Beta testing | After v1 alpha | Pending | Increase price or subscription |
| LLM accuracy >90% | Test 100 menus | Week 1 | Pending | Pivot to translation-only |

---

## Notes

**Constraints vs. Assumptions:**
- **Constraints** = Fixed (cannot change them, must work within them)
- **Assumptions** = Testable (should validate before committing resources)

**Red Flags:**
- If >3 critical assumptions are rejected → reconsider viability
- If constraints make product impossible → pivot or cancel

**Update Frequency:**
- Review constraints: Quarterly (rarely change)
- Review assumptions: Weekly during development, monthly post-launch
- Mark assumptions as "Validated" or "Rejected" based on evidence

---

## Constraint & Assumption Ownership

**Product Owner:**
- Responsible for identifying and documenting assumptions
- Prioritizing which assumptions to validate first
- Deciding on pivots if assumptions rejected

**Engineering Team:**
- Responsible for technical constraint validation
- Assessing feasibility within constraints
- Proposing workarounds for constraints when possible

**Both:**
- Jointly review this document monthly
- Update based on new learnings
- Communicate changes to stakeholders
