---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

Decide whether one candidate pull request is ready to submit. A PR
package includes the title, description, commits, diff, and test evidence,
read against the accepted plan, its deviation notes, the issue and thread,
and the repository's contribution requirements. Grade only that question
for one package per run.

## Inputs and modes

Choose the mode from the supplied input.

- In **live mode**, read the issue URL and its current thread, `plan.md`
  including `## Deviations`, `test_evidence.md`, and `pr_draft.md`. From
  the repository's top-level working copy, read every committed branch
  change with `git diff main...HEAD`. Also read
  `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`. If the
  student is using the house chain, use its issue, repro pack, plan, and
  branch in the same roles. Do not silently substitute uncommitted work
  for the committed diff.
- In **eval mode**, treat the provided package bundle as the whole world.
  Fetch nothing and read no outside files or live pages. Run every rubric
  check and apply the complete verdict rule to the frozen package.

## The scope seam (live mode only)

In live mode, read `scope.md` before gathering any evidence. Apply its
repository boundary and house rules. Refuse to grade a PR aimed outside
the named repository. If the `Repo:` line still contains its bracketed
placeholder, stop without grading and tell the student to replace it with
the section's Path Review repository. Never guess the repository. Ignore
`scope.md` entirely in eval mode.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` before reviewing the outgoing PR
title and description. Report each broken voice rule in the readable
summary and quote the rule that was broken. A voice-guide concern does
not change the verdict unless a rubric check independently covers the
same problem. Ignore `voice-guide.md` entirely in eval mode.

## Component reads

Read `rubric.md` for the checks, weights, pass conditions, and verdict
rule. Use `references/evidence-guide.md` to locate each evidence family,
then execute `procedure.md` exactly as written. If the procedure is
silent about a needed step, report the gap instead of inventing a method.
If `rubric.md` contains no completed checks or `procedure.md` contains no
completed steps, refuse to grade and explain which required component is
empty.

## Verdict and output

Use only two verdicts: `accept` means the PR is ready to submit, and
`reject` means hold it. A short per-check summary may come first. End
with the valid fenced JSON block below, and put nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Name the specific fact or quote that decides every check. Never use
  "looks fine" as evidence.
- Grade the actual plan, diff, evidence, and repository requirements,
  not the length, confidence, or polish of the write-up.
- Apply each rubric pass condition as written even when intuition points
  elsewhere. A concern that the rubric does not capture belongs in the
  summary and in a later rubric revision, not in an improvised grade.
- Follow the procedure as written. Report procedural gaps instead of
  filling them with a new workflow during the run.
- Apply the rubric's explicit treatment of `unclear`. If it is silent,
  count `unclear` as a failure because unverifiable readiness is not
  readiness.
