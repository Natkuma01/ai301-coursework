# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. In live mode, read `scope.md` first, confirm that the issue belongs to the named repository, and record the Path Review house rules. Then read `voice-guide.md`. In eval mode, skip both files.
2. Read `rubric.md` and `references/evidence-guide.md`. List every check, its weight, and the verdict rule before looking at the candidate plan so that the candidate's wording does not change the standard being applied.
3. Read the issue context and thread highlights. Record the requested outcome, explicit maintainer direction, and any limits or open questions in the thread.
4. Read the repo-facts block in eval mode, or the repository's contribution guide, issue template, and relevant AI-use policy in live mode. Record every convention that the plan comment must follow.
5. Read the reproduction evidence before the candidate plan. Record the triggering input or steps, actual output, expected output, controls, and the narrowest cause the evidence supports.
6. Read the complete candidate plan and then the candidate plan comment. Record the stated diagnosis, in-scope and out-of-scope work, named files or code areas, implementation steps, tests and expected results, risks, unknowns, and deviations. Reading the evidence first prevents a confident plan from replacing what the reproduction actually proved.

## Evidence gathering

1. For diagnosis and grounding, place the plan's cause beside the reproduction's triggering steps, actual output, controls, and failure location. Record one quote or fact that supports or contradicts the cause.
2. For cause-to-change alignment, place the proposed implementation beside the grounded diagnosis. Record the mechanism by which the change would prevent the reproduced behavior; if the plan only masks an output or error, record that mismatch.
3. For scope, compare the issue's requested outcome with the plan's in-scope work, exclusions, named files, and any additional refactors, migrations, options, or features. Record whether each extra item is necessary for the one requested outcome.
4. For executability, extract the first actionable implementation step, the file, function, or code area where it occurs, and the intended result. Record any decision deferred to build time that would prevent another contributor from starting.
5. For the test plan, map each proposed test to the reproduced input or steps. Record the command or action, the observable post-fix result, and any regression or control check for related existing behavior.
6. For honesty, compare the plan's certainty with the limits of the reproduction and thread evidence. Record meaningful risks or unknowns and, after a build, whether each departure from the original approach is named with a reason under Deviations.
7. For communications, compare the comment with the issue, thread direction, repo conventions, templates, and AI-disclosure policy. Record the exact direction or convention it follows or misses, and whether it states the contributor's own specific diagnosis, scope, and test intent.

## Check execution

1. Grade `diagnosis_matches_evidence` first, using only the diagnosis-and-grounding comparison. Do not let a plausible implementation rescue a diagnosis contradicted by the reproduction.
2. Grade `change_addresses_cause` next, using the grounded diagnosis and the proposed change. If the diagnosis failed, still grade this check independently against the cause the reproduction actually supports.
3. Grade `scope_is_bounded`, then `approach_is_executable`, from the recorded scope and execution facts. A terse plan may pass when it names a concrete starting point and result; length and formatting are not evidence.
4. Grade `test_plan_proves_result` from the test mapping. Running a broad suite alone is not an observable check of the fix.
5. Grade `risks_are_honest` from the evidence limits, risks, unknowns, and deviations. The absence of a risk is not automatically a failure when the package presents no meaningful uncertainty; unsupported certainty is.
6. Grade `comment_follows_context` last, from the comment-to-context comparison. Apply explicit maintainer direction and repository requirements exactly as written.
7. Assign `pass` when the gathered evidence meets the check's pass condition, `fail` when it contradicts or misses that condition, and `unclear` only when the required evidence is genuinely absent or too ambiguous to decide. For every grade, write one concise quote or fact from the recorded evidence. Do not reread the whole package unless two recorded facts conflict.

## Verdict assembly

1. Verify that every rubric row has one `pass`, `fail`, or `unclear` grade and a one-line evidence statement.
2. Apply the rubric rule mechanically: return `accept` only if every required check passes. Return `reject` when any required check fails or is unclear. Preferred checks never change the verdict.
3. In the readable summary, name each grade. For a rejection, quote the fact for every required check that failed or was unclear; for an acceptance, quote the most specific grounding and test facts that establish readiness.
4. In live mode, add any voice-guide violation to the summary without changing the verdict unless a rubric check also covers it.
5. Emit the required fenced JSON object with the issue URL or package id, all checks in rubric order, their grades and evidence, and the binary verdict. Put nothing after the JSON block.
