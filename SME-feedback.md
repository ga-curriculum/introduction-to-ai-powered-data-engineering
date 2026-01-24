# SME Feedback: Introduction to AI-Powered Data Engineering

**Reviewer:** Sumit Rahman  
**Date:** 2025-01-23  
**Status:** Requires Revisions

---

## Overall Assessment

The lesson provides a solid conceptual foundation for understanding data engineering's role in AI systems. The framing of "AI as a data systems problem" is excellent and industry-aligned. However, there are gaps in technical depth, missing content that should support the practice materials, and some structural issues that need addressing.

**Verdict:** Acceptable with revisions noted below.

---

## Must-Fix Issues

### 1. Missing Learning Objective Coverage

**Issue:** The competency map specifies the learning objective as:
> "Explain how data engineering supports the AI lifecycle and enables automation in modern ML systems."

The current content adequately covers the AI lifecycle but provides **insufficient depth on automation**. The "Automation and Data Flow Patterns" section (10 minutes) is too brief and lacks concrete examples of what automation looks like in practice.

**Required Action:**
- Expand the automation section to include at least one concrete example of manual vs. automated workflow
- Add a brief discussion of what "enabling automation" means (e.g., idempotency, scheduling, error handling, observability)
- Consider adding a simple diagram showing a manual workflow vs. an automated pipeline

---

### 2. Table of Contents Mismatch

**Issue:** The Table of Contents lists:
```
6. ResourcesTitle of Section
```

This appears to be a copy-paste error.

**Required Action:** Fix to read "6. Resources"

---

### 3. Timing Inconsistency Between README and Instructor Guide

**Issue:** The README shows timing as:

| Segment | Duration |
|---------|----------|
| Lab | 50 min |

But the pacing guide allocates **60 minutes** for the lab (1:00-2:00 in Classes 1-2 combined for Week 1).

**Required Action:** Reconcile timing. Recommend adjusting to:
- Segments 1-3: 30 minutes total (condensed)
- Lab: 60 minutes
- Wrap-up: 10 minutes

---

### 4. Missing Python/Cloud Setup Context

**Issue:** The competency map indicates learners will "build a simple Python script to move sample data from a local file into cloud storage." However, the theory content contains **zero Python references** and no mention of cloud storage mechanics.

**Required Action:** Add a brief section (5-7 minutes) covering:
- High-level overview of how Python fits into data engineering workflows
- Conceptual introduction to cloud object storage (S3/GCS/Azure Blob) — what it is, not how to use it
- Mention that the lab will involve writing Python code

This bridges the conceptual content to the hands-on activity.

---

## Recommended Improvements (Non-Blocking)

### 5. Add Real-World Examples

**Suggestion:** The content is currently abstract. Adding 1-2 concrete industry examples would improve engagement:
- Example: "Netflix's recommendation system processes billions of events daily. When their data pipelines fail, recommendations become stale, directly impacting user engagement."
- Example: "Uber's surge pricing depends on real-time data pipelines. A 5-minute delay in data can mean incorrect pricing across thousands of rides."

---

### 6. Strengthen the "Models as Consumers" Concept

**Suggestion:** The statement "AI models are consumers of data pipelines" is powerful but underdeveloped. Consider adding:
- What models consume (features, training data, inference data)
- How consumption patterns differ between training and inference
- Why this consumer relationship matters for data engineers

---

### 7. Instructor Guide: Add Discussion Prompts

**Suggestion:** The instructor guide mentions asking:
> "Where do you think most AI systems fail in production?"

Consider adding 2-3 more discussion prompts with expected responses to help instructors facilitate engagement:
- "What happens to a fraud detection model if transaction data arrives 2 hours late?"
- "Why might a model that works perfectly in testing fail in production?"

---

## Discrepancies Between README and Instructor Guide

| Item | README | Instructor Guide | Resolution Needed |
|------|--------|------------------|-------------------|
| Wrap-up title | "Wrap-Up Reflection" | "Wrap-Up and Reflection" | Minor — standardize |
| Lab timing | 50 min | Not specified | Align with pacing guide (60 min) |

---

## Alignment with Practice Materials

The following topics are needed in the theory to support the practice problems and lab:

| Topic | Currently Covered? | Notes |
|-------|-------------------|-------|
| AI data lifecycle stages | ✅ Yes | Well covered |
| Batch vs. streaming patterns | ✅ Yes | Conceptual level appropriate |
| Automation benefits | ⚠️ Partial | Needs concrete examples |
| Python for data engineering | ❌ No | Add brief mention |
| Cloud object storage concept | ❌ No | Add brief mention |
| Data quality/validation | ⚠️ Partial | Mentioned in monitoring, could expand |
| Pipeline failure scenarios | ❌ No | Add 1-2 examples |

---

## Summary of Required Changes

1. **Fix** the Table of Contents typo ("ResourcesTitle of Section")
2. **Expand** automation section with concrete manual vs. automated example
3. **Add** brief Python and cloud storage context section (5-7 min)
4. **Reconcile** timing with pacing guide

---

## Sign-Off

- [ ] Content developer has addressed all Must-Fix issues
- [ ] SME has reviewed revisions
- [ ] Materials are ready for practice problem and lab development

**Next Review Date:** _TBD after revisions_