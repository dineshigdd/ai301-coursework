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

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->
1. In live mode, read `scope.md` and confirm the candidate issue URL matches the designated repository on the `Repo:` line; note any repository house rules. In eval mode, ignore `scope.md` entirely, as the practice package bundle contains all necessary context.
2. Read `rubric.md` and `references/evidence-guide.md` (both modes) to identify all rubric checks, weights, and the verdict rule.
3. In live mode, also read `voice-guide.md` to load the student's communication and formatting rules. In eval mode, ignore `voice-guide.md` entirely.
4. Read the whole package or candidate artifacts before grading anything: the issue thread and repository context first, then `plan.md` (including any deviations), the candidate PR draft (`pr_draft.md` or bundle metadata), the diff (`git diff main...HEAD` or package diff), and test evidence (`test_evidence.md` or bundle test section).
5. Maintain this exact reading sequence so proposed pull requests are evaluated against true problem context and posted plans rather than in isolation.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->
How to gather the evidence:
- Identify execution mode first:
  - In `eval mode` (eval harness running on practice packages in `eval/packages/`): Extract evidence directly from the static package files (e.g., plan context, candidate PR title/description, commits, diff, and test evidence blocks).
  - In `live mode` (checking workspace drafts against GitHub issue context): Read `plan.md`, `pr_draft.md`, `test_evidence.md`, and the branch diff (`git diff main...HEAD`), and gather issue context/thread standards from the locations defined in `references/evidence-guide.md`.
- Gather specific evidence for each rubric check:
  - For **Title**: Locate the PR title in `pr_draft.md` (or bundle title block) and record whether it is specific and clearly states what the PR does.
  - For **Description**: Locate the PR description and record details on functions used, references, tests, and required GitHub keywords (`close`, `fix`, or `resolve`) followed by the issue number.
  - For **Commits**: Locate the commit list and record the valid commit references.
  - For **Diff & Plan Fidelity (Silent Drift)**: Compare the code diff against `plan.md` to ensure the diff faithfully implements the plan without silent drift (does not silently do more or less than posted).
  - For **Test Evidence (Not Tested)**: Locate `test_evidence.md` (or bundle test evidence) and record repro re-run code blocks, expected-after validation, and observable behavior.
  - For **Diff Quality (Unreviewable)**: Inspect the diff hunks to ensure they are free of debug debris, commented-out code, or unrelated hunks that bury the change.
  - For **Standards & Comms (Standards Wall)**: Read the description and repository PR template/contribution guidelines to verify compliance with stated templates and disclosure requests.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
How to grade each check:
- Execute checks in sequential order as listed in the rubric table in `rubric.md`.
- Evaluate the gathered evidence for each check strictly against its corresponding Pass Condition in `rubric.md`.
- Grade each check as `pass`, `fail`, or `unclear`, accompanied by a one-line evidence quote or fact supporting the decision.
- Assign `pass` if the gathered evidence satisfies all requirements of the pass condition.
- Assign `fail` if evidence is present but explicitly contradicts or fails to meet the pass condition (including silent drift, un tested behavior, unreviewable diffs, or standards wall violations).
- Assign `unclear` if the required section or evidence is genuinely absent from the package or lacks critical details needed to evaluate the check.
- Treat `unclear` grades as failing conditions as dictated by the verdict rule.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->
How to reach the verdict:
- Apply the verdict rule defined in `rubric.md` to aggregate individual check grades into the final verdict.
- Output either `accept` (ready to submit) or `reject` (hold) as the final verdict. No other verdict values are permitted.
- Treat any check graded as `unclear` as a failed check when applying the verdict rule.
- Select and quote the specific line of evidence or key fact from the package that decided the pass, fail, or unclear result for each check.
- In `live mode`, verify the draft PR against `voice-guide.md` and log any rule violations in the feedback summary.
- Before the JSON block, show a short readable summary with one line per check, plus any voice-guide notes in live mode.
- Output the machine-readable result as a single fenced JSON block at the very end. The eval harness parses the last fenced JSON block in your output, so it must be present, valid, and the final content generated:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
