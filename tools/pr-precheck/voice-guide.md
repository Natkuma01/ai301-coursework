# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2 and carried it through week 3; paste your filled voice-guide.md
here, whole. It is not re-authored and it is not graded as new work
this week.

Then reread it with the PR in mind. Your comments promised, reported,
and committed to an approach; a PR title and description ask a
maintainer to spend review time on your work. If your rules do not
cover that register (for example: how a title earns its thirty
seconds, how a description promises exactly what the diff contains,
how a disclosed shortfall is worded so it reads as honesty rather
than apology), extend the guide with what it needs. Extending is
allowed and encouraged; starting over is not required.

Live mode reads this file and holds your draft PR title and
description against it, reporting any rule your draft breaks. Eval
mode ignores it entirely, because your voice is yours and carries no
gold labels.
-->

## Who I am in threads

I am a new computer science graduate building more experience contributing
to open-source projects. I write in plain, conversational English and keep
the tone friendly while being precise about what changed, what I tested,
and what I still do not know.

## Rules I write by

### Rule: Say only what I verified

Separate results I observed from information I learned in the issue or
from someone else's comment. Never claim that a test passed or a behavior
changed without checking it.

- Wrong: "Everything is fixed and all cases pass."
- Right: "I reran the array-input case and the existing object-input test;
  both passed on this branch."

### Rule: Match the description to the actual diff

Describe every meaningful change plainly, and do not claim a planned item
landed unless it is present. Mention any intentional departure or deferral
instead of hiding it.

- Wrong: "This implements the whole plan exactly."
- Right: "The parser fix and regression test are included. I deferred the
  documentation update because the behavior is already documented in the
  existing error reference."

### Rule: Be specific about testing

Name the command, input, or user flow and its result. A broad statement
such as "tested locally" is not useful to a reviewer.

- Wrong: "Tests pass on my machine."
- Right: "`make test-unit` passed, and the reproduced array input now
  returns a validation error instead of raising `AttributeError`."

### Rule: Explain failures honestly

Report a failed or unavailable check with its actual result and context.
Do not turn missing evidence into a success claim.

- Wrong: "All checks are good."
- Right: "`make test-integration` reported `no tests ran`, which is the
  expected result for this repository right now."

### Rule: Sound like myself, not a formal report

Use simple sentences and familiar words. Keep the PR easy to scan, but do
not remove details a reviewer needs.

- Wrong: "Pursuant to the aforementioned implementation, the defect has
  been remediated."
- Right: "This change handles the list input before the parser reads
  object-only fields."

### Rule: Give reviewers a useful AI-use disclosure

State in my own words how AI helped and what I personally checked. Do not
paste a generic disclosure or imply that AI output was accepted without
review.

- Wrong: "AI was used."
- Right: "I used AI to help compare the implementation with my plan and
  organize the test notes. I reviewed the diff and ran the listed commands
  myself."

## Things I never post

- A claim that I ran a check I did not run.
- A statement that the diff matches the plan when I have not compared them.
- A hidden failed check or unexplained missing test.
- "Same as above" instead of a complete issue-specific explanation.
- Unrelated cleanup presented as part of the fix.
- A generic AI disclosure with no explanation of how I used it.
- Overly formal language when plain English is clearer.
