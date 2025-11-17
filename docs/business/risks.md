# Risk Register

VegyScan App - Risk Analysis and Mitigation Strategies

**Last Updated:** 2025-11-16
**Status:** Active

---

## Risk Assessment Framework

**Probability Scale:**
- **Low:** <20% chance of occurring
- **Medium:** 20-60% chance
- **High:** >60% chance

**Impact Scale:**
- **Low:** Minor inconvenience, easily recoverable
- **Medium:** Significant setback, affects timeline or quality
- **High:** Major impact on business viability or user safety
- **Critical:** Business-ending or user safety-critical

**Priority:** Probability × Impact

---

## CRITICAL RISKS (Address Immediately)

### Risk 1: LLM Classification Accuracy Too Low

**Probability:** Medium (40%)
**Impact:** Critical (core value proposition fails)
**Priority:** HIGH

**Description:**
- LLM fails to achieve >90% accuracy in vegan/vegetarian classification
- Users get incorrect classifications leading to accidental consumption of animal products
- Reputation damage, user churn, potential liability

**Indicators:**
- Accuracy falls below 85% in testing
- User complaints about misclassifications
- High rate of "uncertain" classifications (>30%)

**Mitigation Strategies:**

**Before Development:**
1. **Test classification accuracy EARLY** with 100+ real menu samples
2. Set minimum 90% accuracy threshold as go/no-go decision
3. Test across multiple cuisines (Italian, Thai, Chinese, Japanese, Indian)
4. Test menu symbol recognition separately (must be 100% accurate)

**During Development:**
1. **Menu symbols = highest authority** (REQ-F-004): If menu shows vegan symbol, override LLM if conflict
2. **Show confidence levels** (REQ-F-007): Be transparent when uncertain
3. **Provide reasoning** (REQ-F-010): Users can judge classification quality themselves
4. **Conservative classification:** Default to "uncertain" or "check with staff" rather than false positive/negative

**Post-Launch:**
1. User feedback mechanism (v2) to identify misclassifications
2. Continuous LLM prompt refinement based on real-world errors
3. Consider multiple LLM providers for cross-validation on uncertain cases

**Fallback Plan:**
- If accuracy <85%, pivot to "translation-only" app (removes vegan/vegetarian classification)
- Less valuable, but still useful for travelers

---

### Risk 2: LLM API Costs Exceed Viability Threshold

**Probability:** Medium (50%)
**Impact:** Critical (business model fails)
**Priority:** HIGH

**Description:**
- LLM API costs >€0.005/page (target) making app unprofitable
- Caching doesn't achieve 70%+ hit rate
- API provider increases prices
- Business cannot sustain at €8 one-time purchase price

**Indicators:**
- Actual cost testing shows €0.01-0.02/page
- Cache hit rate <50%
- Provider announces price increase
- Users scan more pages than expected (average >5 pages/session)

**Mitigation Strategies:**

**Cost Monitoring:**
1. **Measure costs from Day 1** with detailed analytics
2. Set cost alerts (if per-page cost exceeds €0.008, trigger alert)
3. Track cache hit rates (must be >60% to stay viable)

**Technical Mitigations:**
1. **Aggressive caching** (REQ-F-029, REQ-F-030, REQ-F-031):
   - Menu-level duplicate detection (same restaurant, same menu)
   - Dish-level caching (perceptual hashing)
   - Smart result retrieval (fuzzy matching)
2. **On-device OCR** (REQ-NF-014): No API cost for text extraction
3. **Optimize LLM prompts:** Minimize token usage while maintaining accuracy
4. **Batch processing:** Send multiple dishes in one API call if possible

**Business Mitigations:**
1. **Alternative pricing models:**
   - If costs too high, switch to subscription (€2.99/month) instead of one-time
   - Freemium: 10 free scans, then €0.99/month
   - Higher one-time price (€12-15) if users find high value
2. **Multiple LLM providers:** Test OpenAI, Anthropic, Google - use cheapest that meets accuracy
3. **Rate limiting:** If costs spike, limit scans per user (10 scans/day free, unlimited with subscription)

