# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives:** In the repro report's environment record. In eval mode, use the environment details in the candidate report and compare them with the issue context and repo-facts block. In live mode, use the student's draft report and compare its recorded environment with the issue and the repository's documented setup requirements.

**What good looks like:** The record identifies the operating system, relevant runtime or tool versions, repository revision or commit, and setup details needed to understand the test. Details match the issue's stated target, or any relevant differences are clearly identified instead of being presented as an exact match.

## Steps

**Where it lives:** In the repro report's reproduction steps. In eval mode, use the steps and inputs in the package bundle. In live mode, use the student's draft report, including commands, actions, starting state, and any required input or configuration.

**What good looks like:** A stranger can follow the steps from the stated starting state to the reported result using the recorded environment and repository state. Required commands, actions, and inputs are present; the reader does not have to guess or supply an unstated step.

## Behavior shown

**Where it lives:** In the repro report's artifacts and output excerpts, read against the issue description. In eval mode, compare the included evidence with the issue context in the bundle. In live mode, compare the student's artifacts with the issue's stated behavior and any relevant issue-thread details.

**What good looks like:** The evidence demonstrates the specific behavior the issue describes, not merely a related symptom or nearby feature. If the behavior does not occur, the artifacts show what was tested and what happened, supporting a cannot-reproduce outcome rather than implying that the issue was confirmed.

## Honesty

**Where it lives:** In the repro report's stated outcome and the artifacts or output that support it. In eval mode, compare the report's conclusion with its included evidence and issue context. In live mode, compare the student's draft conclusion with the evidence in the draft and the behavior described in the issue.

**What good looks like:** The conclusion says only what the evidence supports. A cannot-reproduce result can be a pass when the report clearly records the attempt and the observed result; claiming a reproduction is not supported when the artifacts do not show the issue's behavior.

## Comms

**Where it lives:** In the claim and repro comments, compared with the issue thread, the repository's contribution guidance, and any stated classroom or repository conventions. In eval mode, use the comments and convention evidence included in the package bundle. In live mode, inspect the draft comments, issue thread, and applicable repository guidance. Check for any explicit AI-use disclosure requirement.

**What good looks like:** The claim identifies the issue and describes the investigation the student plans to do, without claiming that reproduction has already happened or promising a fix or deadline. The repro comment reports the student's own work and evidence, including on a shared issue; it does not piggyback on another person's reproduction. Comments follow applicable repository conventions and include any AI-use disclosure the repository explicitly requires.
