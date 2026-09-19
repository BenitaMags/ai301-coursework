# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | Last 5 default-branch commits, commit authors, and the maintainer first-response sample described in `references/evidence-guide.md` | Pass if there is at least one human-authored default-branch commit within the past 90 days OR the maintainer first-response sample shows at least one Owner, Member, or Collaborator responding within 30 days | required |
| Repository activity | Latest release, last push, archived status, and adoption signals described in `references/evidence-guide.md` | Pass if the repository is not archived and has either a default-branch commit within the past 180 days or a release within the past 180 days | required |
| Newcomer scope | Issue body, issue labels, and comment thread | Pass if the issue asks for one coherent, bounded deliverable a newcomer could finish in a single pull request. Fail only if it is an umbrella/tracking issue whose body is a checklist of separate sub-issues, a pure usage or support question, or a proposal whose approach is still an open design question the maintainers have not settled. Several files or sub-steps inside one coherent deliverable still pass, and a maintainer-applied `good first issue` or `help wanted` label is positive evidence of bounded scope | required |
| Available to contribute | Assignees, linked PRs and their states, claim comments and their dates, and label history from the issue sidebar and comment thread | Pass if there is no active assignee, no open linked PR, and no maintainer-confirmed existing implementation. Linked PRs that are closed without merging do not fail this check, and a claim comment older than 90 days with no follow-up from that commenter is stale and does not fail it either. Student claim comments do not cause failure because of the Path Review house rule in `scope.md` | required |
| Attempt history | Linked PRs and their states, and the claim/abandonment pattern in the comment thread | Pass if the issue has fewer than two linked PRs that were closed without merging, and the thread does not show a maintainer clarification question left unanswered while contributors repeatedly claimed and abandoned the work. Two or more abandoned attempts mean the work is harder or less settled than the issue text suggests, which is not a first contribution | required |
| Contribution policy | `CONTRIBUTING.md`, `.github/`, dedicated AI policy files, contributor documentation, and PR templates | Pass if the repository does not explicitly ban AI-assisted or AI-generated contributions. Disclosure, testing, understanding, or human-review requirements count as conditions to follow rather than failures | required |
| Issue clarity | Issue body and comment thread | Pass if the issue communicates a concrete problem or requested change and provides enough information to understand the intended contribution, even if reproduction steps are absent | preferred |

## Verdict rule

Accept if every required check passes. Preferred checks never change the verdict and are used only to rank issues that are accepted. If a required check is unclear, treat it as a fail. Student claim 
comments in the Path Review repository do not cause the Available to contribute check to fail because of the Path Review house rule.
