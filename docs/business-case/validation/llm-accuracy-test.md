# Experiment 1: LLM Accuracy Test

**Status:** ⚪ Not Started
**Priority:** 🔴 CRITICAL
**Duration:** 1 week
**Owner:** [Your Name]

---

## Hypothesis

**GPT-4, Claude, or Gemini can achieve >90% accuracy on vegan/vegetarian menu classification**

**If this fails:** Core value proposition invalid → STOP or pivot to translation-only

---

## Objective

Validate that modern LLMs can reliably classify menu items as:
- ✅ Vegan (no animal products)
- 🟡 Vegetarian (dairy/eggs OK, no meat/fish)
- ❌ Contains meat/fish/seafood
- ❓ Uncertain (needs human review)

**Target Accuracy:** >90% (best-in-class)
**Acceptable:** 85-90% (conditional GO)
**Failure:** <85% accuracy

---

## Method

### 1. Data Collection (Days 1-2)

**Collect 100 menu photos covering:**
- **Italian:** 20 menus (pasta, pizza, seafood)
- **Thai:** 20 menus (curry, noodles, fish sauce concerns)
- **Japanese:** 20 menus (sushi, tempura, dashi concerns)
- **Chinese:** 20 menus (stir-fry, soups, oyster sauce concerns)
- **Indian:** 20 menus (curry, paneer, ghee concerns)

**Sources:**
- Own photos from restaurants
- Public menu databases (e.g., Yelp, Google Maps)
- Travel photos from friends
- Stock photo sites (with proper licensing)

**Diversity Requirements:**
- Mix of languages (English, local language, bilingual)
- Mix of photo quality (good lighting, poor lighting, angles)
- Mix of menu formats (printed, handwritten, digital displays)
- Mix of complexity (clear items vs ambiguous descriptions)

---

### 2. Ground Truth Labeling (Days 2-3)

**For each menu item, create ground truth labels:**

**Label each dish:**
- Vegan (V)
- Vegetarian (VEG)
- Contains Meat/Fish (MEAT)
- Uncertain (UNC)

**Labeling Process:**
1. Research each dish online if unfamiliar
2. Consult with vegan friends for ambiguous cases
3. Flag common hidden animal products:
   - Fish sauce (Thai food)
   - Dashi (Japanese food)
   - Oyster sauce (Chinese food)
   - Ghee (Indian food)
   - Parmesan (Italian food - contains rennet)
   - Chicken/beef broth (soups)

**Create spreadsheet:** `llm-accuracy-test-data.csv`

| Menu ID | Item Name | Language | Cuisine | Ground Truth | Notes |
|---------|-----------|----------|---------|--------------|-------|
| IT-001 | Margherita Pizza | English | Italian | VEG | Contains cheese |
| TH-001 | Pad Thai | English | Thai | MEAT | Often contains fish sauce |
| ... | ... | ... | ... | ... | ... |

---

### 3. LLM Testing (Days 3-5)

**Test with 3 providers:**
1. **OpenAI GPT-4** (gpt-4-turbo-2024-04-09 or latest)
2. **Anthropic Claude** (claude-3-5-sonnet-20241022 or latest)
3. **Google Gemini** (gemini-1.5-pro or latest)

**Prompt Template:**
```
You are a vegan/vegetarian menu assistant. Classify this menu item:

MENU ITEM: [Item Name]
DESCRIPTION: [Item Description if available]
CUISINE: [Cuisine Type]

Classify as:
- VEGAN: No animal products (no meat, fish, dairy, eggs, honey)
- VEGETARIAN: No meat/fish, but may contain dairy/eggs
- MEAT: Contains meat, fish, or seafood
- UNCERTAIN: Not enough information or ambiguous

Also provide:
- Reasoning: Why you classified it this way
- Confidence: High / Medium / Low
- Hidden concerns: Any ingredients that might not be obvious

Format response as JSON:
{
  "classification": "VEGAN|VEGETARIAN|MEAT|UNCERTAIN",
  "reasoning": "...",
  "confidence": "HIGH|MEDIUM|LOW",
  "hidden_concerns": ["fish sauce", "chicken broth", etc.]
}
```

