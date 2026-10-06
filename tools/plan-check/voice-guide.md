# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2; paste your filled week-2 voice-guide.md here, whole. It is not
re-authored and it is not graded as new work this week.

Then reread it with the plan comment in mind. Your claim and repro
comments promised and reported; a plan comment commits you to an
approach in front of the people who maintain the code. If your rules
do not cover that register (for example: how you state an approach you
are not certain of, or how you respond when a maintainer already
suggested a direction), extend the guide with what it needs. Extending
is allowed and encouraged; starting over is not required.

Live mode reads this file before your plan comment goes out and
reports any rule your draft breaks. Eval mode ignores it entirely,
because your voice is yours and carries no gold labels.
-->

## Who I am in threads

<!-- Paste your week-2 section here. -->
I have handled beginner-friendly or good-first issues successfully, and I am ready to challenge myself to tackle issues with intermediate difficulty. I am focused on AI-related issues in tier-1 or backend/API-related issues in tier-1 or tier-2. I would like to stay away from issues related to testing and documentation.

## Rules I write by

<!-- Paste your week-2 rules here, wrong/right pairs and all. Add any
rule the plan-comment register needs that your week-2 comments did
not. -->
Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"


### Rule: Lead with execution

Always state what was tested and what output was observed before proposing hypotheses or asking questions. Never post empty "I will look into this" promises.

- Wrong: "I'm going to take a look at this issue and try to reproduce it on my local machine soon."
- Right: "Reproduced on Python 3.11 / v4.53.2. Running the script with the `--config` flag throws `KeyError: 'embeddings'` as shown in the attached output."

### Rule: Pin the environment

When sharing a bug finding, pair every error message with the exact OS, dependency versions, and command used. Avoid vague statements about environment setup.

- Wrong: "I ran the server on my machine and it failed with a database connection error."
- Right: "Executed `docker-compose up backend` on macOS 14.5 (Docker v26.1.1). The container exited with `ConnectionRefusedError: [Errno 111] Could not connect to Postgres on port 5432`."

### Rule: Facts over hypotheses

Clearly distinguish between observed terminal output and your personal guess about root cause. Never state an unverified guess as a proven fact.

- Wrong: "The issue is caused by the async event loop closing before the Supabase client finishes writing."
- Right: "The trace shows `RuntimeError: Event loop is closed`. This likely points to an issue with how the Supabase client handles async cleanup, though I am still testing that specific path."

### Rule: No-fluff disclosures

Include mandatory disclosures (such as AI usage or tool assistance) cleanly and concisely in accordance with repository guidelines without making excuses or adding defensive preamble.

- Wrong: "Sorry if this comment isn't perfect, I used an AI assistant to help me draft the reproduction script because I'm new to this module."
- Right: "Reproduction script generated and tested with AI assistance in accordance with repo contribution guidelines."

### Rule: Commit to approaches with grounded confidence

When proposing a plan, explicitly state the technical approach and targeted files based on verified reproduction facts. If a maintainer suggested a direction or an edge case remains uncertain, acknowledge it directly without making unverified promises.

- Wrong: "I think this might fix the bug, so I'll probably try changing a few files tomorrow and see if it works."
- Right: "Proposed fix modifies `src/auth/client.py` to handle loop closure during cleanup as detailed in `plan.md`. Following @maintainer's suggestion, this approach avoids mutating global state."


## Things I never post

<!-- Paste your week-2 list here; extend it if planning tempts you
toward new ones (overpromised timelines are the classic). -->
- Unprofessional, aggressive, offensive, or dismissive comments.
- Off-topic chit-chat or commentary unrelated to the specific issue thread.
- Unverified timeline promises (e.g., "I will fix this by tomorrow").
- Apologetic or self-deprecating statements about skill level (e.g., "Sorry, I am new here", "Pardon if this is a silly question").
- Speculative root-cause claims presented without a supporting terminal trace or log snippet.
- Generic boilerplate greetings or polite fluff (e.g., "Hope this helps!", "Thanks for reading!").