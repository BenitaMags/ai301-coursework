# Plan-check rubric

Grade whether the candidate plan is sufficiently grounded, scoped, actionable, and testable to implement, and whether its draft issue comment is appropriate to post. Grade the substance of the plan, not its length or formatting.

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis is grounded in evidence | Issue description, reproduction evidence, and the plan's diagnosis | The proposed cause is consistent with the reported actual and expected behavior and the reproduction evidence. The plan does not claim facts that contradict the evidence. | required |
| Cause explains the behavior | Plan's diagnosis and proposed approach compared with the reproduction steps | The plan identifies a plausible underlying mechanism rather than merely restating the visible symptom. The proposed change addresses that mechanism. | required |
| Scope is controlled | Plan's in-scope and out-of-scope statements, files to touch, proposed change, issue's expected behavior, and relevant thread highlights | The proposed change addresses the issue's stated expected behavior and relevant maintainer guidance, and is limited to what is needed. Any broader changes are justified by evidence, and unrelated features or refactors are excluded. A workaround or documentation change alone does not pass when the issue expects the underlying behavior to be fixed. | required |
| Implementation is actionable | Plan's target files or code locations, proposed change, and implementation steps | A contributor can identify the target area and central design well enough to begin without inventing them. Exact function names may be pinned down during implementation when the plan gives a concrete approach and explains how to locate the relevant code. | required |
| Test plan verifies the behavior | Plan's test steps, expected results, and original reproduction evidence | The plan includes observable checks for the reported failure and the expected fixed behavior. Tests are specific enough to determine whether the issue is fixed. Relevant regression checks are included when justified by the proposed change. | required |
| Uncertainty is represented honestly | Plan's stated assumptions, unknowns, and claims compared with available evidence | Unverified assumptions are identified as assumptions or unknowns. The plan does not present unsupported implementation details or test results as established facts. | required |
| Draft comment is accurate and useful | Candidate plan comment, issue context, thread highlights, and repository facts or contribution conventions | The comment accurately summarizes the diagnosis and planned change, does not claim work or results that have not happened, and follows relevant thread and repository conventions. When the repository requires disclosure or review of AI-assisted comments, the comment must account for those requirements. It is concise and useful to maintainers. | required |

## Verdict rule

Return `accept` only when every required check passes. Return `reject` if any required check fails or is unclear. Treat `unclear` as a failure for the verdict because missing evidence does not establish readiness. Preferred checks, if added later, may inform the explanation but do not change the verdict. Do not invent evidence to resolve uncertainty.

## Grading principles

- Cite a specific fact or short quote from the package or live evidence for every check.
- Distinguish a plausible diagnosis from a proven diagnosis. Evaluate whether the plan is supported by the available evidence, not whether the proposed fix is guaranteed to work.
- Do not require a particular implementation merely because it is familiar. Judge whether the proposed approach is justified, scoped, and testable.
- Do not reject a plan solely because it is concise or proposes a small change.
- A passing plan is ready to implement, not proof that the implementation is already correct.