**Contingency:**
- If costs unsustainable, pivot to local LLM model (on-device inference, no API costs)
- Trade accuracy for cost reduction

---

### Risk 3: Users Don't Trust AI Classifications (Low Adoption)

**Probability:** Medium (40%)
**Impact:** High (users don't use core feature)
**Priority:** MEDIUM-HIGH

**Description:**
- Users skeptical of AI making dietary decisions
- Fear of false positives ("AI said it's vegan but it's not")
- Users stick to Google Translate or asking staff
- Low engagement with classification feature

**Indicators:**
- Users scan menus but don't open dish details (low tap-through rate)
- High rate of users asking "How do I know this is accurate?"
- App Store reviews: "I don't trust the AI"
- Low retention after first use

**Mitigation Strategies:**

**Transparency & Education:**
1. **Show reasoning** (REQ-F-010): Explain WHY dish is classified as vegan
   - "Contains: tomato sauce, basil. No animal products detected."
2. **Show confidence levels** (REQ-F-007): Be honest about uncertainty
   - "⚫⚫⚫ High Confidence" vs "⚫◯◯ Low Confidence - check with staff"
3. **Menu symbols = authority** (REQ-F-004): Show that we trust official symbols first
4. **Onboarding messaging** (UC-008): Educate users on how classification works

**Social Proof:**
1. App Store description: "Powered by advanced AI, trained on thousands of menus"
2. Testimonials from beta testers (if available)
3. Accuracy stats in-app: "95% accuracy on 10,000+ dishes tested"

**Conservative Approach:**
1. **When uncertain, say so:** Better to show "uncertain - check with staff" than guess wrong
2. **Country/cuisine context** (REQ-F-012): "In Thailand, fish sauce is common in 'vegetable' dishes"
3. **Highlight risks:** "Some dishes may contain hidden animal products - always confirm if allergic"

**User Control:**
1. Allow users to override classification (v2 feature)
2. "Report Incorrect" button (v2 - REQ-F-028)

---

## HIGH RISKS (Monitor Closely)

### Risk 4: User Acquisition Costs Too High (Can't Scale)

**Probability:** High (60%)
**Impact:** High (can't grow profitably)
**Priority:** MEDIUM-HIGH

**Description:**
- Cost to acquire user (CAC) exceeds customer lifetime value (LTV)
- €8 one-time purchase = low LTV
- Paid ads too expensive (CAC €10-20)
- Cannot scale user base profitably

**Indicators:**
- Organic downloads < 100/month
- Paid ad CAC > €10
- LTV < CAC (unprofitable)

**Mitigation Strategies:**

**Organic Growth Focus:**
1. **iOS Share Extension** (REQ-F-034) enables viral growth:
   - User shares menu from Google Maps → friend sees VegyScan → downloads app
2. **Target vegan/vegetarian communities:**
   - Reddit: r/vegan, r/vegetarian
   - Facebook groups for vegan travelers
   - Instagram hashtags: #vegantraveler, #vegetariantravel
3. **Content marketing:**
   - Blog: "Top 10 Vegan-Friendly Cities in Europe"
   - YouTube: "How to Find Vegan Food When Traveling"
4. **App Store Optimization (ASO):**
   - Keywords: "vegan menu translator," "vegetarian travel app"
   - Screenshots showcasing key features

**Low-Cost Channels:**
1. PR outreach to vegan lifestyle blogs/magazines
2. Partnerships with vegan travel influencers
3. Cross-promotion with vegan restaurant apps (HappyCow, etc.)

**Measure & Iterate:**
1. Track CAC from Day 1 (source: organic, paid, referral)
2. Set CAC target: <€3 (allows profitability at €8 price)
3. Kill channels that don't meet CAC target

---

### Risk 5: Competitors Copy Features (Google Lens Adds Vegan Classification)

**Probability:** High (70%)
**Impact:** High (lose competitive advantage)
**Priority:** MEDIUM-HIGH

**Description:**
- Google adds vegan/vegetarian classification to Google Lens
- Apple adds to Live Text feature
- Competitors have more resources, better distribution

**Indicators:**
- Competitor launches similar feature
- Downloads plateau or decline
- User reviews comparing to Google Lens

**Mitigation Strategies:**

**Defensibility Through Execution:**
1. **Execution excellence:** Make VegyScan 10x better, not just first-to-market
   - Faster (< 2s response time)
   - More accurate (>90% classification)
   - Better UX (iOS-native, not web-based)
2. **Niche focus:** Vegan/vegetarian travelers (not general translation)
3. **Community building:** Build loyal user base before competitors enter

**Moat Features:**
1. **iOS Share Extension** (REQ-F-034): Deep iOS integration competitors can't easily copy
2. **Offline-first architecture:** Works without constant internet (competitive advantage over web tools)
3. **Privacy-first:** No cloud storage, no accounts (trust signal)

**Continuous Innovation:**
1. v2 features: Community shared scans, user feedback, personalization
2. Always be 6-12 months ahead of competitors in roadmap

**Accept Reality:**
- If Google/Apple enter space, pivot to B2B (licensing to restaurants/travel apps)
- Or focus on premium features they won't offer (allergen tracking, etc.)

---

### Risk 6: OCR Accuracy Too Low for Real-World Menus

**Probability:** Medium (30%)
**Impact:** High (app doesn't work)
**Priority:** MEDIUM

**Description:**
- iOS VisionKit OCR fails on:
  - Handwritten menus
  - Low-quality photos (blur, glare)
  - Stylized fonts (decorative scripts)
  - Dark photos (bad lighting)
- Users frustrated by "No text detected" errors

**Indicators:**
- >20% of scans fail OCR
- User reviews: "Doesn't work on my menu"
- High rate of retakes (UC-005)

**Mitigation Strategies:**

**Quality Guidance:**
1. **Scanner guide lines** (REQ-F-001): Help users align photo properly
2. **Auto quality detection** (REQ-F-025): Warn before taking bad photo
3. **Actionable feedback** (UC-005): "Menu is blurry - hold phone steady and try again"

**Fallback Handling:**
1. **Graceful failure** (error-handling.md): Clear message when OCR fails
   - "No menu text detected. Try better lighting or a clearer photo."
2. **Manual entry option** (future): Let user type dish name if OCR fails

**Technical Improvements:**
1. **Image preprocessing:** Enhance contrast, remove glare before OCR
2. **Multiple OCR attempts:** Try different image processing techniques
3. **Alternative OCR engines:** Test Google Cloud Vision, AWS Textract if VisionKit insufficient

**Set Expectations:**
1. Onboarding: "Works best with clear, printed menus"
2. Help section: "Tips for best results" (good lighting, steady hand, etc.)

---

## MEDIUM RISKS (Manage Proactively)

### Risk 7: Privacy Concerns / GDPR Non-Compliance

**Probability:** Low (15%)
**Impact:** Critical (legal liability, fines)
**Priority:** MEDIUM

**Description:**
- GDPR violation leads to fines (up to 4% of revenue or €20M)
- User complaints about data collection
- App Store rejection for inaccurate privacy labels

**Mitigation Strategies:**

**Compliance First:**
1. **GDPR requirements implemented** (REQ-NF-022):
   - Privacy policy accessible from app
   - Data export (REQ-F-038)
   - Right to erasure (REQ-F-039)
   - Data retention policy (REQ-F-041)
2. **App Store privacy labels accurate** (REQ-NF-023)
3. **Privacy-first architecture:**
   - Local-only storage (no cloud in v1)
   - No user accounts (no PII collected)
   - Minimal data collection

**Legal Review:**
1. Have privacy policy reviewed by lawyer before launch
2. Ensure terms of service compliant with EU law
3. Disclaimer: "AI classifications are not perfect - always verify if allergic"

**Transparency:**
1. Explain data practices in onboarding (UC-008): "All data stays on your device"
2. Make privacy policy easy to read (avoid legalese)

---

### Risk 8: Device Storage Constraints (Users Run Out of Space)

**Probability:** Medium (40%)
**Impact:** Medium (poor UX, user churn)
**Priority:** MEDIUM

**Description:**
- Menu photos consume storage (2-5 MB/menu)
- Users with 64 GB iPhone run out of space
- App blamed for storage issues

**Indicators:**
- User reviews: "App uses too much storage"
- High rate of "Clear All History" usage
- Storage-related errors

**Mitigation Strategies:**

**Storage Management:**
1. **Auto-delete old scans** (REQ-F-041): Default 90-day retention
2. **Clear cache option** (UC-011 Alt-1): Free space without deleting menus
3. **Photo compression:** Reduce photo file size without quality loss
4. **Storage display** (UC-011): Show "Storage Used: 47.2 MB (23 menus)"

**User Control:**
1. Configurable retention period (30/60/90/180 days)
2. Manual deletion (UC-010)
3. Export then delete old scans

**Optimization:**
1. Use HEIC format (50% smaller than JPEG) where supported
2. Downsample large photos (4K → 2K resolution sufficient for OCR)

---

### Risk 9: Users Can't Find App (Poor App Store Discovery)

**Probability:** Medium (50%)
**Impact:** Medium (slow growth)
**Priority:** MEDIUM

**Description:**
- App doesn't rank for key search terms
- Lost in crowded translation/travel app category
- Low organic downloads

**Mitigation Strategies:**

**App Store Optimization (ASO):**
1. **Keywords in title:** "VegyScan - Vegan Menu Translator"
2. **Subtitle:** "Find vegan & vegetarian dishes abroad"
3. **Keywords:** vegan, vegetarian, menu, translator, travel, diet, food, restaurant
4. **Screenshots:** Show before/after (menu → classified dishes)
5. **Demo video:** 30-second showcase of scanning menu

**Category Selection:**
- Primary: Food & Drink
- Secondary: Travel

**Reviews & Ratings:**
1. Prompt happy users for reviews (after 5+ successful scans)
2. Respond to all reviews (build trust)
3. Target 4.5+ star average

---

## LOW RISKS (Acceptable)

### Risk 10: Platform Dependency (iOS API Changes)

**Probability:** Low (10%)
**Impact:** Medium
**Priority:** LOW

**Description:**
- Apple deprecates VisionKit or changes APIs
- iOS update breaks app functionality

**Mitigation:**
- Follow Apple deprecation notices
- Test on beta iOS versions before public release
- Have 6-12 month buffer before APIs removed

---

### Risk 11: LLM Provider Outage / Service Interruption

**Probability:** Low (10%)
**Impact:** Medium (temporary app unavailability)
**Priority:** LOW

**Description:**
- LLM API provider has outage
- Users can't get classifications during outage

**Mitigation:**
1. **Graceful degradation:** Show cached results if available
2. **Retry logic** (error-handling.md): Auto-retry after outage resolves
3. **User communication:** "Service temporarily unavailable. Try again in a few minutes."
4. **Multiple providers:** If one provider down, failover to backup (OpenAI → Anthropic)

---

## Risk Monitoring Plan

**Weekly:**
- Monitor crash reports and error rates
- Check user reviews for new issues
- Track cost metrics (API costs per scan)

**Monthly:**
- Review risk register, update probabilities
- Assess mitigation effectiveness
- Identify new risks

**Quarterly:**
- Comprehensive risk assessment
- Adjust priorities based on product evolution
- Update mitigation strategies

---

## Escalation Criteria

**Immediate Action Required:**
- Classification accuracy <85% in testing
- LLM costs >€0.01/page
- GDPR violation discovered
- Critical bug affecting >10% of users

**Review Within 1 Week:**
- User acquisition costs >€5
- Competitor launches similar feature
- >10% of scans failing OCR

---

## Notes

This risk register should be reviewed and updated:
- Before each major release
- After significant product changes
- Quarterly at minimum
- Whenever new risks identified

**Risk ownership:** Product owner responsible for monitoring, engineering team responsible for technical mitigations.
