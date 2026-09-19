# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/53

**Verdict output**

Live-mode output of `issue-select` for this issue, pasted verbatim:

````
Scope confirmed: the candidate is in codepath/pathreview-ai301-fa26-s3.

Evidence gathered. Grading against `rubric.md`:

- **Maintainer activity** — pass: default-branch commit `chore: track five more
  manifest entries against the tracker` by human author `Aburke225` on 2026-09-16,
  3 days before today, well inside the 90-day window.
- **Repository activity** — pass: `archived: false`, `pushed_at: 2026-09-16T21:50:20Z`,
  a default-branch commit inside 180 days.
- **Newcomer scope** — pass: one coherent bounded deliverable (extend one
  phone-number regex in `safety/pii_scrubber.py`), four named failing tests, and a
  maintainer-applied `good first issue` label as positive evidence.
- **Available to contribute** — pass: `assignees: []`, no linked PRs in the issue
  timeline, `comments: 0`.
- **Attempt history** — pass: zero linked PRs closed without merging; no
  claim/abandon pattern in an empty thread.
- **Contribution policy** — pass: `docs/CONTRIBUTING.md` exists and contains no
  mention of AI, LLM, generated code, or disclosure; silence passes.
- **Issue clarity** (preferred) — pass: runnable repro with observed output and
  named failing tests.

All required checks pass → accept. Fit: this is the top-ranked kind of candidate
for the profile in `scope.md` — Python plus a regex fix inside a `safety/`
PII-redaction module, which sits directly on the stated security/AI interest with
no unfamiliar framework required.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/53",
  "checks": [
    {"name": "Maintainer activity", "grade": "pass", "evidence": "Default-branch commit 2026-09-16T21:42:18Z authored by human Aburke225: 'chore: track five more manifest entries against the tracker' (3 days ago, within 90)"},
    {"name": "Repository activity", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16T21:50:20Z, a default-branch commit within the past 180 days"},
    {"name": "Newcomer scope", "grade": "pass", "evidence": "One bounded fix to the phone-number pattern in pii_scrubber.py, with four named failing tests; labels include maintainer-applied 'good first issue'"},
    {"name": "Available to contribute", "grade": "pass", "evidence": "assignees: [], no linked PRs in the issue timeline, comments: 0"},
    {"name": "Attempt history", "grade": "pass", "evidence": "Zero linked PRs closed without merging and no unanswered maintainer question in an empty comment thread"},
    {"name": "Contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no mention of AI, LLM, generated code, or disclosure requirements; no ban stated"},
    {"name": "Issue clarity", "grade": "pass", "evidence": "Body gives a runnable repro with observed output: \"observed: 'Call me at (555) 123-4567 or [REDACTED]'\""}
  ],
  "verdict": "accept"
}
```
````

---

## Eval iterations

**Run history**

One full run. Its agreement score, quoted from the final line of the committed
`eval-run.txt`:

```
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

That is the last (and only) score in my list, and it is the agreement line of the
`eval-run.txt` committed in this directory. The header of that file fingerprints the
rubric it graded:

```
#   rubric.md  sha256:16abef3abfa9042f
#   SKILL.md  sha256:bbb295bf984701fd
```

Both fingerprints match the current `tools/issue-select/rubric.md` and `SKILL.md`, so
the committed run is the record of the rubric as it now stands.

**Issue analysis**

`issue-19`. My rubric's decision, the gold label, and the note, quoted from the
results table in `eval-run.txt`:

```
issue-19  accept  reject   NO     failed: Newcomer scope
```

The gold label is `accept`; my rubric produced `reject`. The `note` column names the
required check that produced it: `Newcomer scope`. That check is the only untagged
failure listed, so it alone caused the reject.

The reasoning that produced it is visible in the bundle. `issue-19` is
`zxcalc/zxlive#517`, "Selecting large subgraphs in proof mode freezes the UI", and its
body opens:

```
There are two potential causes which should be fixed:
1. The matchers are slow for certain rewrites (quadratic instead of linear)
2. UI update is waiting for the matching thread to finish

Additional suggestions:
1. We should use multi-processing to use all the cores to match rewrites in parallel
```

That trips two of my three enumerated failure shapes at once. The body is a numbered
checklist of separable fixes, which my condition reads as an umbrella issue, and the
approach is plainly unsettled — "two *potential* causes", "additional *suggestions*",
with no maintainer having picked one and no comments in the thread to settle it, so it
also reads as "a proposal whose approach is still an open design question the
maintainers have not settled." The gold label says a newcomer could still take the
first listed cause as one bounded fix; my check saw the list and the tentative framing
and rejected the whole issue. It is one of exactly two disagreements in the run; the
other, `issue-01`, failed on the same check:

```
issue-01  accept  reject   NO     failed: Newcomer scope
```

Both misses are false rejects concentrated in a single check, which is the signal
that my Newcomer scope condition is tuned conservatively rather than that six
different checks are each slightly wrong.

