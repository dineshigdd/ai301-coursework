Want to contribute to open source? In this post, I’ll share how I tackled my first open-source contribution with the help of AI coding agents.

As a student at CodePath—a community focused on AI-assisted software engineering—I had the opportunity to contribute to Kaoto, an open-source visual integration builder on GitHub.I initially looked for a backend or AI-related task, but since those issues didn't fit my timeline, I pivoted to a UI bug: fixing column misalignments between parameter tables inside Kaoto's component properties modal.

To solve this, I looked past quick CSS fixes and addressed the core layout structure. I refactored the component code to group consecutive tables that shared identical headers into a single <Table> element utilizing multiple <tbody> row groups. This ensured the browser rendered the columns with uniform widths. I also updated the component test suite to verify the layout fix.


You can check out my pull request and code changes [here](https://github.com/KaotoIO/kaoto/pull/4412#issue-6322633045)

#OpenSource #React #TypeScript #WebEngineering #CodePath
