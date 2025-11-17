# Business Case Status Tracker

**Last Updated:** 2024-11-17
**Current Phase:** Phase 0 - Planning Complete

---

## 📊 Overall Progress

**Phase 1 (Validation):** 0% complete (0/4 experiments)
**Phase 2 (Feasibility):** 0% complete (conditional on Phase 1)
**Phase 3 (Business Model):** 0% complete (conditional on Phase 2)

---

## ✅ Phase 1: Critical Validation (NOT STARTED)

### Experiment 1: LLM Accuracy Test
**Status:** ⚪ Not Started
**Priority:** 🔴 CRITICAL
**Owner:** [Your Name]
**Deadline:** TBD (Week 1 of Phase 1)

**Hypothesis:** GPT-4/Claude/Gemini can achieve >90% accuracy on vegan/vegetarian classification

**Progress:**
- [ ] Collect 100 menu photos (0/100)
  - [ ] Italian menus (0/20)
  - [ ] Thai menus (0/20)
  - [ ] Japanese menus (0/20)
  - [ ] Chinese menus (0/20)
  - [ ] Indian menus (0/20)
- [ ] Set up OpenAI API account
- [ ] Set up Anthropic API account
- [ ] Set up Google AI API account
- [ ] Run LLM tests (0/3 providers tested)
- [ ] Analyze results
- [ ] Document decision

**Blockers:** None
**Next Action:** Start collecting menu photos

**Results:** [TBD]
**Decision:** [TBD - GO / CONDITIONAL / NO-GO]

**Document:** [validation/llm-accuracy-test.md](./validation/llm-accuracy-test.md)

---

### Experiment 2: Willingness to Pay Survey
**Status:** ⚪ Not Started
**Priority:** 🔴 CRITICAL
**Owner:** [Your Name]
**Deadline:** TBD (Week 1-2 of Phase 1)

**Hypothesis:** Vegan/vegetarian travelers will pay validated price point

**Progress:**
- [ ] Design survey (Van Westendorp questions)
- [ ] Create survey in Google Forms / Typeform
- [ ] Recruit respondents (target: 50-100)
  - [ ] Post in r/vegan (0 responses)
  - [ ] Post in r/vegetarian (0 responses)
  - [ ] Post in vegan travel Facebook groups (0 responses)
  - [ ] Share on Instagram #vegantraveler (0 responses)
- [ ] Gather responses (0/50 minimum)
- [ ] Analyze results (pricing, market, model preference)
- [ ] Document decision

**Blockers:** None
**Next Action:** Design survey using template

**Results:** [TBD]
**Validated Price Point:** [TBD]
**Validated Market:** [TBD - US/UK vs DE vs other]
**Validated Model:** [TBD - One-time vs Subscription vs Freemium]

**Document:** [validation/willingness-to-pay-survey.md](./validation/willingness-to-pay-survey.md)

---

### Experiment 3: Competitor Gap Test
**Status:** ⚪ Not Started
**Priority:** 🟡 HIGH
**Owner:** [Your Name]
**Deadline:** TBD (Week 2 of Phase 1)

**Hypothesis:** Google Lens/ChatGPT have significant gaps we can exploit

**Progress:**
- [ ] Select 20 test menus (use subset from Exp 1)
- [ ] Test with Google Lens (0/20)
- [ ] Test with ChatGPT (0/20)
- [ ] Test with Google Translate Camera (0/20)
- [ ] Document gaps (accuracy, speed, UX)
- [ ] Analyze differentiation opportunity
- [ ] Document decision

**Blockers:** None
**Next Action:** Run competitive tests

**Results:** [TBD]
**Identified Gaps:** [TBD]
**Decision:** [TBD - Clear gap exists?]

**Document:** [validation/competitor-gap-test.md](./validation/competitor-gap-test.md)

---

### Experiment 4: Market Selection
**Status:** ⚪ Not Started
**Priority:** 🟡 HIGH
**Owner:** [Your Name]
**Deadline:** TBD (End of Week 2)

**Hypothesis:** One market is clearly better for initial launch

**Progress:**
- [ ] Embedded in WTP survey (Exp 2)
- [ ] Analyze responses by market (US vs UK vs DE vs other)
- [ ] Research iOS penetration by market
- [ ] Research competitor intensity by market
- [ ] Calculate estimated CAC by market
- [ ] Make data-driven market selection
- [ ] Document decision

**Blockers:** Depends on Experiment 2 completion
**Next Action:** (Runs alongside Exp 2)

**Results:** [TBD]
**Selected Market:** [TBD - US/UK vs DE vs other]
**Rationale:** [TBD]