**Check rationale**

The `Newcomer scope` check from `tools/issue-select/rubric.md`, quoted as it is
currently written:

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Newcomer scope | Issue body, issue labels, and comment thread | Pass if the issue asks for one coherent, bounded deliverable a newcomer could finish in a single pull request. Fail only if it is an umbrella/tracking issue whose body is a checklist of separate sub-issues, a pure usage or support question, or a proposal whose approach is still an open design question the maintainers have not settled. Several files or sub-steps inside one coherent deliverable still pass, and a maintainer-applied `good first issue` or `help wanted` label is positive evidence of bounded scope | required |

The reasoning behind its current form: an earlier, looser version of this check
rejected on vaguer grounds — short bodies, missing reproduction steps, anything that
read as unpolished. The evidence guide is explicit that this is the wrong axis:
"Short is not the same as unscoped... Grade the size of the work being asked for, not
the polish of the writeup." So I rewrote the pass condition as a default-pass with
three enumerated failure shapes ("Fail only if...") instead of a default-fail on
adjectives. I also added the two clauses at the end — that sub-steps inside one
deliverable still pass, and that a maintainer-applied `good first issue` label is
positive evidence — because the check was otherwise punishing bounded work that
merely spanned a few files, and was ignoring the strongest signal a maintainer can
give about scope.

**Trade-offs**

What this check gives up: by enumerating only three failure shapes and defaulting to
pass otherwise, it cannot fail an issue that is genuinely too large but is written as
a single coherent-sounding request — a one-sentence "add OAuth support" that touches
core internals reads as one bounded deliverable to this condition and passes. The
evidence guide names that shape ("a maintainer says outright that the fix touches core
internals") and my current wording does not encode it.

The cost of that is visible in the committed run: `issue-01` and `issue-19` are both
still false rejects on this check, so the loosening did not go far enough to catch
them, while the guard against over-rejecting on polish is what keeps the other
eighteen in agreement. I accept the miss on those two. The run clears the bar at
`18/20` with the category floor held — `categories: claimed 4/4  clear-accept 6/8
dead-repo 3/3  policy 1/1  scope 4/4` — and the two misses sit inside `clear-accept`,
the only category not at full marks. Tightening the check further to catch a
disguised-large issue would risk re-introducing the polish-based rejects that the
current wording was written to remove, which would cost more than the two it would
gain.

---

## Selection rationale

**Selection rationale**

**Fit to my interests and the time available.** Issue #53 is a PII redaction bug in
`safety/pii_scrubber.py` — the phone-number pattern catches `555-123-4567` but misses
`(555) 123-4567`, so a common US format passes through `scrub()` unredacted. That is
squarely where I want to be working. It is a safety and privacy control in an AI
application, which is the security/AI intersection I care about, and it is Python and
regex, both of which I have actually used rather than would be learning from scratch.
On time: the issue names the exact file and lists four failing tests
(`test_us_phone_number_redaction`, `test_us_phone_formats`, `test_detect_phone_pii`,
`test_phone_at_start_of_text`), so I know where the work starts and what tells me it
is done. I do not have to reverse-engineer the scope before I can estimate it, which
is what usually makes a first issue eat a weekend.

**What the verdict got right, and what I weighed beyond it.** The rubric was right on
the mechanical facts, and those are the ones I would have gotten wrong by eyeballing:
the repo is live (a human commit three days ago, not a bot), nobody is on the issue
(no assignees, no linked PRs, an empty thread), there is no abandoned-attempt history,
and `docs/CONTRIBUTING.md` says nothing that bans AI-assisted work. Confirming all of
that by hand is exactly the tedious part I built the skill to stop skipping.

What the rubric could not weigh is whether I will actually do a good job on it. It has
no opinion on the fact that a redaction bug has a real failure mode I understand — PII
leaking into logs or model context — which makes me more likely to think about edge
cases the tests do not name, like extensions, country codes, or `(555)123-4567` with no
space. I also considered that a regex fix is easy to over-fix: the tempting move is to
write one pattern that swallows every phone format on earth and start producing false
positives on things that are not phone numbers. The rubric graded whether the issue is
takeable. It did not, and could not, tell me that the hard part here is restraint.

**Anticipated difficulty in claiming it.** Low, mechanically. The issue is unassigned
with zero comments, so there is nothing to negotiate, and the Path Review house rule in
`scope.md` means classmates' claim comments would not block me even if some appear
before I post. The real difficulty is not the claim, it is after it: the repo's PR
template requires CI green on all five jobs (`make test-unit`, `make test-integration`,
`make lint`, `make typecheck`, plus test coverage), and it asks me to remove the
`@pytest.mark.xfail` marker on the seeded bug and any matching suppression in
`pyproject.toml`. If I miss that last step the tests will keep reporting as expected
failures and my fix will look like it did nothing. That is the part I expect to trip on,
so it is the part I will check first.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
