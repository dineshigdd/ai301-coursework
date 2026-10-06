# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

dineshigdd

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60#issuecomment-5989322499  
I reproduced the `TypeError` on Ubuntu 24.04 following the issue report. 

**Diagnosis:**
The root cause occurs in `FaithfulnessChecker.check()` where `chunk.get("text", "")` is used to extract text. When a context chunk explicitly contains `{"text": None}`, `dict.get()` finds the existing `"text"` key and returns `None` instead of the default `""`. Passing `None` into `" ".join(...)` causes the `TypeError`.

**Scope:**
- **In Scope:** Modifying `FaithfulnessChecker.check()` in `rag/evaluator/faithfulness_checker.py` to sanitize `None` text values, and removing the corresponding test marker in `tests/unit/test_faithfulness_checker.py`.
- **Out of Scope:** Refactoring surrounding RAG evaluation logic, prompt templates, or creating new test modules.

**Proposed Approach:**  
I will update `FaithfulnessChecker.check()` to safely handle `None` values using `chunk.get("text") or ""` before string join execution. Additionally, per `docs/CONTRIBUTING.md` guidelines for seeded bug fixes, I will remove the `@pytest.mark.xfail(strict=True)` marker from `test_none_context_chunk_text` in `tests/unit/test_faithfulness_checker.py` so the test suite reports a clean `PASSED` status with exit code 0.

---

## Your branch

**Branch**  
fix/60-faithfullchecker-crash
[The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.]

**Evidence** 

#### Before Fix (Unit 2 Reproduction)
Command:
```bash
python -c "from rag.evaluator.faithfulness_checker import FaithfulnessChecker; FaithfulnessChecker().check('Knows Python.', [{'text': None}])"
```

Output:
```bash
TypeError: sequence item 0: expected str instance, NoneType found
```
#### After Fix (Unit 3 Verification)
Command:
```bash
python -c "from rag.evaluator.faithfulness_checker import FaithfulnessChecker; print(FaithfulnessChecker().check('Knows Python.', [{'text': None}]))"
```
Output:
```bash
0.0
```
Command:
```bash
pytest tests/unit/test_faithfulness_checker.py
```

Output:
```bash
19 passed, 3 xfailed in 11.72s
```

## Eval iterations  

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**  
Run 1: 18/20 (90%)

**Package analysis**  

Package: pkg-13
* Rubric Decision: REJECT (failed: files)
* Gold Label: ACCEPT (clear-accept)

**Check rationale**  

| files | `Files to Touch` section in `plan.md` | Identifies specific repository file paths to be created, modified, or deleted. | required |

Rationale: I did not revise this check during evaluation runs because my rubric achieved a passing agreement score (18/20) on the first run. When designing this check, I rejected a lenient condition that would accept conceptual module descriptions (e.g., naming `AdaptDispatch::EraseInDisplay` without a specific file path, as seen in `pkg-13`, which omitted a dedicated `Files to Touch` section entirely). I rejected that looser condition in favor of requiring explicit repository file paths to ensure implementation plans are immediately actionable without ambiguity.

**Trade-offs**  
In pkg-13, requiring an explicit `Files to Touch` section with concrete repository file paths caused a strict rejection because the candidate plan described the fix locations conceptually (e.g., `AdaptDispatch::EraseInDisplay`) without naming exact file paths. While this strictness caused a single mismatch against the gold label's clear-accept verdict on pkg-13, it prevents under-specified or incomplete plans from passing evaluation in live engineering environments.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
