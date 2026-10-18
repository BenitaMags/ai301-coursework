# Plan: Fix parenthesized US phone number detection

## Diagnosis

The `phone_us` pattern in `safety/pii_scrubber.py` has two relevant limitations. Its leading `\b` cannot start a match at the opening `(` in `(555) 123-4567`, so a match that starts at the digits would leave the opening parenthesis outside the redacted value. Also, the optional separators accept hyphens and periods but not spaces. That prevents a complete match of the space after the closing parenthesis and the spaces in `+1 555 123 4567`.

My reproduction confirms that the parenthesized number is left unchanged and `detect()` returns no match, while the dashed control is redacted. Since `scrub()` and `detect()` use the same `phone_us` pattern, these pattern gaps explain both results.

## Scope

In scope:

- Update the US phone pattern in `safety/pii_scrubber.py` to match the full parenthesized number and the spaced US formats covered by the existing issue tests.
- Update the phone tests in `tests/unit/test_pii_scrubber.py`: verify detection includes the opening parenthesis, and remove the strict `xfail` markers from the four phone tests once they pass.

Out of scope:

- Changes to international phone, email, SSN, or address patterns.
- `test_mixed_pii_and_text` and its strict `xfail` marker. I ran `pytest tests/unit/test_pii_scrubber.py -q --runxfail -k test_mixed_pii_and_text`; it fails at `assert "Python" in scrubbed`, and the output contains `[REDACTED]ications.` The dashed phone in that test is redacted. This evidence points to a separate false positive in the existing address pattern, so I will leave that test and pattern unchanged.
- A general redesign of PII detection or redaction.

## Planned branch

`fix/53-parenthesized-us-phone`

## Files to touch

- `safety/pii_scrubber.py`
- `tests/unit/test_pii_scrubber.py`

## Approach

Adjust the US phone pattern’s start and end boundaries so a match can include a leading `(` while still rejecting numbers embedded in word characters. Allow spaces as optional separators where the US phone pattern currently accepts hyphens or periods, including after the optional country code and between digit groups.

Keep the change limited to the US phone pattern. Add or strengthen an assertion that `detect()` returns the complete value `(555) 123-4567`. Remove the strict `xfail` markers from the four phone tests after they pass. Leave the marker on `test_mixed_pii_and_text` because its failure is a separate address-pattern issue.

## Test plan

1. Re-run the Unit 2 reproduction:

   ```python
   from safety.pii_scrubber import PIIScrubber
   s = PIIScrubber()
   print(s.scrub("Call me at (555) 123-4567 or 555-123-4567"))
   print(s.detect("Call me at (555) 123-4567"))
   ```

   Expected scrub output: `'Call me at [REDACTED] or [REDACTED]'`. Expected detection: a `phone_us` match whose value is `(555) 123-4567`, including the opening parenthesis.

2. Run `test_us_phone_number_redaction`, `test_us_phone_formats`, `test_detect_phone_pii`, and `test_phone_at_start_of_text` without their `xfail` markers. Expected: all pass, including the `+1 555 123 4567` case in `test_us_phone_formats`.

3. Run the full `tests/unit/test_pii_scrubber.py` file normally. Expected: the four phone tests pass after their `xfail` markers are removed, `test_mixed_pii_and_text` remains xfailed for the separate address-pattern failure described above, and the suite passes.

## Risks and unknowns

Changing boundaries and allowing spaces could match inputs beyond the reported examples. I will keep the change limited to the US phone pattern and check that numbers embedded in word characters are still excluded, along with the existing non-parenthesized formats.

## Deviations

The plan held. The phone pattern and its tests were the only code files changed. The focused phone tests passed (7 passed), and the full PII scrubber test file passed (25 passed, 1 xfailed). The full project suite could not be collected because the environment is missing dependencies, including numpy, rank-bm25, redis, pypdf, sqlalchemy, and jose. The existing `test_mixed_pii_and_text` xfail remains because it fails on the unrelated address-pattern behavior documented above.
