# Procedure: how this tool grades a PR package

## Read order

1. Identify whether this is live mode or eval mode. If the mode or package is unclear, ask for the missing information instead of guessing.
2. In live mode, read `scope.md` first. Stop if its `Repo:` line is a placeholder or the PR is outside the named repository. Then read `voice-guide.md`.
3. In eval mode, read only the supplied bundle. Do not fetch anything or read other files.
4. Read the issue and plan, including deviation notes, before examining the diff. For a house-chain package, use the house plan and repro pack.
5. Read the repository's PR template and contribution policy, then gather the test evidence and required-check results.
6. Read the branch diff against the plan, then the draft PR title and description against both the diff and the test evidence. This order helps reveal unplanned changes and claims the artifacts do not support.

## Evidence gathering

For each rubric check, record the specific facts that determine its grade.

- **Plan fidelity:** Pair each changed file and substantive diff hunk with the plan's stated scope. Record any unplanned change, missing planned work, or deviation note. Compare the PR text with what the diff actually contains.
- **Test evidence:** Record the relevant test or check, its result, and what behavior it verifies. Compare this with the plan's test expectations and the repository's required checks. Record any required check that was not run or did not pass.
- **Diff quality:** Identify changes unrelated to the issue or plan, and artifacts or leftover code that make the intended change harder to review. Record the affected file or hunk and why it obstructs review.
- **Standards and communication:** Compare the PR title and description with the PR template and contribution policy. Record required asks that are missing, and any claim about the change or tests that conflicts with the diff or evidence.

In live mode, use the working copy's `git diff main...HEAD`, the repository's issue thread, PR template, contribution policy, and supplied test evidence. In eval mode, use the corresponding facts in the bundle only. Do not infer a test result or policy that is absent from the available evidence.

## Check execution

Run each check in the order it appears in `rubric.md`. Apply that check's pass condition to the evidence gathered for it; do not substitute a general impression of the PR. If evidence is missing or does not establish the pass condition, grade the check `unclear`. Give each check one concise evidence line naming the deciding fact or quote. Do not change a grade to offset another check.

## Verdict assembly

Apply the verdict rule in `rubric.md` exactly. A failed or unclear required check means `reject`; otherwise, return `accept`. Preferred checks do not change the verdict.

When the verdict is `reject`, identify the first failed or unclear required check in rubric order as the deciding check in the readable summary. If all required checks pass, state that in the summary. Include evidence for every check in the required JSON output, and end with the valid fenced JSON block specified in `SKILL.md`, with nothing after it.
