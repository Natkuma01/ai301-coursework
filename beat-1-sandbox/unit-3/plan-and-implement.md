# Unit 3 Plan and Build

## Posted upstream

**GitHub username**

Natkuma01

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69#issuecomment-6051167852

I reproduced the top-level JSON array failure on issue #69. The array is decoded successfully, but `_parse_json_output()` receives a Python list and calls `.items()`, which causes the reported `AttributeError`.

I plan to keep the change focused on `rag/generator/output_parser.py` and `tests/unit/test_output_parser.py`: send only dictionary-shaped JSON to `_parse_json_output()` so arrays use the existing plain-text fallback, preserve the current JSON-object behavior, remove the existing `xfail` marker, and add coverage for an array inside a JSON code fence. I will rerun the reproduced array test and the full output-parser test file, checking that raw and fenced arrays no longer crash and that the existing object and plain-text paths still pass.

## Your branch

**Branch**

`fix/69-json-array-fallback`

**Evidence**

Before the change:

```text
$ .venv/bin/python -m pytest tests/unit/test_output_parser.py -k test_json_array_fallback --runxfail -v
collected 19 items / 18 deselected / 1 selected

tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback FAILED

data = ['First feedback item', 'Second feedback item']
for key, value in data.items():
AttributeError: 'list' object has no attribute 'items'

FAILED tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback
1 failed, 18 deselected in 0.18s
```

After the change, the same focused case through the real parser passes:

```text
$ .venv/bin/python -m pytest tests/unit/test_output_parser.py -k test_json_array_fallback -v
collected 20 items / 18 deselected / 2 selected

tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback_in_fence PASSED

2 passed, 18 deselected in 0.11s
```

The full parser test file also passes and confirms the object and plain-text paths still work:

```text
$ .venv/bin/python -m pytest tests/unit/test_output_parser.py -v -rx
collected 20 items
...
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED
...
20 passed in 0.22s
```

Static checks:

```text
$ .venv/bin/ruff check rag/generator/output_parser.py tests/unit/test_output_parser.py
All checks passed!

$ .venv/bin/mypy rag/generator/output_parser.py
Success: no issues found in 1 source file
```

## Eval iterations

**Run history**

- Calibration attempt: no score. All four calibration items returned `ERROR` because the Claude CLI was not logged in.
- Final full run: 20/20 agreement. Every category met its floor, and this score matches the agreement line in `eval-run.txt`.

**Package analysis**

I analyzed `pkg-02`. My rubric returned `accept`, matching the gold label. The reproduction isolates unsigned subtraction in the two line-range adjustment sites, and the plan applies saturating subtraction at those named sites. It explicitly excludes a larger parser redesign, gives another contributor a concrete starting point, and reruns the reproduced case with an observable expected exit status of 0. Those facts satisfy the diagnosis, cause alignment, bounded scope, executability, and decisive-test checks; the comment also stays specific to the issue and repository context.

**Check rationale**

From `tools/plan-check/rubric.md`:

> `test_plan_proves_result` | Compare the proposed test steps and expected results with the reproduction evidence. Use the Test plan section of `references/evidence-guide.md`. | Pass when the test plan repeats the reproduced case, defines the expected behavior after the fix, and checks that related existing behavior still works. Fail when it only says to run tests or does not identify an observable result. | required

I wrote the check this way because a broad test-suite command can be green without exercising the reported failure. Requiring the reproduced case, a post-fix observable, and a related regression check makes the plan prove both that the bug changed and that an existing path was not broken.

**Trade-offs**

This test check rejects otherwise thoughtful plans that have not yet chosen a fix-specific assertion, including a plan that only promises to run the full suite. That is stricter than accepting a plan whose implementation details are still exploratory. I accept that trade-off because the plan is supposed to be ready to build from: without an observable result, another contributor cannot tell whether the proposed change solved the reproduced problem. `calib-04` is the canary for this boundary; its bounded approach still rejects because its test plan names only the full suite.
