# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Where it lives:** In an eval bundle, use the plan-context block's scope and deviation notes, the candidate PR's diff, and its description. In live mode, use `plan.md`, its deviation notes, `git diff main...HEAD`, and the draft PR title and description.

**What good looks like:** Every substantive change and omission is either consistent with the plan or explained in a deviation note. The PR text accurately describes what the diff does and does not deliver.

## Test evidence (harness category: not-tested)

**Where it lives:** In an eval bundle, use the plan-context block's test plan, the candidate PR's test-evidence section, and the repo-facts block's required checks. In live mode, use the plan's test plan, captured test output, CI results, and repository instructions about required checks.

**What good looks like:** Evidence shows an observable result for the changed behavior and how it compares with the expected result. The outcomes of the repository's required checks are available; “tests pass” without identifying a result does not establish what was verified.

## Diff quality (harness category: unreviewable)

**Where it lives:** In an eval bundle, inspect the candidate PR's diff and commit list. In live mode, inspect `git diff main...HEAD` and the branch's commits relative to `main`.

**What good looks like:** The diff makes the issue-related change clear, and unrelated edits or leftover debug code do not obscure it. Formatting changes are acceptable when they support the change and do not bury its substance.

## Standards and comms (harness category: standards-wall)

**Where it lives:** In an eval bundle, use the repo-facts block's PR template asks, stated policy, and any maintainer direction included in the issue context, then compare them with the candidate PR title and description. In live mode, read the repository's PR template and contribution policy, check relevant issue-thread direction, and compare those requirements with the draft title and description.

**What good looks like:** The PR addresses the repository's stated requirements with information relevant to this change. Include disclosures, such as AI-use disclosure, when the repository's stated policy requires them. Boilerplate or ignored maintainer direction does not satisfy a stated ask.
