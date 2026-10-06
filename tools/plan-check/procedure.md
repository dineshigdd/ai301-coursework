# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->
1. In live mode, read `scope.md` and confirm the candidate issue URL matches the designated repository on the Repo: line; note any repository house rules. In eval mode, ignore `scope.md` entirely, as the practice package bundle contains all necessary context.
2. Read `rubric.md` and `references/evidence-guide.md` (both modes) to identify all rubric checks and the verdict rule.
3. Read the whole package before grading anything: the issue thread and repository context first, then reproduction logs/findings, then `plan.md` (or `Candidate plan` block), then `comment.md` (or `Candidate plan comment` block).
4. Maintain this exact reading sequence (Issue -> Repro -> `plan.md` -> `comment.md`) so proposed plans are evaluated against true problem context rather than in isolation.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->
How to gather the evidence:
- Identify execution mode first:
  - In `eval mode` (eval harness running on practice packages in `eval/packages/`): Extract evidence directly from the static package files (e.g., `plan.md`, `comment.md`, or `Candidate plan` or `Candidate comment` blocks in the bundle).
  - In `live mode` (checking workspace drafts against GitHub issue context): Read `plan.md` and `comment.md` in the current workspace for candidate evidence, and gather issue context/thread standards from the locations defined in `references/evidence-guide.md`.
- Gather specific evidence for each rubric check:
  - For `diagnosis`, locate the `Diagnosis` section in `plan.md` and record the root-cause explanation along with any directly quoted reproduction error messages or logs.
  - For `scope`, locate the `Scope` section in plan.md and record both what is explicitly marked as `in scope` to change and what is explicitly defined as `not in scope`.
  - For files, locate the Files to Touch section (or Files, File) in `plan.md` and record all specific repository file paths targeted for creation, modification, or deletion.
  - For approach, locate the Approach section in `plan.md` and record the step-by-step logic, implementation design, or architecture changes described.
  - For `test-plan`, locate the `Test Plan` section in `plan.md` and record the concrete test commands, scripts, and expected post-fix output/behavior.
  - For `risks`, locate the `Risks and Unknowns section` in `plan.md` and record any listed edge cases, potential regressions, side effects, or dependencies.
  - For `comment`, inspect `comment.md` (or the `Candidate plan comment` block) and record whether it accurately summarizes diagnosis, scope, approach, and test plan while adhering to thread conventions described in `references/evidence-guide.md`.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
How to grade each check:
- Execute checks in sequential order as listed in the rubric table in `rubric.md`: diagnosis, scope, files, approach, test-plan, risks, and comment.
- Evaluate the gathered evidence for each check strictly against its corresponding Pass Condition in rubric.md.
- Grade each check as pass, fail, or unclear, accompanied by a one-line evidence quote or fact supporting the decision.
- Assign pass if the gathered evidence satisfies all requirements of the pass condition.
- Assign fail if evidence is present in the plan or comment draft but explicitly contradicts or fails to meet the pass condition.
- Assign unclear if the required section or evidence is genuinely absent from the package or lacks critical details needed to evaluate the check.
- Once evidence is gathered during step 2, evaluate each check directly against the rubric criteria without re-reading the full package.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
How to reach the verdict:
- Apply the verdict rule defined in `rubric.md` to aggregate individual check grades into the final verdict.
- Output either `accept` (ready to post) or `reject` (hold) as the final verdict. No other verdict values are permitted.
- Treat any check graded as unclear as a failed check when applying the verdict rule.
- Select and quote the specific line of evidence or key fact from the package that decided the pass, fail, or unclear result for each check.
- In `live mode`, verify the draft comment against `voice-guide.md` and log any rule violations in the feedback summary.
- Before the JSON block, you may show a short readable summary with one line per check, plus any voice-guide notes in live mode.
- Output the machine-readable result as a single fenced JSON block (as shown below) at the very end. The eval harness parses the last fenced JSON block in your output, so it must be present, valid, and the final content generated:

```json
{
  "item": "<issue URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```