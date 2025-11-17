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
- **Primary:** Vegan/vegetarian travelers (iOS users)
- **Market Selection:** TO BE VALIDATED in Phase 1 (US/UK vs Germany vs multi-market)
- **Language:** TO BE VALIDATED (depends on market selection)
  - If US/UK selected: English-first
  - If Germany selected: German-first
  - Decision driven by WTP data, iOS penetration, CAC potential
- **Constraint:** Niche market (smaller TAM than general translation apps)
- **Impact:** Must dominate niche before expanding
- **See:** [business-case/hypotheses.md](../business-case/hypotheses.md) - Question #4

**Pricing Constraints:**
- **Constraint:** Users expect low-cost or free travel apps
- **Benchmark:** Google Translate (free), ChatGPT (free tier)
- **Challenge:** Must demonstrate 10x value to justify paid app
- **Pricing Model:** TO BE VALIDATED (one-time vs subscription vs freemium)
- **Price Point:** TO BE VALIDATED (Van Westendorp survey in Phase 1)
- **See:** [business-case/validation/willingness-to-pay-survey.md](../business-case/validation/willingness-to-pay-survey.md)

---

## Key Assumptions

Assumptions are beliefs we're operating on but have NOT validated. These SHOULD be tested.

### User Assumptions

**Assumption 1: Users Have iPhones (iOS 16+)**
- **Assumption:** Target users primarily use iPhones, not Android
- **Validation Needed:** Survey vegan/vegetarian travelers on device usage
- **Risk if Wrong:** Excluding 50%+ of potential market (Android users)
- **Mitigation:** If demand high, consider Android app in v2

**Assumption 2: Pricing Model and Price Point**
- **STATUS:** ❌ REMOVED - Now TO BE VALIDATED in Phase 1
- **Previous Assumption:** Users will pay one-time €8 for app (no subscription)
- **Removed:** 2024-11-17
- **Reason:** Developer intuition, not user research. Multiple pricing models possible (one-time, subscription, freemium, hybrid, pay-per-use)
- **Now Validating:**
  - Pricing model preference (Van Westendorp survey)
  - Optimal price point (data-driven, not assumed)
  - Market-specific pricing (US vs UK vs DE may differ)
- **See:** [business-case/validation/willingness-to-pay-survey.md](../business-case/validation/willingness-to-pay-survey.md)
- **See:** [business-case/hypotheses.md](../business-case/hypotheses.md) - Questions #2 and #3

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
- **Impact on Business Model:** At 10-page trip and €0.005/page = €0.05 LLM cost per user (pricing model TBD in Phase 1)

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
- **Risk if Wrong:** CAC €10-20, unprofitable at validated price point
- **Mitigation:** iOS Share Extension for viral growth, target niche communities
- **Note:** Acceptable CAC depends on validated pricing model from Phase 1

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

**Phase 1: Critical Validation (BEFORE Development Starts) - 2 weeks**
See: [business-case/validation/](../business-case/validation/)

1. ⚪ **Test LLM classification accuracy** (100+ real menus) - CRITICAL
   - See: [business-case/validation/llm-accuracy-test.md](../business-case/validation/llm-accuracy-test.md)
   - Target: >90% accuracy

2. ⚪ **Willingness to Pay Survey** (50-100 respondents) - CRITICAL
   - See: [business-case/validation/willingness-to-pay-survey.md](../business-case/validation/willingness-to-pay-survey.md)
   - Validates: Pricing model, price point, target market

3. ⚪ **Competitor Gap Test** - Validate differentiation
   - See: [business-case/validation/competitor-gap-test.md](../business-case/validation/competitor-gap-test.md)
   - Tests: Google Lens, ChatGPT, Google Translate gaps