**Testing Process:**
1. Set up API accounts for all 3 providers
2. Write simple script to batch process all 100 menus
3. Log all responses with timestamps and costs
4. Calculate metrics (see below)

---

### 4. Metrics Calculation (Day 6)

**Primary Metrics:**

**Accuracy:** (Correct Classifications) / (Total Items)
- Target: >90%
- Acceptable: 85-90%
- Failure: <85%

**Precision by Category:**
- Vegan Precision: (True Vegan) / (All classified as Vegan)
- Vegetarian Precision: (True Vegetarian) / (All classified as Vegetarian)
- Meat Precision: (True Meat) / (All classified as Meat)

**Recall by Category:**
- Vegan Recall: (True Vegan detected) / (All actual Vegan items)
- Vegetarian Recall: (True Vegetarian detected) / (All actual Vegetarian items)
- Meat Recall: (True Meat detected) / (All actual Meat items)

**Cost Metrics:**
- Cost per page (average)
- Cost per classification
- Estimated monthly cost at scale (1000 users, 10 scans/user/month)

**Error Analysis:**
- False Positives (classified as safe, but contains animal products) - **CRITICAL**
- False Negatives (classified as unsafe, but is vegan/vegetarian) - Less critical
- Common failure patterns (e.g., always misses fish sauce)

---

### 5. Results Documentation (Day 7)

**Create results document:** `llm-accuracy-test-results.md`

**Include:**
- Overall accuracy by provider
- Confusion matrix for each provider
- Cost analysis
- Error patterns
- Recommendations

---

## Success Criteria

### ✅ PASS (Proceed to Phase 2)
- At least 1 provider achieves >90% accuracy
- Cost <€0.005 per page
- False positive rate <2% (critical: misclassifying unsafe food as safe)
- Reasoning quality is transparent and helpful

**Action:** Select best provider, proceed to Phase 2

---

### ⚠️ CONDITIONAL (Needs Adjustment)
- 85-90% accuracy achieved
- Cost slightly higher but manageable
- Some error patterns can be addressed with prompt engineering

**Action:**
- Refine prompts and re-test
- Consider ensemble approach (multiple LLMs voting)
- Reassess after improvements

---

### ❌ FAIL (Stop or Pivot)
- <85% accuracy with all providers
- Cost >€0.01 per page
- False positive rate >5%
- No clear path to improvement

**Action:**
- STOP development OR
- Pivot to translation-only (no dietary classification) OR
- Investigate fine-tuning custom models

---

## Tools & Budget

**Required Tools:**
- API accounts: OpenAI, Anthropic, Google AI
- Spreadsheet: Google Sheets or Excel
- Simple scripting: Python + requests library

**Estimated Budget:**
- API costs: ~€50-100 (100 menus × 3 providers × ~€0.01-0.03/request)
- Time: ~40 hours over 1 week

---

## Deliverables

1. ✅ Dataset: 100 labeled menu photos with ground truth
2. ✅ Results: Accuracy metrics for all 3 providers
3. ✅ Cost analysis: Per-page costs and scaling projections
4. ✅ Recommendation: Which provider to use (if any)
5. ✅ Decision: GO / CONDITIONAL / NO-GO

**Document findings in:** [DECISIONS.md](./DECISIONS.md)

---

## Next Steps

**If PASS:**
- Proceed to Experiment 2 (Willingness to Pay Survey)
- Select primary LLM provider
- Plan caching strategy to reduce costs

**If CONDITIONAL:**
- Refine prompts
- Test ensemble approach
- Re-run experiment

**If FAIL:**
- Stop development OR
- Pivot to different value proposition

---

**Last Updated:** 2024-11-17
**Status:** ⚪ Not Started
**Owner:** [Your Name]
