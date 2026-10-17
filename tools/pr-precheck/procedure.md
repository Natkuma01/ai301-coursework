# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. In live mode, read `scope.md` first and verify the target repository;
   then read `voice-guide.md`. In eval mode, skip both.
2. Read `rubric.md` and `references/evidence-guide.md`. Record each
   check, its weight, and the verdict rule before reading the candidate.
3. Read the issue and thread, followed by the repo facts in eval mode or
   the PR template and `docs/CONTRIBUTING.md` in live mode. List the
   requested outcome, maintainer direction, template sections, required
   checks, documentation or changelog asks, and AI policy.
4. Read the plan and its deviation notes before the diff. Record promised
   outcomes, in-scope files or areas, explicit exclusions, test cases,
   expected results, and disclosed departures.
5. Read the entire unified diff and commit list. Note every changed file,
   each substantive behavior change, missing planned work, and any debris
   or unrelated churn.
6. Read the test evidence and map each result to the plan's tests and the
   repository's checks.
7. Read the candidate title and description last. This keeps its claims
   from shaping the independent reading of the plan, diff, and evidence.
   Record what it says changed, what it says was tested, its issue link,
   its limitations, and its policy disclosures.

## Evidence gathering

1. Build a plan-to-diff ledger. For every changed file and substantive
   hunk, point to the plan scope or deviation that authorizes it. Then
   mark every promised outcome as present, deferred with a reason, or
   absent.
2. Build a description-to-diff ledger. Match each summary and Changes
   claim to a visible diff hunk, and record any changed behavior the
   description leaves out. Check the issue reference and stated
   limitations against the issue and plan.
3. Build a test ledger. For every fix-specific case in the plan, record
   the exact command or action, the behavior before, the behavior after,
   and whether the evidence exercised the changed path. Keep controls
   separate from proof of the fix.
4. Build a repository-check ledger from the stated required commands.
   Record the actual result shown for each command, including honest
   failures and expected no-tests outcomes.
5. Inspect the full diff for temporary logging, commented-out attempts,
   dead helpers, TODO markers, unrelated files, repeated lines, formatting
   churn, import churn, and generated changes. Record a concrete hunk or
   file for every concern.
6. Build a standards ledger from each applicable template, policy,
   changelog, documentation, and maintainer ask. Match it to real content
   in the description or a required artifact in the diff. Record the AI
   policy separately and quote the candidate disclosure when present.
7. In live mode, compare the title and description with every relevant
   voice-guide rule and record violations for the summary only, unless a
   rubric check also fails on the same evidence.

## Check execution

1. Grade checks in rubric order using the corresponding ledger. Do not
   let a polished description override contradictory diff or test facts.
2. Grade `diff_matches_plan` from the plan-to-diff ledger, then
   `description_matches_change` from the description-to-diff ledger.
   Honest, recorded deferrals may pass; silent additions, omissions, and
   contradicted fidelity claims fail.
3. Grade `fix_specific_evidence` and `repository_checks_reported`
   independently. A passing suite does not replace proof of the broken
   behavior, and a good before/after does not prove required checks ran.
4. Grade `diff_is_reviewable` from the complete diff, not just the fix
   hunk. One concrete debug or dead-code artifact is enough to fail when
   it remains in the submitted change; harmless necessary mechanical
   edits are not debris.
5. Grade `repository_standards_met` and `ai_use_disclosed` from explicit
   repository asks. Do not invent standards that are absent. When an ask
   is stated, do not excuse it because the code itself is strong.
6. Grade `reviewer_context_is_clear` last. Keep it preferred and do not
   use it to override any required grade.
7. Assign `pass` when the recorded evidence meets the stated condition,
   `fail` when it contradicts or misses it, and `unclear` only when the
   needed evidence is genuinely missing or ambiguous. Attach one concise,
   package-specific fact or quote to every grade. Re-read only the
   relevant source when ledger entries conflict.

## Verdict assembly

1. Confirm that every rubric row has one grade and one evidence line.
2. Apply the verdict rule mechanically. Accept only if every required
   check passes. Reject if any required check fails or is unclear.
   Preferred results never change the verdict.
3. In the readable summary, list every check and its evidence. For a
   rejection, identify the first failing or unclear required check in
   rubric order as the primary blocker, then list the remaining blockers.
   For an acceptance, lead with the most decisive plan-fidelity and
   fix-specific test facts.
4. In live mode, add voice-guide notes after the check summary without
   changing the verdict unless the same evidence failed a rubric check.
5. Emit the required JSON with the item identifier, all checks in rubric
   order, their grades and evidence, and the binary verdict. Put nothing
   after the fenced JSON block.
