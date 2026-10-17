# Plan for issue 69 JSON array fallback

## Diagnosis

The raw JSON path in `parse_review_output()` successfully decodes a top-level array, then passes the resulting Python list to `_parse_json_output()`. That helper assumes every decoded value is a dictionary and immediately iterates with `data.items()`.

The reproduction pins down the failure at that boundary:

> `data = ['First feedback item', 'Second feedback item']`
>
> `for key, value in data.items():`
>
> `AttributeError: 'list' object has no attribute 'items'`

This shows that JSON decoding is working and the crash occurs because `_parse_json_output()` does not handle the decoded list shape.

## Scope

In scope:

- Update both JSON-decoding paths in `rag/generator/output_parser.py` so only dictionary-shaped JSON is sent to `_parse_json_output()` and a top-level array reaches the existing plain-text fallback.
- Strengthen and enable the existing raw-array regression test in `tests/unit/test_output_parser.py`, and cover a fenced array because it reaches a separate decode site.
- Run the focused reproduction and the complete output-parser unit test file.

Out of scope:

- Changing the `FeedbackSection` data model.
- Changing plain-text fallback behavior or JSON code-fence detection.
- Refactoring other seeded parser defects or unrelated generator code.
- Adding a new schema for model output.

## Files

- `rag/generator/output_parser.py`: handle a decoded list before the existing dictionary iteration.
- `tests/unit/test_output_parser.py`: remove the issue #69 `xfail` marker and assert the two array items are retained in order.

## Approach

1. At both `json.loads()` call sites, call `_parse_json_output()` only when the decoded value is a dictionary. Let arrays and other valid non-object JSON continue to the existing `_parse_plaintext_output(raw)` return.
2. Leave `_parse_json_output()` and the existing dictionary behavior unchanged so structured JSON callers keep their section names, confidence values, and suggestion extraction.
3. Remove the strict expected-failure marker from `test_json_array_fallback` and assert that a raw array returns one `general_feedback` section containing the unchanged raw input.
4. Add the same assertion for an array inside a `json` code fence, covering the other `json.loads()` call site.

## Test plan

Before the change, run the reproduced case directly through the real test with:

```bash
.venv/bin/python -m pytest tests/unit/test_output_parser.py -k test_json_array_fallback --runxfail -v
```

Expected before result: the test fails in `_parse_json_output()` with `AttributeError: 'list' object has no attribute 'items'`.

After the change:

1. Run the same focused test without `--runxfail`:

   ```bash
   .venv/bin/python -m pytest tests/unit/test_output_parser.py -k test_json_array_fallback -v
   ```

   Expected: it passes and returns one `general_feedback` section containing the unchanged array text instead of raising an exception.

2. Run the complete parser test file:

   ```bash
   .venv/bin/python -m pytest tests/unit/test_output_parser.py -v -rx
   ```

   Expected: all parser tests pass with no remaining expected failure for issue #69. The added fenced-array test covers the second decode path, and the existing JSON-object and plain-text tests verify those behaviors still work.

## Risks and unknowns

- The plain-text fallback preserves the raw JSON array as one section rather than exposing each element as a separate section. This loses structure, but it matches the issue's requested fallback behavior and avoids a misleading per-item design because the current generator consumes only the first returned section.
- The same guard also routes valid JSON scalars through the plain-text fallback. They would otherwise fail on `.items()` for the same reason, and treating every non-object JSON shape consistently keeps this fix bounded.
- The repository contains another intentionally seeded accumulator defect in the same module. It is unrelated to the reproduced array crash and will remain out of scope.

## Deviations

The implementation followed the planned behavior and test scope. I made one
small documentation-only adjustment: the `_parse_json_output()` docstring now
says "Parsed JSON object" instead of "Parsed JSON dict." I did not change the
helper's behavior; the wording matches the new guards that ensure it receives
only dictionary-shaped JSON.
