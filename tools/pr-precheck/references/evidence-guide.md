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

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->
- **Where it lives:** 
  - **eval mode:** Under the `## Plan context` block (the accepted plan's scope boundary and test plan) compared side-by-side against the `## Candidate PR` block (specifically `## Diff`, `## Commits`, and `## Description`).
  - **live mode:** Compared between your accepted plan in `plan.md` (including any documented `## Deviations` notes) and your active branch diff (`git diff main...HEAD`) and `pr_draft.md`.
- **What good looks like:** Every changed file and hunk falls strictly inside the plan's stated scope or a documented deviation note, and the diff faithfully implements the planned changes without silent drift (does not silently do more or less than posted).

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->
- **Where it lives:** 
  - **eval mode:** Under the `## Test evidence` block (containing repro command re-runs, before/after transcripts, expected-after validation, and test suite outcomes).
  - **live mode:** In your `test_evidence.md` file (recording your re-run transcripts, expected-after behavior per the plan, and the execution results of the repo's own checks like unit tests and lints).
- **What good looks like:** Complete, observable transcripts showing clear proof of behavior (e.g., reproducing the failure before and showing success/exit-code changes after), alongside explicit validation against the plan's test criteria and visible test suite outcomes. Vague assertions or missing proof fail this check.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->
- **Where it lives:** 
  - **eval mode:** Under the `## Diff` code block and `## Commits` list.
  - **live mode:** Your active branch diff (`git diff main...HEAD` and `git diff main...HEAD --stat`) and commit history.
- **What good looks like:** A clean, focused unified diff containing only the necessary changes and tests required for the fix. It is entirely free of review-blocking debris such as stray debug print statements, commented-out dead code, temporary test files, or unrelated cleanup/formatting hunks that bury the core change.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->
- **Where it lives:** 
  - **In eval bundles:** Under the `## Repo facts` block (stating PR template rules and contribution policies) and the candidate PR's `## Title` and `## Description`.
  - **In live mode:** Your `pr_draft.md` file (incorporating `.github/PULL_REQUEST_TEMPLATE.md` from your Path Review repo, required GitHub issue linking keywords like `closes #`, and AI-use disclosures in the review notes).
- **What good looks like:** A fully populated PR template where every section contains real content, the correct issue-closing keyword and number are present, maintainer requests or thread guidance are addressed, and AI-use disclosure is explicitly declared in the review notes. Boilerplate text or a visibly ignored contribution ask fails this check.
