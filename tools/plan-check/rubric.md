# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `diagnosis_matches_evidence` | Compare the plan's diagnosis with the steps, output, and error in the reproduction evidence. Use the Diagnosis and grounding section of `references/evidence-guide.md`. | Pass when the diagnosis clearly explains the behavior shown in the reproduction evidence. Fail when it contradicts the evidence, assumes a different cause, or makes claims the evidence does not support. | required |
| `change_addresses_cause` | Compare the proposed approach with the diagnosis and the reproduction evidence. | Pass when the proposed change addresses the cause identified by the evidence rather than only treating the visible symptom. The plan should make it clear how the change will prevent the reproduced failure. | required |
| `scope_is_bounded` | Review the plan's stated scope, exclusions, and named files or code areas against the issue. Use the Scope section of `references/evidence-guide.md`. | Pass when the plan stays focused on the issue and describes one bounded change. Fail when it includes unrelated cleanup, a broad redesign, or additional features that are not necessary for the fix. | required |
| `approach_is_executable` | Review the files, functions or code areas, and implementation steps named in the plan. Use the Executability section of `references/evidence-guide.md`. | Pass when another contributor could begin the work without needing clarification about where to start or what outcome to produce. A minor detail may remain open if the plan identifies it and explains how it will be resolved. | required |
| `test_plan_proves_result` | Compare the proposed test steps and expected results with the reproduction evidence. Use the Test plan section of `references/evidence-guide.md`. | Pass when the test plan repeats the reproduced case, defines the expected behavior after the fix, and checks that related existing behavior still works. Fail when it only says to run tests or does not identify an observable result. | required |
| `risks_are_honest` | Review the plan's risks, unknowns, assumptions, and any recorded deviations against the rest of the package. Use the Honesty section of `references/evidence-guide.md`. | Pass when the plan acknowledges meaningful uncertainty and does not present untested assumptions as established facts. If the implementation changed from the plan, the deviation should explain what changed and why. | required |
| `comment_follows_context` | Compare the plan comment with the issue, thread highlights, repository facts, contribution guidelines, templates, and any AI-use requirements. Use the Comms section of `references/evidence-guide.md`. | Pass when the comment is specific to the issue, describes the contributor's own plan, responds to relevant maintainer guidance, and follows the repository's communication requirements. Fail when it is generic, copies another contributor's plan, or ignores a required convention. | required |

## Verdict rule

Accept the package only when every required check passes. Reject it if any
required check fails or is unclear. Treat an unclear result as a failure
because a plan should contain enough evidence to support a confident
decision before it is posted and used for implementation. Preferred checks,
if added later, do not affect the final verdict.
