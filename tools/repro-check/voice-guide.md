# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->
I have handled beginner-friendly or good-first issues successfully, and I am ready to challenge myself to tackle issues with intermediate difficulty. I am focused on AI-related issues in tier-1 or backend/API-related issues in tier-1 or tier-2. I would like to stay away from issues related to testing and documentation.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->
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

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->
- Unprofessional, aggressive, offensive, or dismissive comments.
- Off-topic chit-chat or commentary unrelated to the specific issue thread.
- Unverified timeline promises (e.g., "I will fix this by tomorrow").
- Apologetic or self-deprecating statements about skill level (e.g., "Sorry, I am new here", "Pardon if this is a silly question").
- Speculative root-cause claims presented without a supporting terminal trace or log snippet.
- Generic boilerplate greetings or polite fluff (e.g., "Hope this helps!", "Thanks for reading!").