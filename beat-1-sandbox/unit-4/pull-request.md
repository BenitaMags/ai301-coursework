# Unit 4 — Test and Submit

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/262

**Branch**

fix/53-parenthesized-us-phone

## Eval iterations

**Run history**

- The first full attempt produced errors for all packages because Claude Code authentication had expired; it had no scored agreement result.
- First scored full run: 19/20. `pkg-18` was graded accept, but its gold label was reject.
- Focused `pkg-18` canary after refining the rubric: 1/1 correct.
- Final full run: 20/20, PASS. Categories: clear-accept 7/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, unreviewable 3/3.

**Package analysis**

`pkg-18` was labeled reject in the gold data. My first full run graded it accept because the rubric did not sufficiently hold a change with leftover debug output and unrelated formatting churn. After tightening the Diff quality check, the focused rerun graded it reject, matching the gold label; the final full run also matched.

**Check rationale**

I added this Diff quality pass condition to the rubric: “The changes are relevant to the issue and bounded by the plan; unrelated changes or leftover artifacts do not obstruct review.” I chose it after `pkg-18` showed that tests can pass while debug leftovers and formatting churn still make a small change harder to review.

**Trade-offs**

A stricter Diff quality check can reject a tested change when unrelated churn or leftover artifacts obstruct review. That stricter rule corrected the `pkg-18` mismatch: the canary matched 1/1, and the final full run matched 20/20.
