# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| active_repository | Repository status, recent commits, releases, and issue activity | The repository is NOT archived, NOT marked read-only, and has demonstrated maintainer activity (commits, release, or issue responses) within the past 12 months. | required |
| policy_compliance | Repository contributing guidelines, issue policy, and labels | The repository contributing guidelines or issue text do NOT prohibit AI-generated code, documentation, or LLM-assisted contributions. | required |
| unassigned_issue | Assignees section, issue comments, and linked pull requests | The issue is currently open, displays "No one assigned" in the assignees sidebar, and has no active claim comments or open pull requests submitted by external contributors in the comment thread. | required |
| clear_requirements | Issue description body and title | The issue clearly states what needs to be fixed, updated, or implemented (e.g., specific bug report, documentation cleanup, performance issue with named causes, or maintainer-specified task). | required |
| scope_complexity | Issue description body and title | The issue description does NOT request a complete repository-wide architectural rewrite, multi-subsystem migration, or open-ended refactor of the entire codebase. | required |
| author_is_human | Issue creator username | The issue creator's username does not end in `[bot]`. | required |
| no_blocker_labels | Issue labels section | The issue labels section does NOT contain explicit rejection labels: `duplicate`, `invalid`, `wontfix`, or `needs-info`. | required |
| beginner_friendly_label | Issue labels section | Issue labels include `good first issue`, `help wanted`, `easy`, `documentation`, or `beginner-friendly`. | preferred |
| active_discussion | Issue comment thread | At least one comment posted within the last 90 days. | preferred |
| maintainer_involvement | Comment thread author badges | Comments from users with `Owner`, `Member`, or `Collaborator` badges. | preferred |

```
## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
Accept the candidate issue if and only if every check with weight `required` passes (`P`); otherwise, if any `required` check fails (`F`) or lacks sufficient evidence (`?`), reject the candidate issue, while checks with weight `preferred` are used solely for ranking accepted issues and never alter the accept or reject verdict.