**Document:** [validation/willingness-to-pay-survey.md#market-selection](./validation/willingness-to-pay-survey.md#market-selection)

---

## Phase 1 Decision Gate

**Criteria:**
- ✅ 3-4 experiments PASS → 🟢 GO to Phase 2
- ⚠️ 2 experiments PASS → 🟡 CONDITIONAL GO (adjust & re-test)
- ❌ 0-1 experiments PASS → 🔴 NO-GO (stop or major pivot)

**Results:** [TBD after all experiments complete]

**Decision:** [TBD]
**Date:** [TBD]
**Rationale:** [TBD]

**Document:** [validation/DECISIONS.md](./validation/DECISIONS.md)

---

## ⚪ Phase 2: Feasibility Study (CONDITIONAL)

**Status:** Not Started (conditional on Phase 1 GO decision)

### Technical Feasibility
**Status:** ⚪ Not Started
**Progress:** 0% complete
**Next Action:** Run iOS VisionKit OCR tests on 100 menus
**Document:** [feasibility-study.md#technical-feasibility](./feasibility-study.md#technical-feasibility)

### Economic Feasibility
**Status:** ⚪ Not Started
**Progress:** 0% complete
**Next Action:** Model costs (development + LLM + infrastructure)
**Document:** [feasibility-study.md#economic-feasibility](./feasibility-study.md#economic-feasibility)

### Schedule Feasibility
**Status:** ⚪ Not Started
**Progress:** 0% complete
**Next Action:** Estimate MVP timeline (solo dev + AI)
**Document:** [feasibility-study.md#schedule-feasibility](./feasibility-study.md#schedule-feasibility)

---

## ⚪ Phase 3: Business Model Definition (CONDITIONAL)

**Status:** Not Started (conditional on Phase 2 GO decision)

### Business Model Canvas
**Status:** ⚪ Not Started
**Progress:** 0% complete (awaiting Phase 1 validation data)
**Next Action:** Fill canvas with validated pricing/market/model
**Document:** [business-model.md#business-model-canvas](./business-model.md#business-model-canvas)

### Unit Economics
**Status:** ⚪ Not Started
**Progress:** 0% complete
**Next Action:** Calculate LTV, CAC, LTV:CAC ratio
**Document:** [business-model.md#unit-economics](./business-model.md#unit-economics)

### Financial Projections
**Status:** ⚪ Not Started
**Progress:** 0% complete
**Next Action:** Build 3-scenario model (spreadsheet)
**Document:** [financial-projections.md](./financial-projections.md)

---

## 📋 Open Questions (Hypotheses to Validate)

See [hypotheses.md](./hypotheses.md) for complete list.

**Critical (Phase 1):**
1. ❓ LLM accuracy >90%? (Experiment 1)
2. ❓ Users will pay $X? (Experiment 2)
3. ❓ Which market? US/UK vs DE? (Experiment 4)
4. ❓ Which model? One-time vs Subscription vs Freemium? (Experiment 2)
5. ❓ Competitive gap exists? (Experiment 3)

**High Priority (Phase 2):**
6. ❓ iOS VisionKit reliable (>80%)? (Technical Feasibility)
7. ❓ LLM costs <€0.005/page achievable? (Economic Feasibility)
8. ❓ Cache hit rate >70% achievable? (Economic Feasibility)
9. ❓ Solo dev can build in 6-12 months? (Schedule Feasibility)

**Medium Priority (Phase 3):**
10. ❓ What's the break-even user count? (Financial Model)
11. ❓ What's realistic CAC by channel? (GTM Planning)

---

## 🚧 Blockers

**Current Blockers:** None (Phase 0 complete, ready to start Phase 1)

**Anticipated Blockers:**
- Finding 50+ survey respondents (may take 2+ weeks)
- Access to diverse menu photos (may need to visit restaurants or use online sources)
- LLM API costs for testing (budget ~€50-100 needed)

---

## 📅 Timeline

**Phase 1 Target:** 2 weeks from start
**Phase 2 Target:** 1-2 weeks after Phase 1 GO
**Phase 3 Target:** 1 week after Phase 2 GO
**MVP Development:** 6-12 months after Phase 3 GO

**Critical Path:** Phase 1 → Phase 2 → Phase 3 → MVP Development

---

## 🎯 Success Metrics

**Phase 1 Success:**
- LLM accuracy >90% (at least 1 provider)
- 60%+ willing to pay at validated price
- Clear competitive gap identified
- Market selection validated

**Phase 2 Success:**
- Technical feasibility confirmed
- Economic feasibility confirmed (break-even achievable)
- Timeline realistic (6-12 months)

**Phase 3 Success:**
- Business model defined and validated
- LTV:CAC ratio >3:1
- Financial model shows path to sustainability

---

**Last Updated:** 2024-11-17
**Next Review:** Daily during Phase 1 execution
**Owner:** [Your Name]
