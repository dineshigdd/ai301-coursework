# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | `Environment.` section | Contains explicit values for key runtime parameters: OS/platform, main runtime/binary name, and tool version string. | required |
| steps-to-complete | `Preparation.` and/or `Execution.` section | Provides followable setup and execution commands (such as CLI commands or scripts). Standard workspace setups or common CLI flags are acceptable; only fail if essential steps or core commands are missing entirely. | required |
| target-alignment | `Execution.` and `Actual.` sections read against Issue description and metadata | The commands run, parameters used, AND the exact error or behavior reported in `Actual.` directly correspond to the bug described in the issue description rather than an unrelated bug, command, or feature. | required |
| actual-output | `Actual.` section (or `Execution.`) | Contains raw, un-summarized terminal output, stack traces, or log excerpts showing the observed failure or result. | required |
| expected-output | `Expected.` section | Explicitly states the expected non-error outcome or intended behavior to contrast with `Actual.`. | required |
| analysis | `Analysis.` section (or summary notes in `Execution.` / `Actual.`) | Contains a non-empty statement declaring the reproduction verdict (e.g., "reproduced", "cannot reproduce") or identifying the root cause. | required |
| disclosure-policy | Claim comment or report footer | Includes required repository disclosures (such as AI/tool assistance statements) and complies with repo contribution guidelines. | required |

## Verdict rule

Accept the candidate issue if and only if every check with weight `required` passes (`P`); otherwise, if any `required` check fails (`F`) or lacks sufficient evidence (`?`), reject the candidate issue, while checks with weight `preferred` are used solely for ranking accepted issues and never alter the accept or reject verdict.

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept the candidate issue if and only if every check with weight `required` passes (`P`); otherwise, if any `required` check fails (`F`) or lacks sufficient evidence (`?`), reject the candidate issue, while checks with weight `preferred` are used solely for ranking accepted issues and never alter the accept or reject verdict.