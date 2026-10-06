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

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->
* **Where it lives:**
  * **Eval mode:** Under `## Candidate plan` in the `Diagnosis:` block, referencing details from `## Issue`, `## Thread highlights`, or `## Repro evidence`.
  * **Live mode:** In the `## Diagnosis` section of workspace `plan.md`, referencing the posted reproduction comment on the GitHub issue thread.
* **What good looks like:**
  * The stated cause directly cites behavior and stack traces or terminal output demonstrated in the reproduction evidence.
  * The explanation identifies specific functions, modules, parameters, or state transitions responsible for the defect rather than making generic claims.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->
* **Where it lives:**
  * **Eval mode:** Under `## Candidate plan` in the `Scope:` block of the practice package.
  * **Live mode:** In the `## Scope` section of workspace `plan.md`.
* **What good evidence looks like:**
  * Explicitly distinguishes between what is in-scope to change and what is out-of-scope (such as refactoring, unrelated bugs, or additional features).
  * Defines boundaries that remain strictly within the issue description without refactoring unrelated components.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->
* **Where it lives:**
  * **Eval mode:** Under `## Candidate plan` in the `Approach:` block and explicit paths listed in `Scope:`, `Approach:`, or `Files:` blocks of the practice package.
  * **Live mode:** In the `## Files` (or `Files to Touch`) and `## Approach` sections of workspace `plan.md`.
* **What good looks like:**
  * **Files:** Lists exact, concrete repository file paths targeted for creation, modification, or deletion (e.g., `src/adapter/dispatch.py`), describing the specific logic change occurring within each path.
  * **Approach:** Details step-by-step logic, API changes, structural design, or unit tests to implement, allowing an engineer to start executing without asking the author clarifying questions.
  * Aligns with maintainer recommendations or constraints noted in thread highlights or repository guidelines.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->
* **Where it lives:**
  * **Eval mode:** Under `## Candidate plan` in the `Test plan:` block of the practice package.
  * **Live mode:** In the `## Test Plan` section of workspace `plan.md`.
* **What good looks like:**
  * Specifies exact commands, test scripts, or reproduction re-runs used to verify the fix.
  * Explicitly states expected terminal output or post-fix assertions without relying on manual UI adjustments or unstated steps.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->
* **Where it lives:**
  * **Eval mode:** Under `## Candidate plan` in the `Risk:`, `Risks and Unknowns:`, or `Deviations:` block of the practice package.
  * **Live mode:** In the `## Risks and Unknowns` and `## Deviations` sections of workspace `plan.md`.
* **What good looks like:**
  * Explicitly identifies potential edge cases, breaking changes, shared dependencies, or uncertain implementation locations rather than projecting false confidence.
  * Outlines concrete verification steps or fallback actions for each identified risk or unknown.
  * Honestly records any mid-build deviations from the original plan with justification for what changed and why.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->
* **Where it lives:**
  * **Eval mode:** In the `## Candidate plan comment` section of the practice package, evaluated against `## Issue`, `## Thread highlights`, and `## Repo facts` (including contribution guidelines and AI policies).
  * **Live mode:** In workspace `comment.md`, evaluated against the live GitHub issue thread, repository contribution guide (`CONTRIBUTING.md`), and workspace `voice-guide.md`.
* **What good looks like:**
  * Accurately summarizes the diagnosis, scope, approach, and test plan from `plan.md` without introducing contradictory claims.
  * Demonstrates thread awareness by directly aligning with maintainer observations and comments in the thread highlights rather than posting boilerplate summaries.
  * Strictly adheres to repository contribution rules in `## Repo facts`, including required issue template fields, contribution policies, and explicit AI-use disclosures where mandated.
  * Free of generic fluff, self-deprecating apologies, or unverified timeline commitments.
