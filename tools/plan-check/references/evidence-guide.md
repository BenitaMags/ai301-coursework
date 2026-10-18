# Evidence Guide

Use evidence from the supplied issue package to evaluate the candidate plan and its draft comment. In evaluation mode, rely only on the package. In live mode, use the issue and repository evidence available for the task.

## Diagnosis and grounding

**Where to look**
- Issue description and expected behavior
- Reported actual behavior
- Reproduction steps and reproduction results
- Repository facts relevant to the suspected cause
- The diagnosis and explanation in the candidate plan

**What good evidence looks like**
- A specific reproduction result showing the reported failure
- A clear connection between the observed behavior and the proposed cause
- Repository facts that support the proposed explanation
- A distinction between what the evidence establishes and what remains a hypothesis

Do not treat a plausible explanation as proven unless the evidence supports it. A plan that merely repeats the symptom without explaining a plausible underlying mechanism may be insufficient.

## Scope

**Where to look**
- Candidate plan's in-scope and out-of-scope statements
- Proposed files and code locations
- Proposed implementation steps
- Issue requirements and repository contribution conventions
- Relevant thread highlights

**What good evidence looks like**
- A concrete description of the change needed to address the issue
- Files or code locations tied to the proposed change
- Explicit exclusions for unrelated changes
- Evidence-based justification for any broader changes

Check that the plan does not add unrelated features, unnecessary refactoring, or work that belongs to a separate issue.

## Executability

**Where to look**
- Candidate plan's implementation approach
- Named files, functions, or code locations
- Ordered implementation steps
- Relevant repository facts supplied in the package

**What good evidence looks like**
- Specific actions a contributor can follow
- A clear relationship between the proposed change and the reported problem
- Enough detail to begin implementation without inventing the central design
- Assumptions or unknowns called out when repository evidence is incomplete

A plan does not need to prescribe every line of code. It does need to make the central approach understandable and actionable.

## Test plan

**Where to look**
- Original reproduction steps and results
- Candidate plan's proposed tests
- Expected results for each test
- Relevant existing tests or repository test commands mentioned in the package

**What good evidence looks like**
- A test that reproduces the original failure
- An observable expected result after the proposed fix
- Specific test actions and outcomes rather than vague statements such as "test the change"
- Relevant regression checks justified by the affected behavior

Do not count a test as verified merely because the plan proposes it. Distinguish proposed future tests from test results already observed.

## Honesty

**Where to look**
- Candidate plan's claims about the cause, implementation, and test results
- Explicit assumptions, risks, and unknowns
- Repository facts and reproduction evidence
- Candidate comment's claims about work completed or results obtained

**What good evidence looks like**
- Claims that match the supplied evidence
- Assumptions clearly labeled as assumptions
- Unknowns acknowledged rather than presented as facts
- Future work described as planned, not completed
- Test results reported only when the package provides evidence that the tests were run

Do not fill evidence gaps with guesses or outside knowledge. If important evidence is absent, use the rubric's unclear grade when appropriate.

## Comms

**Where to look**
- Candidate draft issue comment
- Issue description and thread highlights
- Repository facts and contribution conventions
- In live mode, voice-guide.md

**What good evidence looks like**
- A concise and accurate summary of the diagnosis and intended change
- A comment that responds to the issue without misrepresenting the discussion
- No unsupported claims that implementation or testing is complete
- Compliance with relevant repository and issue-thread conventions
- In live mode, wording consistent with the voice guide

Evaluate the draft comment separately from the technical plan. A sound plan does not automatically make its comment accurate or appropriate to post.
