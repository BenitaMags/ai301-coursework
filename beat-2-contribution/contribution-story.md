# Contribution: Add sync coverage for mismatched task data

Path: `beat-2-contribution/contribution-story.md`

**Contribution Number:** [1]  
**Student:** Benita Magdalene Kingsley Prince  
**GitHub Username:** BenitaMags  
**Issue:** https://github.com/GothenburgBitFactory/taskchampion/issues/410  
**Pull Request:** https://github.com/GothenburgBitFactory/taskchampion/pull/795

---

## Toolkit

**Unit 5: Built and tested an issue scout for first-contribution candidates**

I updated my issue-selection tool into an issue scout with a search strategy and rubric for checking maintainer activity, repository activity, issue scope, availability, contribution policy, and clarity. My first scan did not run because I had left the search queries and ranking filters inside template comments; I moved them outside the comments and reran it. Grading candidate issues taught me that a “good first issue” label alone is not enough when a maintainer has raised an unresolved concern. I recorded scan problems and lessons in my scan notes.

**Unit 6: Voice guard and issue-scout scope patch**

I wrote upstream communication rules for claims, questions, and follow-up pings, then installed the voice guard and its Claude Code hook. I linked the repro-check, plan-check, and PR-precheck tools to the shared voice guide, and changed the repro and plan scopes to allow public repositories. I also patched the issue-scout rubric: a bounded but unfamiliar task can pass the scope-feasible check, while its difficulty is recorded separately. The accepted TaskChampion issue was marked ambitious because Rust and the sync subsystem were new to me and the initial work description was broad. I confirmed a one-test starting scope with the maintainer before coding. The hook is installed; I did not capture a verified hook-block/allow test, so I am not claiming that test passed.

**Unit 7: Ship gate and project manifest**

I installed the ship-gate and added a local manifest for TaskChampion. It names the full Cargo test suite, the SQLite storage feature-matrix command from CI, and a formatting check. I recorded that no applicable checks were excluded. The installer added the gate hook and changed the local PR-precheck scope for real repositories. I did not capture a successful end-to-end hook run on this branch, so the manifest and installation are verified artifacts, but I am not claiming the gate blocked or cleared a PR attempt.

**Unit 8: PR monitor and playbook**

I reviewed five recent merged PRs from non-maintainer contributors to estimate the usual first-response time, then wrote a playbook with response, nudge, and walk-away rules. The monitor found PR #795 approved with 21 checks passing and drafted an optional thank-you. The PR was merged before I posted anything, so I left the draft unposted and recorded the merged outcome.

---

## Why I Chose This Issue

I chose TaskChampion issue #410 after reviewing candidates from the AI301 Issue Selection site and asking my issue scout to grade it. The scout accepted it, and the maintainer suggested starting with one integration test. I wanted to learn how TaskChampion keeps task data and operation history consistent and how its sync tests work. Rust was new to me, and the issue’s overall scope was broad, so I asked the maintainer about a focused first test before coding. The maintainer approved my proposed test, and I added coverage for a manually changed SQLite task row while checking that sync succeeds and an unrelated task stays unchanged.

The scout helped me compare activity, availability, scope, and repository policies, but its “accept” verdict did not mean the issue was automatically a perfect fit. I still needed to consider that the codebase uses Rust and clarify the starting scope with the maintainer. My claim comment is https://github.com/GothenburgBitFactory/taskchampion/issues/410#issuecomment-6754590645.

**Toolkit**

- Tool: issue-scout, using my search strategy and rubric to scan and grade candidates.
- What it produced: Candidate issue results and an accepted verdict for TaskChampion #410.
- Difficulties: My first scan did not run because queries and ranking filters were inside template comments. Later, the scan favored very new issues, and the accepted issue used a language outside my stated experience. The first rubric treated an open design edge as an automatic scope failure.
- What changed: I moved the queries and filters outside the comments, recorded ranking and fit problems in scan notes, then patched the rubric to separate bounded scope from difficulty. I marked TaskChampion ambitious and asked the maintainer to confirm a focused starting scope.

---

## Understanding the Issue

**Problem Description**

TaskChampion stores current task data and its operation history separately. If someone edits the SQLite database directly, those can disagree and violate the replica invariant. The issue asks for tests showing how sync behaves when that happens.

**Expected Behavior**

Sync should complete without crashing, and the effects of a manual database edit should stay limited to the affected task. Other tasks should remain consistent between replicas.

