## Candidate plan

## Diagnosis
The `check()` method in the `FaithfulnessChecker` class uses `chunk.get("text", "")` to extract text from items in `context_chunks`. However, when a `chunk` explicitly contains `{"text": None}`, `dict.get()` evaluates the existing key and returns `None` rather than falling back to the default `""`. Passing `None` into `" ".join(...)` subsequently raises a `TypeError`.

## Scope
### In Scope
- **Targeted Component:** `FaithfulnessChecker.check()` in `rag/evaluator/faithfulness_checker.py`.
- **Logic Fix:** Safely handle context chunks where the `text` key exists but has a `None` value, ensuring string joining receives valid `str` types instead of `NoneType`.
- **Verification & Testing:** Execute the existing unit test suite in `tests/unit/test_faithfulness_checker.py` (specifically `test_none_context_chunk_text`) and re-run the reproduction snippet to verify the fix.

### Not in Scope
- **RAG Pipeline Redesign:** Any structural refactoring of surrounding evaluation or retrieval components.
- **Unrelated System Code:** Modifications to non-evaluator modules, prompt templates, or database schemas.
- **New Test Files:** Adding external or unrelated test suites outside of executing the provided failing unit test.

## Files to Touch
- `rag/evaluator/faithfulness_checker.py` (Modify): Fix `check()` to safely resolve `None` text values before calling `" ".join(...)`.
- `tests/unit/test_faithfulness_checker.py` (Modify): Remove the `@pytest.mark.xfail(strict=True, reason="issue #60: ...")` marker above `test_none_context_chunk_text` per `docs/CONTRIBUTING.md`.

## Approach

1. **Root-Cause Remediation in `rag/evaluator/faithfulness_checker.py`:**
   - Locate the context assembly loop inside `FaithfulnessChecker.check()`.
   - Update the chunk text extraction logic to safely handle `None` values returned when the `"text"` key exists with `None` as its value.
   - Sanitize the text values using `chunk.get("text") or ""` so that `NoneType` is safely converted to an empty string (`""`) prior to calling `" ".join(...)`.

2. **Remove `xfail` Marker in `tests/unit/test_faithfulness_checker.py`:**
   - Per `docs/CONTRIBUTING.md` guidelines for seeded bug issues, locate `test_none_context_chunk_text` in `tests/unit/test_faithfulness_checker.py`.
   - Delete the `@pytest.mark.xfail(strict=True, reason="issue #60: ...")` decorator directly above the test function so that `pytest` reports a clean `PASSED` status with exit code `0` once the bug is resolved.

## Test Plan
1. **Reproduction Check (Before Fix):**
   - Run the reproduction script:
     ```python
     from rag.evaluator.faithfulness_checker import FaithfulnessChecker
     FaithfulnessChecker().check('Knows Python.', [{'text': None}])
     ```
   - *Expected result before fix:* Raises `TypeError: sequence item 0: expected str instance, NoneType found`.

2. **Remove `xfail` Marker & Run Unit Tests (After Fix):**
   - Remove the `@pytest.mark.xfail(strict=True, reason="issue #60: ...")` marker from `test_none_context_chunk_text` in `tests/unit/test_faithfulness_checker.py` per `docs/CONTRIBUTING.md`.
   - Run the unit test suite:
     ```bash
     pytest tests/unit/test_faithfulness_checker.py
     ```
   - *Expected result post-fix:* `test_none_context_chunk_text` and all adjacent tests report a clean `PASSED` status with exit code `0` (avoiding an `XPASS(strict)` failure).

3. **Reproduction Re-verify (After Fix):**
   - Re-run the reproduction script:
     ```python
     from rag.evaluator.faithfulness_checker import FaithfulnessChecker
     FaithfulnessChecker().check('Knows Python.', [{'text': None}])
     ```
   - *Expected result post-fix:* Executes cleanly without raising `TypeError` and returns the expected evaluation outcome.

## Risks and Unknowns

- **Strict `xfail` Marker CI Failure:**
  - *Risk:* Per `docs/CONTRIBUTING.md`, the existing test `test_none_context_chunk_text` carries `@pytest.mark.xfail(strict=True)`. If the code fix is applied without removing this marker, `pytest` will report an `XPASS(strict)` result and treat it as a test suite failure.
  - *Mitigation:* Ensure that removing the `@pytest.mark.xfail(strict=True)` marker from `test_none_context_chunk_text` in `tests/unit/test_faithfulness_checker.py` is included as an explicit step in the build execution and verified during test execution.

- **Impact of Empty Context Strings on Evaluation Outputs:**
  - *Risk:* Converting `None` to `""` silences `TypeError` inside `FaithfulnessChecker.check()`, but passing empty context strings to the LLM evaluator might cause valid claims to be flagged as ungrounded during evaluation runs.
  - *Mitigation:* Run the full unit test suite (`pytest tests/unit/test_faithfulness_checker.py`) to confirm that adjacent tests pass and that empty context inputs produce expected fallback outputs without raising unhandled exceptions.

## Deviations
- Nothing changed during implementation.
