# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->
-**Where it lives**
  -**Eval mode:** Look inside the `# Candidate Repro Report` block, specifically under the `Environment.` header or section.
  -**Live mode:**  Look inside the candidate's draft report file (e.g., under `## Reproduction Report:` or `# Candidate Reproduction Report`), specifically under the `Environment.` header.


- **What good looks like:**
  - Explicitly states **both** the tool/runtime version (e.g., `yq version 4.53.3`) **and** the host operating system (e.g., `macOS 15.5 (arm64)`).
  - Shell info (e.g., `zsh 5.9`) or installation method (e.g., `Homebrew`) can be present as optional context, but are not required to pass.
  - **Fails if:** Missing either the OS or tool version, or if it only contains general claims (e.g., "tested on Mac") without explicit version numbers.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->
looks like against the issue's stated target. -->
- **Where it lives:**
  - **Eval mode:** Look inside the `# Candidate Repro Report` block, specifically under the `Preparation` and `Execution` headers (or equivalent reproduction step sections).
  - **Live mode:** Look inside the candidate's draft report file, under the `Preparation` and `Execution` headers (or equivalent reproduction step sections).

- **What good looks like:**
  - Provides complete, step-by-step instructions needed to reproduce the issue from scratch.
  - Includes exact setup details (e.g., sample input files, config) under `Preparation` and the exact command or action used to trigger the bug under `Execution`.
  - Commands and code blocks are clear, specific, and copy-pasteable so a stranger can follow them.
  - **Fails if:** Steps are vague or incomplete (e.g., "create an input file and run yq" without providing the actual file contents or command arguments), or if essential setup/execution commands are missing entirely.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->
- **Where it lives:**
  - **Eval mode:** Look inside the `# Candidate Repro Report` block, under the `Actual.` and `Expected.` headers (or right after commands in `Execution.`).
  - **Live mode:** Look inside the candidate's draft report file, under the `Actual.` and `Expected.` headers (or right after commands in `Execution.`).

- **What good looks like:**
  - `Actual.` explicitly details the specific failure or incorrect behavior, providing raw evidence/artifacts such as terminal logs, stack traces, output excerpts, or screenshots.
  - `Expected.` explicitly states the correct/intended behavior, which may include expected code snippets, YAML outputs, or descriptions of expected success.
  - **Fails if:** `Actual.` only summarizes the failure conceptually (e.g., "it crashed" or "it failed") without providing raw output/log artifacts, or if either `Actual.` or `Expected.` is omitted.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->
- **Where it lives:**
  - **Eval mode:** Look inside the `# Candidate Repro Report` block, specifically comparing the candidate's claims in `Analysis.` against the command output in `Execution.`/`Actual.`.
  - **Live mode:** Look inside the candidate's draft report, specifically comparing claims in `Analysis.` against the execution output logs.

- **What good looks like:**
  - The conclusions in `Analysis.` truthfully reflect what the execution logs show.
  - Accurately states whether the bug was reproduced or not, and explicitly notes if a different version/environment was tested.
  - **Fails if:** Claims a bug was reproduced when the output log shows an unrelated setup/syntax error (e.g., `command not found`, wrong flags, missing file), makes claims contradicted by the logs, or claims to test a specific version without disclosing that a different version/environment was actually used.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->
- **Where it lives:**
  - **Eval mode:** Look inside the `# Candidate claim comment` block.
  - **Live mode:** Look inside the candidate's draft or posted issue/PR comment on GitHub, cross-referenced against the repository's issue templates and contribution policies (including AI-use disclosures).

- **What good looks like:**
  - States clear intent to investigate or report findings on the specific issue.
  - Serves as a concise, informal summary of the full reproduction report found under `# Candidate Repro Report`.
  - May include supporting context, key observations (e.g., unintended behaviors, environmental quirks), suggestions, or evidence snippets.
  - Complies with repository contribution guidelines and required policies (e.g., AI-use disclosures).
  - Maintains a clear, professional, and grounded tone.
  - **Fails if:** Uses generic or unhelpful boilerplate, contains overly emotional or unprofessional remarks, fails required policy/AI-use disclosures, or makes claims that contradict the reproduction report.