**Current Behavior**

The issue concerns missing test coverage rather than a specific reported crash. In my test, I manually changed one task’s SQLite data without changing its operation history. Sync completed; that task remained different between the replicas, while the other task stayed the same on both.

**Affected Components**

The SQLite `tasks` and `operations` tables hold state that can become inconsistent. Sync behavior is handled in `src/taskdb/sync.rs` and `src/taskdb/apply.rs`. My integration test is in `tests/sqlite-task-mismatch-sync.rs`.

**Toolkit**

- Tool: GitHub issue #410, the TaskChampion source and test files, and my local `CLAUDE.local.md` repo-memory notes.
- What it produced: An understanding of the replica invariant, current test locations, build commands, and existing sync-test patterns.
- Difficulties: The issue linked to an older test path, and the existing sync tests used in-memory storage.
- What changed: I used the current SQLite storage and sync APIs in a separate integration test after confirming the test scope with the maintainer. The repo-memory file is local and excluded from Git.

---

## Reproduction Process

**Environment Setup**

I used macOS with Rust `rustc 1.99.1 (58cf8f9c3 2026-10-13)` and Cargo `1.99.1 (5f94df478 2026-08-27)`. I cloned the TaskChampion repository and ran the integration tests with Cargo.

**Steps to Reproduce**

1. Create a SQLite-backed replica with two tasks and sync it to a second replica.
2. Close the SQLite-backed replica. Directly change one task’s `description` in the SQLite `tasks` table without changing the `operations` table.
3. Reopen the replica and sync both replicas.

**Reproduction Evidence**

- **Commit showing reproduction:** https://github.com/BenitaMags/taskchampion/commit/e18ef72d71e28393a43ed9341efb3d4f5ad05b89
- **Screenshots/logs:** The focused integration test passed: 1 passed. The full `cargo test` run also passed.
- **My findings:** The manual edit creates a mismatch between the task row and operation history. In this test, sync completed, the edited task stayed different between replicas, and the other task remained unchanged.

**Toolkit**

- Tool: Terminal, Cargo, and the TaskChampion integration-test setup.
- What it produced: A repeatable SQLite-backed test for a manual task-data edit followed by sync.
- Difficulties: The initial sync tests used in-memory storage, so they could not create the SQLite mismatch.
- What changed: I added a separate SQLite-backed integration test and verified it with the focused test and full test suite.

---

## Solution Approach

**Analysis**

A manual edit to the SQLite `tasks` row can break the replica invariant without changing the `operations` table. The issue asks for tests that check how sync behaves in these situations.

**Proposed Solution**

Add an integration test that manually changes one task’s SQLite data while leaving its operation history unchanged. Verify that sync completes, that the edited task may differ between replicas, and that an unrelated task remains unchanged on both. This PR adds test coverage and does not change production code.

**Implementation Plan**

1. Create two tasks in a SQLite-backed replica and sync them to a second replica.
2. Edit one task’s `description` directly in the SQLite `tasks` table without changing its operation history.
3. Reopen the local replica, sync both replicas, and assert the described outcomes.

**Toolkit**

- Tool: Codex for help understanding the Rust test APIs, and Terminal/Cargo to edit, format, and run the test.
- What it produced: One SQLite-backed integration test for a manually changed task row.
- Difficulties: The existing sync examples used in-memory storage, and the first test draft needed formatting.
- What changed: I used SQLite storage in a separate integration test, formatted it with `cargo fmt`, and confirmed the test and full suite passed.

---

## Testing Strategy

I first ran the existing update/delete sync integration test as a baseline; both tests passed, but they use in-memory storage and do not cover a manual SQLite edit. The new test creates and syncs two tasks, changes one task’s SQLite `description` without changing its operation history, then syncs both replicas. It passes and confirms that sync completes, the manually edited task differs between replicas, and the other task remains unchanged on both.

Verification:

- `cargo test --manifest-path /Users/benz.mags/taskchampion/Cargo.toml --test sqlite-task-mismatch-sync` — 1 passed.
- `cargo fmt --manifest-path /Users/benz.mags/taskchampion/Cargo.toml -- --check` — passed.
- `cargo test --manifest-path /Users/benz.mags/taskchampion/Cargo.toml` — 432 unit tests passed; integration and doc tests passed.
- GitHub CI on PR #795 — the PR monitor recorded 21 passing checks before approval and merge.

