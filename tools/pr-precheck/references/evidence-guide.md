# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Where it lives.** In an eval bundle, compare the Plan context's scope,
boundaries, promised outcome, test plan, and deviation notes with the
Candidate PR's complete diff and description. In live mode, compare
`plan.md`, including `## Deviations`, with `git diff main...HEAD` and the
title and description in `pr_draft.md`.

**What good looks like.** Every substantive diff hunk belongs to the
plan or a deviation that names what changed and why. Every promised
outcome appears in the diff or is honestly deferred in both the plan and
description. Silent drift includes extra features, cleanup, or refactors
with no deviation, missing planned work, and descriptions that claim
more or less than the diff actually delivers.

## Test evidence (harness category: not-tested)

**Where it lives.** In an eval bundle, use the Plan context's test plan
and reproduction, the Candidate PR's Test evidence, and the repo-facts
block's required checks. In live mode, compare the Unit 2 reproduction
and the test plan in `plan.md` with `test_evidence.md`; use the PR template
and `docs/CONTRIBUTING.md` for required repository checks.

**What good looks like.** The evidence runs the behavior that was broken,
shows an observable before and after or a decisive failing-to-passing
test, and covers each failure mode the plan says this PR proves. It also
shows the actual result of every repository-required check. "Tests pass,"
time spent using the app, or a control path that never exercised the bug
does not establish the fix. An honestly reported failing check is still
evidence; hiding or omitting it is not.

## Diff quality (harness category: unreviewable)

**Where it lives.** In an eval bundle, inspect the entire Candidate PR
diff and commit list. In live mode, inspect all of `git diff main...HEAD`
and the branch's commits, not only the files named in the description.

**What good looks like.** The intended change is easy to isolate and
contains no temporary logging, commented-out attempts, dead helpers,
TODO debris, unrelated files, repeated lines, or unnecessary formatting
and import churn. A necessary adjacent or mechanical edit can pass when
its role is clear and it does not bury the fix. A correct, well-tested fix
still fails this family when submission debris makes the diff unsafe or
needlessly hard to review.

## Standards and comms (harness category: standards-wall)

**Where it lives.** In an eval bundle, read the Repo facts and Thread
highlights for PR-template sections, checklists, required issue syntax,
tests, changelog or documentation rules, maintainer direction, and AI-use
policy. Compare those asks with the Candidate PR description and diff. In
live mode, read the live issue thread, `.github/PULL_REQUEST_TEMPLATE.md`,
`docs/CONTRIBUTING.md`, and the title and description in `pr_draft.md`.

**What good looks like.** Every applicable template and policy ask has
specific content or a truthful N/A explanation, and any required file is
actually present in the diff. Relevant maintainer direction is addressed.
When AI disclosure is required, the description includes it in the form
the repository asks for; when no policy requires disclosure, do not invent
one. Boilerplate, unchecked required items, and confident claims that a
missing required artifact exists do not satisfy the standard.
