# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**Where it lives.** In an eval package, use the candidate plan's cause or diagnosis and compare it with the Repro evidence block's steps, actual and expected results, errors, artifacts, and controls. The Issue section supplies the requested behavior, and Thread highlights may narrow the cause. In live mode, use the diagnosis quoted in `plan.md` and the draft comment, the student's posted reproduction comment on the issue, and relevant maintainer replies.

**What good looks like.** The diagnosis explains the behavior the reproduction actually shows and stays within what its controls establish. A confident theory fails when a control rules it out, when the failure occurs before or after the named component, or when it depends on facts absent from the evidence.

## Scope

**Where it lives.** In an eval package, compare the Issue's requested outcome with the candidate plan's change, in-scope and out-of-scope statements, files, code areas, and optional follow-up work. In live mode, compare the same parts of `plan.md` with the issue body and maintainer comments.

**What good looks like.** The plan delivers one outcome needed for the issue and names intentional exclusions. Supporting tests and the smallest necessary adjacent edit belong in scope; unrelated cleanup, new features, broad migrations, architectural rewrites, and "while here" work do not.

## Executability

**Where it lives.** Use the candidate plan's named files, functions or code areas, approach, and sequence of changes. Thread highlights can supply a maintainer-selected implementation direction. In live mode, verify named locations against the repository when needed, but grade what the draft communicates rather than silently filling its gaps from local code.

**What good looks like.** Another contributor can identify where to start, what behavior to change, and the intended result. A small stated unknown may remain when the plan gives a concrete way to resolve it; plans that say only investigate, optimize, fix it somewhere, or choose an approach later are not executable.

## Test plan

**Where it lives.** Compare the candidate plan's test steps with the Repro evidence block's triggering command or actions, inputs, artifacts, controls, and observed failure. In live mode, use the test section of `plan.md` and the student's posted reproduction evidence.

**What good looks like.** The plan reruns the failing case through the real code, states the observable post-fix result, and checks a related working path for regression. "Run the tests," "it should work," or a subjective result such as "feels faster" is insufficient without a fix-specific outcome.

## Honesty

**Where it lives.** Read the candidate plan's risks, unknowns, assumptions, qualifications, and Deviations section against the reproduction limits and thread evidence. In live mode after implementation, compare Deviations with the actual build diff and test result; before implementation, an explicitly pending Deviations section is not itself a failure.

**What good looks like.** Claims are no stronger than the available evidence, meaningful unknowns are named with a way to check them, and optional work is not presented as required. After the build, the plan says either what changed and why or, in the author's own words, that the implementation followed the plan.

## Comms

**Where it lives.** In an eval package, compare the Candidate plan comment with the Issue, Thread highlights, Repo facts, bug-report template asks, contribution policy, and any AI-use disclosure requirement. In live mode, compare the draft comment with the current issue thread, repository contribution guide and templates, and the student's `voice-guide.md`; use `scope.md` for Path Review house rules.

**What good looks like.** The comment is the contributor's own issue-specific plan, acknowledges relevant maintainer direction or competing work, briefly connects the diagnosis to the reproduction, and states a bounded change and decisive test. It includes any required AI disclosure and never substitutes "same as above" or generic enthusiasm for a plan.