**Phase 2: Feasibility Study (AFTER Phase 1 GO decision) - 1-2 weeks**
4. ⚪ **Test iOS VisionKit OCR** (50+ diverse menus)
   - See: [business-case/feasibility-study.md#technical-feasibility](../business-case/feasibility-study.md#technical-feasibility)
   - Target: >80% success rate

**DURING Development:**
5. **Beta test with real users** (20+ users, measure usage patterns)
6. **Measure actual LLM costs** (track per-scan costs, cache hit rates)
7. **Test Share Extension** (across multiple iOS apps, versions)

**BEFORE Launch:**
8. **CAC measurement** (test 2-3 acquisition channels, measure cost)

---

## Assumption Tracking

For each assumption, track:
- **Validation method:** How will we test this?
- **Validation date:** When will we know?
- **Result:** Confirmed / Rejected / Partially True
- **Action:** What do we do based on result?

**Phase 1 Validation Tracking:**

| Assumption | Validation Method | Phase | Status | Action if Rejected |
|------------|-------------------|-------|--------|-------------------|
| Pricing model preference | WTP survey (Phase 1) | 1 | ⚪ Not Started | Test alternative models |
| Price point viable | Van Westendorp survey | 1 | ⚪ Not Started | Adjust pricing or model |
| Target market selection | Market analysis + WTP | 1 | ⚪ Not Started | Choose alternative market |
| LLM accuracy >90% | Test 100 menus | 1 | ⚪ Not Started | Pivot to translation-only |
| Competitive gap exists | Competitor testing | 1 | ⚪ Not Started | Find new differentiation |
| VisionKit >80% OCR | Test 50 menus | 2 | ⚪ Not Started | Use alternative OCR |
| 70% cache hit rate | Beta testing | During dev | ⚪ Not Started | Adjust pricing/model |

**See:** [business-case/validation/DECISIONS.md](../business-case/validation/DECISIONS.md) for results

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

---

## Removed Assumptions (Now TO BE VALIDATED)

**The following assumptions have been REMOVED and moved to Phase 1 validation:**

### 1. Pricing Model: One-Time Purchase
**Previous Assumption:** €8 one-time purchase
**Removed:** 2024-11-17
**Reason:** Solo dev bias toward one-time purchase (personal preference), but subscription may have better LTV. Must validate with users, not assume.
**Now:** TO BE VALIDATED in Phase 1 (Willingness to Pay Survey)
**Options:** One-time purchase, monthly subscription, annual subscription, freemium, hybrid, pay-per-use
**See:** [business-case/validation/willingness-to-pay-survey.md](../business-case/validation/willingness-to-pay-survey.md)

---

### 2. Price Point: €8
**Previous Assumption:** €8 is the right price
**Removed:** 2024-11-17
**Reason:** Developer intuition, not user research. Must validate optimal price point with Van Westendorp methodology.
**Now:** TO BE VALIDATED in Phase 1 (Van Westendorp Price Sensitivity Meter)
**Method:** Survey asking "too cheap", "good value", "expensive", "too expensive" thresholds
**See:** [business-case/validation/willingness-to-pay-survey.md](../business-case/validation/willingness-to-pay-survey.md)

---

### 3. Target Market: Germany First
**Previous Assumption:** Launch in Germany (familiar market for developer)
**Removed:** 2024-11-17
**Reason:** Familiarity bias. Business logic suggests US/UK may be better (higher WTP, more iOS users). Personal comfort shouldn't override data.
**Now:** TO BE VALIDATED in Phase 1 (Market Selection Analysis)
**Options:**
- US market (English, high WTP, 50%+ iOS penetration)
- UK market (English, high WTP, 50%+ iOS, strong vegan culture)
- Germany (familiar, but lower WTP, 30% iOS)
- Multi-market (English + German from Day 1)
**Decision Criteria:**
- Highest willingness to pay
- Best iOS penetration in target demographic
- Lowest competitive intensity
- Easiest organic acquisition (lowest CAC potential)
**See:** [business-case/hypotheses.md](../business-case/hypotheses.md) - Question #4

---

### 4. UI Language: English First
**Previous Assumption:** v1 launches in English
**Removed:** 2024-11-17
**Reason:** Depends on market selection (Question #3 above). If DE market wins, German-first makes more sense.
**Now:** CONDITIONAL on market selection from Phase 1
- If US/UK selected → English-first
- If Germany selected → German-first
- If multi-market → English + German from Day 1
**See:** [business/vision.md - Differentiation Strategy](./vision.md#differentiation-strategy)

---

## Principle: Data-Driven Decision Making

**How we make decisions:**
1. **Data-driven, not assumption-driven** - Validate every hypothesis
2. **User research over developer intuition** - What users want, not what we think
3. **Business logic over personal comfort** - Best market, not familiar market
4. **Optimize for LTV, not just price** - Long-term value, not one-time extraction
5. **UX as differentiator** - Win on experience, not technology

**When to challenge assumptions:**
- Developer says "I prefer X" → Ask "What do users prefer?"
- Feeling says "X is easier" → Ask "What does data say?"
- Intuition says "X will work" → Ask "How do we validate?"

**See:** [business-case/hypotheses.md](../business-case/hypotheses.md) for all open questions

---

**Last Updated:** 2024-11-17
