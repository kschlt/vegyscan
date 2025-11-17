# Phase 1: Critical Validation

**Duration:** 2 weeks
**Status:** ⚪ Not Started
**Priority:** 🔴 CRITICAL - Must complete before any development work

---

## Overview

**Goal:** Validate 3 critical assumptions before investing months in development.

**Why Phase 1 is Critical:**
- **Low investment:** ~40 hours of work
- **High learning:** Validates core business assumptions
- **Risk mitigation:** Fail fast if fundamentals don't work
- **Data-driven decisions:** Replace assumptions with facts

**Decision Gate:** GO / CONDITIONAL GO / NO-GO

---

## Experiments

### 1. LLM Accuracy Test 🔴 CRITICAL
**File:** [llm-accuracy-test.md](./llm-accuracy-test.md)
**Duration:** 1 week
**Status:** ⚪ Not Started

**Question:** Can GPT-4, Claude, or Gemini achieve >90% accuracy on vegan/vegetarian classification?

**Method:**
- Collect 100 diverse menu photos
- Test with 3 LLM providers (OpenAI, Anthropic, Google)
- Calculate accuracy, precision, recall
- Measure cost per page

**Success Criteria:**
- ✅ >90% accuracy on at least 1 provider
- ✅ Cost <€0.005/page
- ⚠️ 85-90% accuracy (conditional)
- ❌ <85% accuracy (FAIL)

**Impact:** Core value proposition validation

---

### 2. Willingness to Pay Survey 🔴 CRITICAL
**File:** [willingness-to-pay-survey.md](./willingness-to-pay-survey.md)
**Duration:** 1-2 weeks
**Status:** ⚪ Not Started

**Question:** What pricing model and price point maximizes revenue and adoption?

**Method:**
- Van Westendorp pricing survey
- Test 5 pricing models (one-time, subscription, freemium, hybrid, pay-per-use)
- Target: 50-100 responses from vegan/vegetarian travelers
- Analyze by market (US, UK, DE, other)

**Success Criteria:**
- ✅ 60%+ willing to pay at validated price
- ✅ Clear pricing model preference
- ✅ Clear market preference
- ⚠️ 50-60% willing to pay (conditional)
- ❌ <50% willing to pay (FAIL)

**Impact:** Business model viability

---

### 3. Competitor Gap Test 🟡 HIGH
**File:** [competitor-gap-test.md](./competitor-gap-test.md)
**Duration:** 3-5 days
**Status:** ⚪ Not Started

**Question:** Do Google Lens, ChatGPT, and Google Translate have significant gaps we can exploit?

**Method:**
- Test 20 menus with each competitor
- Measure accuracy, speed, UX quality
- Document user pain points
- Identify differentiation opportunities

**Success Criteria:**
- ✅ Clear gap in accuracy, speed, or UX
- ✅ Users frustrated with current tools
- ⚠️ Marginal gap (need stronger differentiation)
- ❌ No meaningful gap (FAIL)

**Impact:** Competitive differentiation validation

---

### 4. Market Selection 🟡 HIGH
**Embedded in:** Experiment 2 (Willingness to Pay Survey)
**Duration:** Same as Experiment 2
**Status:** ⚪ Not Started

**Question:** Which market should we launch in first?

**Method:**
- Analyze survey responses by market
- Research iOS penetration by market
- Research competitor intensity by market
- Estimate CAC by market

**Success Criteria:**
- ✅ One market clearly superior (WTP, iOS, CAC)
- ⚠️ Multiple viable markets (choose based on strategic fit)
- ❌ No viable market (FAIL)

**Impact:** Go-to-market strategy

---

## Decision Gate Criteria

**After all experiments complete, assess overall results:**

### 🟢 GO (Proceed to Phase 2)
**Criteria:**
- 3-4 experiments PASS
- LLM accuracy >90% (Exp 1)
- WTP >60% at validated price (Exp 2)
- Clear competitive gap (Exp 3)
- Validated market selection (Exp 4)

**Action:** Proceed to Phase 2 (Feasibility Study)

---

### 🟡 CONDITIONAL GO
**Criteria:**
- 2 experiments PASS
- Some concerns but addressable
- Need adjustments to model

**Action:**
- Adjust scope or strategy
- Re-run selected experiments
- Reassess before Phase 2

---

### 🔴 NO-GO (Stop or Pivot)
**Criteria:**
- 0-1 experiments PASS
- Core assumptions invalid
- Market/product-fit questionable

**Action:**
- STOP development OR
- Major pivot (e.g., different target market, different feature set)

---

## Timeline

**Week 1:**
- Start Experiment 1 (LLM Accuracy Test)
- Design Experiment 2 (WTP Survey)
- Recruit survey respondents

**Week 2:**
- Complete Experiment 1
- Run Experiment 2 (gather responses)
- Run Experiment 3 (Competitor Gap Test)
- Analyze all results

**End of Week 2:**
- Document all findings in [DECISIONS.md](./DECISIONS.md)
- Make GO / CONDITIONAL / NO-GO decision
- If GO: Plan Phase 2 kickoff

---

## Success Metrics

**Phase 1 is successful if:**
1. All 4 experiments completed with documented results
2. Clear GO/NO-GO decision made
3. Pricing model, price point, and market validated
4. LLM provider selected (if GO decision)

**Total Effort:** ~40 hours over 2 weeks

**Total Cost:** ~€50-100 (LLM API testing + survey tools)

---

## Documents

- [llm-accuracy-test.md](./llm-accuracy-test.md) - LLM testing protocol
- [willingness-to-pay-survey.md](./willingness-to-pay-survey.md) - Pricing research
- [competitor-gap-test.md](./competitor-gap-test.md) - Competitive analysis
- [DECISIONS.md](./DECISIONS.md) - Validation results & final decision

---

**Last Updated:** 2024-11-17
**Owner:** [Your Name]
**Next Review:** Daily during Phase 1 execution
