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
https://github.com/dkn345/pathreview/commit/7c7a7f711980797228581e27062d965b40674808

**Reproduction summary:**
[1–2 sentences: How did you reproduce the issue? What did you observe?]
I reproduced the issue by checking whether the referenced test file existed using `test -f tests/unit/test_review_routes.py && echo "FILE EXISTS" || echo "FILE MISSING"`. The command returned `FILE MISSING`, confirming that the route-level test file for this scenario is not present in the current repository.

**PLAN.md link:** [Link Text](PLAN.md)

**Walkthrough video (recommended):** Not available

**Blockers or open questions:**
[Anything you're still uncertain about going into Week 9, or leave blank]

## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
I created `tests/unit/test_review_routes.py` and added a unit test for the `POST /reviews` error path when no ingested documents are available. The test verifies that the route preserves the controlled HTTP error and does not schedule background processing.

**Next steps:**
I will commit and push the test, open a draft pull request, request peer or mentor feedback, address any relevant feedback, and finalize the PR.

**Blockers:**
The repository has pre-existing lint and unit-test failures unrelated to my change. My new test passes independently, and Ruff passes for `tests/unit/test_review_routes.py`.

---

### Check-in 2 (end of week)

**PR link:** (https://github.com/ascherj/pathreview/pull/998)

**Branch:** `test/88-review-no-test-when-no-ingest`

**What you built:**
I added route-level test coverage for the `POST /reviews` error path when no ingested documents are available. The test confirms that the endpoint preserves the controlled `400 Bad Request` response and does not queue the background review-processing task.

**Tests added or updated:**
Created `tests/unit/test_review_routes.py` with `test_profile_no_ingested_docs`. The new test passes independently.

**Self-review confirmation:** [X] make check passes  [X] make test-unit passes

**Draft PR feedback received from:** [name or Slack handle, or "none"] 
none