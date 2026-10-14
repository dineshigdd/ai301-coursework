---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->
You are grading one candidate pull request package to answer a single question: **is this ready to submit?** A PR package consists of the candidate pull request (title, description, commits, diff, and test evidence), read against the accepted plan it claims to implement, the issue it addresses, and the target repository's standards. You do not answer from gut feel: you answer by executing the student-authored grading procedure in `procedure.md`, which applies the rubric in `rubric.md` to evidence gathered per `references/evidence-guide.md`.

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->
## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->
The pr-precheck tool answers exactly one question about exactly one PR package: **is this ready to submit?** . A PR package is a candidate pull request (title, description, commits, diff, test evidence), read against the plan it claims to implement and the issue that plan belongs to. The tool never answers a different question, never grades more than one package per run, and never answers from gut feel: it executes the components in this directory.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

One of:
- **Live mode**: the student's own `plan.md` (including any `## Deviations`), the diff on their branch, their draft PR title and description (from `pr_draft.md`), and their test evidence (`test_evidence.md`), read against their chosen issue. The branch's diff is everything the branch changes relative to the default branch, produced concretely from `git diff main...HEAD` (three dots) run in the working copy. A house-chain student reads the house plan and house repro pack instead; the same checks grade the same things there. Live mode gathers issue-side evidence from the real repository (the thread, the PR template, and stated policy documents like `docs/CONTRIBUTING.md`).

- **Eval mode**: a package bundle (a Markdown file in `eval/packages/` containing the issue context, repo facts, accepted plan, candidate PR title, description, commits, diff, and test evidence). The bundle text is the whole world: nothing is fetched from GitHub or read from the local working tree. Eval mode always grades a complete package using every check and the full verdict rule.


## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->
In live mode, read `scope.md` in this skill directory before anything else. It names where the student's PR must live and the house rules that apply in that environment (a house rule changes how evidence is read). Refuse to grade a PR package outside the scoped repository. If the scope's `Repo:` line still carries an unfilled placeholder, stop without grading and tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->
In live mode, also read `voice-guide.md` in this skill directory: the student's own rules for how they write upstream, with wrong/right examples. Check the draft PR title and description (from `pr_draft.md`) against those rules and report any rule the draft breaks in the summary, quoting the rule. The voice guide never changes the verdict on its own unless the rubric has a check that reads it. In eval mode, ignore `voice-guide.md` entirely: voice is personal and carries no gold labels; universal communication-quality checks live in the rubric.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

How the components in this directory connect and govern execution:
- `rubric.md` (The Brain): Defines the table of checks and the verdict rule. It references `references/evidence-guide.md` to map where each evidence family lives.
- `procedure.md` (The Hands): Executed strictly as written. If the procedure is silent on a step, report the gap in the summary—never improvise or invent steps around it.
- `references/evidence-guide.md` (The Map): Defines the structural map of evidence locations across live mode files and eval package bundles, setting the standard for what good evidence looks like.
- The Refusal Rule: If `rubric.md` has no checks filled in, or `procedure.md` has no operating steps filled in (or if they contain only template instruction comments), stop immediately and refuse to grade. An empty or template tool that invents checks at runtime is prohibited by design.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->
- Evidence first: No check is graded without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: A terse complete PR can be ready and a beautiful confident one can be hiding drift. Every check reads the artifact itself against the plan, the issue, and the stated standards, never the formatting.
- The rubric decides, not the run: If a check passes by its stated condition but feels wrong, it still passes; the fix belongs in the rubric, not in the run.
- The procedure decides how, not the run: Follow `procedure.md` as written and report its gaps in the summary instead of silently inventing steps.
- Unclear defaults to fail: Treat `unclear` as the rubric's verdict rule directs; where the rule is silent, an unverifiable claim is a failing one. A PR you cannot verify from the package is a PR that is not ready to submit.