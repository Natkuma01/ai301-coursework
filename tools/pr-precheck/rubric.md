# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `diff_matches_plan` | Compare every changed file and substantive hunk in the candidate diff with the plan's stated scope, exclusions, and `## Deviations`. | Pass when every substantive change is covered by the plan or by a deviation that clearly says what changed and why, and every promised plan outcome is present or honestly deferred. Fail for unrecorded extra work, a missing planned outcome, or a claimed deviation that does not account for the mismatch. | required |
| `description_matches_change` | Compare the title and description's summary, issue reference, change list, testing claims, deferrals, and limitations with the diff and plan. | Pass when the description accurately tells a reviewer what the diff does and does not do, names the issue, and discloses any shortfall or departure without claiming work the diff does not contain. | required |
| `fix_specific_evidence` | Compare the plan's fix-specific test plan and original reproduction with the candidate test evidence, including before and after output. | Pass when the evidence exercises the behavior that was broken, shows an observable before and after or an equally decisive failing-to-passing result, and covers every behavior the plan says this PR proves. Fail when it tests only an unchanged control path, relies on a vague claim, or omits a planned failure mode without disclosing the limitation. | required |
| `repository_checks_reported` | Read the repo-facts block's required checks against the candidate test evidence; in live mode use the PR template and `docs/CONTRIBUTING.md` against `test_evidence.md`. | Pass when each repository-required check was run and its actual result is reported. An honest failure or expected no-tests result may pass this evidence check; an omitted check, unsupported "tests pass" statement, or hidden result fails. | required |
| `diff_is_reviewable` | Inspect the unified diff and commit list for debug output, dead or commented-out attempts, TODO debris, unrelated edits, generated noise, and formatting or import churn not needed by the fix. | Pass when the intended change is easy to isolate and no unrelated or leftover material rides along. Necessary mechanical edits may pass when their purpose is clear and they do not bury the change. | required |
| `repository_standards_met` | Compare the repo-facts block's template sections, checklist, contribution policy, changelog or documentation asks, and explicit maintainer direction with the description and diff. | Pass when every applicable stated ask has real content or a truthful N/A explanation, required artifacts are present in the diff, and relevant maintainer direction is addressed. Fail when required template or policy items are visibly skipped or merely asserted without the required artifact. | required |
| `ai_use_disclosed` | Compare the repository's stated AI-use policy in repo facts or contribution docs with the PR description, especially Notes for Reviewers. | Pass when the description gives the disclosure the repository requires, in the contributor's own words when required. Pass when the repository has no disclosure requirement. Fail when a stated disclosure requirement applies but the description omits it or substitutes boilerplate that does not satisfy the policy. | required |
| `reviewer_context_is_clear` | Read the title, description, issue and plan together for a concise explanation of why the change exists, what changed, how it was tested, and any intentionally deferred work. | Pass when a reviewer can understand the bounded change and its known limits without reconstructing the story from the diff. Terse, specific writing passes; length and formatting do not decide the grade. | preferred |

## Verdict rule

Return `accept` only when every required check passes. Return `reject`
when any required check fails or is unclear. Treat `unclear` as a failure
because the package must contain enough evidence to verify readiness.
Preferred checks can improve the review summary but never change the
verdict.
