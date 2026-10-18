# Plan-check procedure

The goal is to grade a candidate plan and draft issue comment, not to create a plan or implement a fix.

## Read order

1. In live mode, read scope.md first. Stop if the repository is outside scope or the repository placeholder is unfilled. In evaluation mode, do not consult live sources.
2. Read rubric.md and references/evidence-guide.md completely.
3. In live mode, read voice-guide.md.
4. Read the complete package in this order: issue description, expected behavior, thread highlights, repository facts, reproduction evidence, candidate plan, and candidate plan comment.
5. Note the reported actual behavior, expected behavior, evidence-supported facts, and missing information before grading.

## Evidence gathering

1. For the diagnosis checks, compare the candidate cause with the issue description and reproduction steps. Record the evidence that supports or contradicts the proposed cause.
2. For scope, record the proposed files, changes, explicit exclusions, and relevant repository conventions.
3. For implementation, identify the stated code locations and concrete actions. Decide whether a contributor could begin without inventing the central approach.
4. For testing, record each proposed action and its observable expected result. Compare these with the original reproduction and the proposed change.
5. For uncertainty, compare factual claims with the supplied evidence. Separate established facts from assumptions, unknowns, and future intentions.
6. For the draft comment, compare its claims with the plan, issue thread, and repository conventions. In live mode, also compare its wording with voice-guide.md.
7. In evaluation mode, use only the package text. Do not fetch external information or infer missing facts from outside knowledge.

## Check execution

1. Evaluate every check in rubric.md in the order written.
2. Grade each check pass, fail, or unclear.
3. Use pass only when the evidence satisfies the stated pass condition.
4. Use fail when evidence shows a substantive contradiction or deficiency.
5. Use unclear only when relevant evidence is genuinely absent or insufficient after checking the locations identified in the evidence guide.
6. For every grade, record a concise supporting quote or specific factual observation.
7. Apply the rubric as written. Do not add criteria, change pass conditions, or substitute personal preferences.
8. In live mode, report voice-guide violations separately and quote the relevant rule. A voice violation changes the verdict only if a rubric check makes it relevant.

## Verdict assembly

1. Apply the verdict rule in rubric.md after grading every check.
2. Accept only if every required check passes. Reject if any required check fails or is unclear.
3. Do not average grades or allow a passing check to cancel a failed required check.
4. Summarize the main reasons for the verdict and identify the most important changes needed for a rejected plan.
5. In live mode, include any voice-guide observations in the readable summary.
6. Output a fenced JSON block containing item, checks, and verdict. Each check must include its exact rubric name, its pass/fail/unclear grade, and concise evidence.
7. Use accept or reject for the verdict. Ensure the JSON is valid and the final output block is the JSON block, with no text after it.
