## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/88#top

**Issue title:** POST /reviews endpoint has no test for when the profile has no ingested documents

**Tier:** [X] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
The issue is that there is currently no test case for when a profile exists but has no associated ingested documents. In this situation, the review endpoint should handle the missing content gracefully rather than crashing. The test should verify that the endpoint returns an appropriate error response when no ingested documents are available. This mainly affects the review route logic in `api/routes/reviews.py` and its related tests.

Is this right for me?
- I can explain the issue: the review endpoint needs a test for when a profile exists but has no ingested content.
- I found the relevant route in `api/routes/reviews.py`.
- The issue references `tests/unit/test_review_routes.py`, which does not currently exist, so I may need to create it.
- I found `tests/unit/test_review_service.py` and will use it to understand the project’s testing style.
- “Done” means the endpoint returns an appropriate error instead of crashing.
- This is a Tier 1 issue with a small, localized scope, which is a good fit for my first contribution.
- The estimated 2–3 hours is realistic for me.
- I will check the issue comments/ledger for other claims and confirm there are no blockers.

**Branch name:** (test/88-review-no-test-when-no-ingest)

**Setup confirmation:** [X] App runs locally at localhost:5173

**Cohort ledger:** [X] Issue added to cohort ledger

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** [link to commit documenting the reproduced issue]

**Reproduction summary:**
[1–2 sentences: How did you reproduce the issue? What did you observe?]
I reproduced the issue by checking whether the referenced test file existed using `test -f tests/unit/test_review_routes.py && echo "FILE EXISTS" || echo "FILE MISSING"`. The command returned `FILE MISSING`, confirming that the route-level test file for this scenario is not present in the current repository.

**PLAN.md link:** [link to PLAN.md in your fork]

**Walkthrough video (recommended):** Not available

**Blockers or open questions:**
[Anything you're still uncertain about going into Week 9, or leave blank]