# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment | The repro report's environment record, including the operating system, relevant runtime or tool versions, repository revision or commit, and any setup details needed for the reported behavior. Compare these details with the issue context and repo-facts block. | Pass if the report records the environment details needed to identify what was tested and those details are consistent with the issue's stated target. If a relevant difference exists, the report must identify it rather than presenting the result as an exact reproduction. | required |
| Steps | The repro report's reproduction steps, including the starting state, commands or actions taken, and inputs needed to trigger the behavior. | Pass if another person with the recorded environment and repository state could follow the steps from the stated starting state to the reported result without needing an unstated action or missing input. | required |
| Behavior shown | The artifacts and output excerpts in the repro report, read against the issue description and the issue context. | Pass if the evidence shows the behavior described by the issue, or clearly shows that the reported behavior could not be reproduced. A result about a different or adjacent behavior does not pass. | required |
| Honesty | The repro report's stated outcome together with the artifacts, output, and other evidence supporting that outcome. | Pass if the stated outcome matches the evidence. A report that honestly says the issue could not be reproduced passes when the evidence supports that statement; a report claiming reproduction without evidence of the issue's behavior fails. | required |
| Conventions | The claim and repro comments, the repository's contribution guidance, and stated classroom or repository conventions. | Pass if the comments follow the applicable contribution and communication conventions stated in the package or repository. Do not treat an AI-related policy as a disclosure requirement in this check. Do not fail this check for premature reproduction or unsupported outcome claims when another check evaluates those issues. | required |
| AI disclosure | The repository or package's stated AI-use policy and the claim and repro comments. | Pass if there is no explicit requirement to disclose AI use, or if an explicit requirement exists and the comments contain the disclosure required by that policy. A policy that merely restricts AI use, requires human-written content, or says AI-generated content may be hidden does not by itself create a disclosure requirement. When the policy explicitly requires disclosure, enforce that requirement without requiring separate evidence that AI assistance occurred. | required |

## Verdict rule

Accept if every required check passes.

Reject if any required check fails.

Unclear counts as fail for the verdict.

A claim-only draft is a special live-mode case: reproduction-dependent checks are reported as `unclear` and are not used to decide the claim-only verdict.

The claim-only verdict is based only on checks whose evidence is applicable to the claim comment and repository conventions.
