---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: is this ready to submit? A PR package contains the plan it claims to implement, the issue that plan belongs to, the branch diff, a draft PR title and description, and test evidence. Read those artifacts against one another and the applicable repository rules. Do not grade a different question or more than one package per run.

## Inputs and modes

Run in exactly one of these modes:

- **Live mode:** Read the student's `plan.md`, including deviation notes; the diff from the working copy produced by `git diff main...HEAD`; the draft PR title and description; test evidence; and the issue thread the plan belongs to. For a house-chain student, use the house plan and house repro pack instead of their own plan and issue repro. Read the repository's PR template and `CONTRIBUTING.md` or other stated contribution policy. Gather issue-side evidence from the real repository.
- **Eval mode:** Treat the provided package bundle as the whole world. Use only facts in that bundle. Do not fetch the issue, repository, or other files. Grade the complete package by running every rubric check and applying the full verdict rule.

Do not silently substitute missing artifacts or assume evidence that was not provided.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. Confirm the PR belongs to the repository named on its `Repo:` line and apply the house rules recorded there. Refuse to grade a PR outside that repository. If the `Repo:` line still contains an unfilled placeholder, stop without grading and tell the student to fill in that line with their section's Path Review repository. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and check the draft PR title and description against its writing rules. In the readable summary, identify any broken rule and quote or clearly name it. The voice guide does not change the verdict by itself; it changes the verdict only if a rubric check explicitly uses it. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read `rubric.md` for the checks and the rule that combines their grades into a verdict. Use `references/evidence-guide.md` to locate and assess each evidence family. Execute `procedure.md` as written to gather evidence, grade each check, and assemble the verdict.

If the procedure is silent about a step, report the gap instead of inventing a step. If `rubric.md` contains no check content or `procedure.md` contains no procedure content, refuse to grade and explain that the tool needs both a rubric and a procedure.

## Verdict and output

Return only the binary verdict `accept` (ready to submit) or `reject` (hold). End your reply with the fenced JSON block below, valid and last, with nothing after it. Give one evidence-based grade for every rubric check. Use `unclear` when the evidence does not establish pass or fail; apply the rubric's verdict rule to that grade.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
