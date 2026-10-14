# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Title | `title` section of `pr_draft.md` | Specific and clearly states what the PR does. | Required |
| Description | `description` section of `pr_draft.md` | Clearly describes what the change does, why it was made, and includes an issue reference (e.g., fixes #...) where applicable. | Required |
| Commits | `commits` section of the practice package / candidate PR | Includes a clear list of valid commit references. | Required |
| Diff & Plan Fidelity (Silent Drift) | `diff` section compared against `plan.md` | The diff faithfully implements the plan without silent drift (does not silently do more or less than posted). | Required |
| Test Evidence (Not Tested) | `Test evidence` section of `test_evidence.md` or practice bundle | Includes repro re-run code blocks, `expected-after` validation, and clearly states observable behavior. | Required |
| Diff Quality (Unreviewable) | `diff` section | Free of debug debris, commented-out code, or unrelated hunks that bury the change. | Required |
| Standards & Comms (Standards Wall) | Description, PR template, and contribution rules | Follows the repo's stated template, disclosure requests, and AI-use notes. | Required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

`Accept` the package if every `required` check passes, `reject` it if any `required` check fails or if an unverified claim defaults to fail, and treat `preferred` checks and unclear grades accordingly.