**Toolkit**

- Tool: Cargo for formatting and running tests; GitHub Actions for CI results.
- What it produced: Local test results and CI confirmation for the proposed sync scenario.
- Difficulties: The pre-existing sync test was not enough because it used in-memory storage.
- What changed: I added a separate SQLite-backed test and checked that it and the full suite passed.

---

## Implementation Notes

**2026-11-10 to 2026-11-11 (Eastern)**

After the maintainer approved a focused integration test, I cloned TaskChampion, read its contribution guide, and ran the existing update/delete sync tests as a baseline; both passed. Those tests used in-memory storage, so I added a separate SQLite-backed test that manually changes one task row and checks sync behavior. My first formatting check found changes to make, so I ran `cargo fmt`; the focused test, full suite, and formatting check then passed. I opened PR #795. GitHub reported all 21 checks passing; maintainer djmitche approved it with “This looks good!”, and it was merged at 2026-11-12 02:30 UTC (November 11 Eastern). I used Codex for guidance and ran the commands and tests myself.

**Toolkit**

- Tool: Git, Terminal, Cargo, GitHub, and Codex for coding guidance.
- What it produced: A tested integration-test commit and PR #795.
- Difficulties: The existing sync example used in-memory storage, and my first test draft needed formatting.
- What changed: I used SQLite storage in a new test, formatted it, and ran the focused and full test suites.

---

## Pull Request

**PR Link:** https://github.com/GothenburgBitFactory/taskchampion/pull/795

**PR Description:** Adds an integration test that changes one SQLite task row without changing its operation history, syncs both replicas, and checks that the other task remains unchanged. Closes #410.

**Maintainer Feedback:**

- 2026-11-10: Maintainer djmitche approved my plan to start with one focused integration test.
- 2026-11-11 (Eastern): Maintainer djmitche submitted an approval with the comment “This looks good!” No changes were requested. The monitor recorded 21 passing checks.

**Status:** Merged at 2026-11-12 02:30 UTC (November 11 Eastern). I did not post the monitor’s optional thank-you draft because the PR was already merged.

**Toolkit**

- Tool: Git, GitHub CLI, GitHub Actions, and the Unit 8 PR monitor.
- What it produced: PR #795, an approved review, 21 passing checks, and a merged contribution. The monitor drafted an optional response; I left it unposted after the merge.
- Difficulties: My clone initially pointed to the upstream repository, so I needed to create my fork and configure the remotes before pushing.
- What changed: I pushed the branch to my fork and opened the PR against the upstream repository, then tracked review feedback and the merge with the monitor.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned how TaskChampion’s `Replica` sync uses task operation history, how SQLite stores task maps in the `tasks` table, and how to use `rusqlite` in an integration test to edit a temporary database directly. I also learned to run a focused Cargo test, the full Rust test suite, and the formatting check.

**Challenges Overcome**

The issue linked to an older test path, and the existing sync example used in-memory storage rather than SQLite. I inspected the current repository, found the SQLite storage and sync APIs, and confirmed a narrow test scope with the maintainer. Rust was new to me, so I used Codex to help me understand the APIs and then ran and checked the test myself.

**What I'd Do Differently Next Time**

I would check the current repository layout and storage type earlier, and run `cargo fmt --check` before reviewing a test draft. I would also keep dated notes on commands and results as I go, so the contribution story is easier to complete.

---

## Resources Used

- [Assignment 5 instructions](https://github.com/codepath/ai301-unit5-starter)
- [Unit 6 voice-guard materials](https://github.com/codepath/ai301-unit6-starter)
- [Unit 7 ship-gate materials](https://github.com/codepath/ai301-unit7-starter)
- [Unit 8 PR-monitor materials](https://github.com/codepath/ai301-unit8-starter)
- [AI301 Issue Selection site](https://ai301-issue-selection.vercel.app/)
- [TaskChampion issue #410 and maintainer guidance](https://github.com/GothenburgBitFactory/taskchampion/issues/410)
- [TaskChampion contribution guide](https://github.com/GothenburgBitFactory/taskchampion/blob/main/CONTRIBUTING.md)
- [TaskChampion replica invariant](https://gothenburgbitfactory.org/taskchampion/sync-model.html#replica-invariant)
- [Existing update/delete sync test](https://github.com/GothenburgBitFactory/taskchampion/blob/main/tests/update-and-delete-sync.rs)
