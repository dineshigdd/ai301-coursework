# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60

**Verdict output**

Grading summary

  Repo-level facts (apply to all three, codepath/pathreview-ai301-fa26-s1): not archived, pushed 2026-09-16 (4 days before today), collaborator commits active →
  active_repository passes for all. No CONTRIBUTING.md, .github/CONTRIBUTING.md, AGENTS.md, or AI_POLICY.md found (all 404) → silence passes, policy_compliance passes   
  for all.

  Issue #60 — Faithfulness checker crashes on text: None
```bash
  ┌────────────────────────────────┬───────┬────────────────────────────────────────────┐
  │             Check              │ Grade │                  Evidence                  │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ active_repository              │ pass  │ repo pushed 2026-09-16, not archived       │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ policy_compliance              │ pass  │ no contribution/AI policy file found       │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ unassigned_issue               │ pass  │ assignees: [], comments: 0                 │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ clear_requirements             │ pass  │ exact repro code + TypeError given         │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ scope_complexity               │ pass  │ single-method fix in check()               │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ author_is_human                │ pass  │ Aburke225, not a bot                       │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ no_blocker_labels              │ pass  │ labels: bug, good first issue, rag, tier-1 │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ beginner_friendly_label (pref) │ pass  │ "good first issue" label                   │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ active_discussion (pref)       │ fail  │ 0 comments                                 │
  ├────────────────────────────────┼───────┼────────────────────────────────────────────┤
  │ maintainer_involvement (pref)  │ fail  │ 0 comments                                 │
  └────────────────────────────────┴───────┴────────────────────────────────────────────┘
```
  Verdict: accept

  Issue #62 — Health check uses nonexistent settings.redis_host

  Same repo-level facts. assignees: [], comments: 0, clear bug description with repro steps, single-file fix in health.py, human collaborator author, labels bug/good    
  first issue/api/tier-1 (no blockers).

  Verdict: accept

  Issue #34 — Add X-RateLimit-Remaining header

  Same repo-level facts. assignees: [], comments: 0, clear ask (wire up existing check_rate_limit via middleware, set two headers), bounded to 3 named files with a 3–5  
  hr estimate (not a rewrite), human collaborator author, labels enhancement/api/tier-2 (no blockers). beginner_friendly_label (preferred) fails — no
  easy/good-first-issue label — but that's preferred-only.

  Verdict: accept

  Ranking (fit profile: JS/TS/Python, prefers backend & AI-related work, wants moderate challenge, avoid docs/testing)

  1. #34 — backend API work, tier-2 with a 3–5 hr estimate: the "more challenging but not too difficult" tier the profile asked for, and squarely backend.
  2. #60 — backend Python, and the only one that's actually AI/RAG-related (FaithfulnessChecker), matching the stated AI preference; but it's a one-line default-value   
     bug, so it's on the easy end.
  3. #62 — backend Python, same easy tier-1 bug-fix size as #60, but generic health-check code rather than AI-related, so it satisfies fewer of the stated preferences.  

```json
[
  {
    "item": "[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/34](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/34)",
    "checks": [
      {"name": "active_repository", "grade": "pass", "evidence": "repo pushed_at 2026-09-16T21:48:27Z, archived:false"},
      {"name": "policy_compliance", "grade": "pass", "evidence": "no CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (404s); silence passes"},
      {"name": "unassigned_issue", "grade": "pass", "evidence": "assignees: [], comments_count: 0"},
      {"name": "clear_requirements", "grade": "pass", "evidence": "body: 'Add middleware that calls it and sets both headers' with named relevant files"},
      {"name": "scope_complexity", "grade": "pass", "evidence": "bounded to api/middleware/, safety/rate_limiter.py, api/main.py; estimated effort 3-5 hours"},
      {"name": "author_is_human", "grade": "pass", "evidence": "user_login: Aburke225, no [bot] suffix"},
      {"name": "no_blocker_labels", "grade": "pass", "evidence": "labels: enhancement, api, tier-2"},
      {"name": "beginner_friendly_label", "grade": "fail", "evidence": "labels do not include good first issue/help wanted/easy/documentation/beginner-friendly"},
      {"name": "active_discussion", "grade": "fail", "evidence": "comments_count: 0"},
      {"name": "maintainer_involvement", "grade": "fail", "evidence": "comments_count: 0, no thread badges to evaluate"}
    ],
    "verdict": "accept"
  },
  {
    "item": "[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60)",
    "checks": [
      {"name": "active_repository", "grade": "pass", "evidence": "repo pushed_at 2026-09-16T21:48:27Z, archived:false"},
      {"name": "policy_compliance", "grade": "pass", "evidence": "no CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (404s); silence passes"},
      {"name": "unassigned_issue", "grade": "pass", "evidence": "assignees: [], comments_count: 0"},
      {"name": "clear_requirements", "grade": "pass", "evidence": "body gives exact repro: 'FaithfulnessChecker().check(...) # TypeError: sequence item 0...'"},
      {"name": "scope_complexity", "grade": "pass", "evidence": "single fix to chunk.get('text','') default-handling in check()"},
      {"name": "author_is_human", "grade": "pass", "evidence": "user_login: Aburke225, no [bot] suffix"},
      {"name": "no_blocker_labels", "grade": "pass", "evidence": "labels: bug, good first issue, rag, tier-1"},
      {"name": "beginner_friendly_label", "grade": "pass", "evidence": "labels include 'good first issue'"},
      {"name": "active_discussion", "grade": "fail", "evidence": "comments_count: 0"},
      {"name": "maintainer_involvement", "grade": "fail", "evidence": "comments_count: 0, no thread badges to evaluate"}
    ],
    "verdict": "accept"
  },
  {
    "item": "[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62)",
    "checks": [
      {"name": "active_repository", "grade": "pass", "evidence": "repo pushed_at 2026-09-16T21:48:27Z, archived:false"},
      {"name": "policy_compliance", "grade": "pass", "evidence": "no CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (404s); silence passes"},
      {"name": "unassigned_issue", "grade": "pass", "evidence": "assignees: [], comments_count: 0"},
      {"name": "clear_requirements", "grade": "pass", "evidence": "body names exact mismatch (redis_host vs redis_url) plus repro via GET /health"},
      {"name": "scope_complexity", "grade": "pass", "evidence": "single fix in api/routes/health.py Redis probe"},
      {"name": "author_is_human", "grade": "pass", "evidence": "user_login: Aburke225, no [bot] suffix"},
      {"name": "no_blocker_labels", "grade": "pass", "evidence": "labels: bug, good first issue, api, tier-1"},
      {"name": "beginner_friendly_label", "grade": "pass", "evidence": "labels include 'good first issue'"},
      {"name": "active_discussion", "grade": "fail", "evidence": "comments_count: 0"},
      {"name": "maintainer_involvement", "grade": "fail", "evidence": "comments_count: 0, no thread badges to evaluate"}
    ],
    "verdict": "accept"
  }
]
```

## Eval iterations

```bash
python3 run_eval.py --rubric /mnt/c/Use
grading 20 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-04: reject
  issue-02: accept
  issue-01: reject
  issue-03: reject
  issue-05: reject
  issue-06: accept
  issue-07: accept
  issue-10: reject
  issue-08: reject
  issue-11: reject
  issue-09: accept
  issue-13: reject
  issue-12: accept
  issue-14: reject
  issue-17: accept
  issue-16: reject
  issue-18: reject
  issue-19: reject
  issue-15: reject
  issue-20: reject

item      gold    verdict  agree  note
issue-01  accept  reject   NO     failed: clear_requirements, scope_complexity, active_discussion (preferred), maiabel (preferred)
issue-02  reject  accept   NO     graded accept
issue-03  reject  reject   yes    
issue-04  accept  reject   NO     failed: active_discussion (preferred), maintainer_involvement (preferred), clear
issue-05  reject  reject   yes    
issue-06  accept  accept   yes    
issue-07  reject  accept   NO     graded accept
issue-08  reject  reject   yes    
issue-09  accept  accept   yes    
issue-10  reject  reject   yes    
issue-11  accept  reject   NO     failed: clear_requirements, scope_complexity, active_discussion (preferred), maiabel (preferred)
issue-12  reject  accept   NO     graded accept
issue-13  reject  reject   yes    
issue-14  accept  reject   NO     failed: active_discussion (preferred), maintainer_involvement (preferred), scope
issue-15  reject  reject   yes    
issue-16  accept  reject   NO     failed: active_discussion (preferred), maintainer_involvement (preferred), clear
issue-17  reject  accept   NO     graded accept
issue-18  reject  reject   yes    
issue-19  accept  reject   NO     failed: clear_requirements, scope_complexity, active_discussion (preferred), maiabel (preferred)
issue-20  reject  reject   yes    

categories: claimed 4/4  clear-accept 2/8  dead-repo 0/3  policy 0/1  scope 4/4
agreement: 10/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in dead-repo, policy)
dinesh@DINESH-LAPTOP:/mnt/f/codepath/ai301/unit1/ai301-unit1-starter/eval$ H-LAPTOP:/mnt/f/codepath/ai301/unit1/ai301-unit1-starter/eva
dinesh@DINESH-LAPTOP:/mn
dinesh@DINESH-LAPTOP:/mnt/f/codepath/ai301/unit1/ai301-unit1-starter/eval$ python3 run_eval.py --rubric /mnt/c/Users/Dinesh/.claude/skills/issue-select/rubric.md --only issue-01,issue,issue-16,issue-17,issue-19
grading 10 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-07: reject
  issue-11: accept
  issue-04: accept
  issue-02: reject
  issue-01: reject
  issue-14: accept
  issue-17: reject
  issue-16: accept
  issue-12: reject
  issue-19: reject

item      gold    verdict  agree  note
issue-01  accept  reject   NO     failed: scope_complexity, active_discussion (preferred), maintainer_involvement (preferred)
issue-02  reject  reject   yes    
issue-04  accept  accept   yes    
issue-07  reject  reject   yes    
issue-11  accept  accept   yes    
issue-12  reject  reject   yes    
issue-14  accept  accept   yes    
issue-16  accept  accept   yes    
issue-17  reject  reject   yes    
issue-19  accept  reject   NO     failed: scope_complexity, beginner_friendly_label (preferred), active_discussion (preferred), maintainer_involvement (preferred)

agreement: 8/10 scored items
dinesh@DINESH-LAPTOP:/mnt/f/codepath/ai301/unit1/ai301-unit1-starter/eval$ python3 run_eval.py --rubric /mnt/c/Users/Dinesh/.claude/skills/issue-select/rubric.md --only issue-01,issue
grading 2 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-19: reject
  issue-01: reject

item      gold    verdict  agree  note
issue-01  accept  reject   NO     failed: scope_complexity, active_discussion (preferred), maintainer_involvement (preferred)
issue-19  accept  reject   NO     failed: scope_complexity, beginner_friendly_label (preferred), active_discussion (preferred), maintainer_involvement (preferred)

agreement: 0/2 scored items
dinesh@DINESH-LAPTOP:/mnt/f/codepath/ai301/unit1/ai301-unit1-starter/eval$ python3 run_eval.py --rubric /mnt/c/Users/Dinesh/.claude/skills/issue-select/rubric.md --only issue-01,issue
grading 2 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-01: accept
  issue-19: accept

item      gold    verdict  agree  note
issue-01  accept  accept   yes    
issue-19  accept  accept   yes    

agreement: 2/2 scored items
dinesh@DINESH-LAPTOP:/mnt/f/codepath/ai301/unit1/ai301-unit1-starter/eval$ python3 run_eval.py --rubric /mnt/c/Users/Dinesh/.claude/skills/issue-select/rubric.md --save-run ../beat-1-
grading 20 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-04: accept
  issue-03: reject
  issue-02: reject
  issue-01: accept
  issue-06: accept
  issue-07: reject
  issue-08: reject
  issue-05: reject
  issue-11: accept
  issue-12: reject
  issue-10: reject
  issue-13: accept
  issue-09: reject
  issue-14: accept
  issue-16: accept
  issue-17: reject
  issue-15: accept
  issue-20: reject
  issue-18: reject
  issue-19: reject

item      gold    verdict  agree  note
issue-01  accept  accept   yes    
issue-02  reject  reject   yes    
issue-03  reject  reject   yes    
issue-04  accept  accept   yes    
issue-05  reject  reject   yes    
issue-06  accept  accept   yes    
issue-07  reject  reject   yes    
issue-08  reject  reject   yes    
issue-09  accept  reject   NO     failed: no_blocker_labels, active_discussion (preferred)
issue-10  reject  reject   yes    
issue-11  accept  accept   yes    
issue-12  reject  reject   yes    
issue-13  reject  accept   NO     graded accept
issue-14  accept  accept   yes    
issue-15  reject  accept   NO     graded accept
issue-16  accept  accept   yes    
issue-17  reject  reject   yes    
issue-18  reject  reject   yes    
issue-19  accept  reject   NO     failed: scope_complexity, beginner_friendly_label (preferred), active_discussion (preferred), maintainer_involvement (preferred)
issue-20  reject  reject   yes    

categories: claimed 3/4  clear-accept 6/8  dead-repo 3/3  policy 1/1  scope 3/4
agreement: 16/20 scored items  (bar: 18/20: below the bar)
run written to ../beat-1-sandbox/unit-1/eval-run.txt
dinesh@DINESH-LAPTOP:/mnt/f/codepath/ai301/unit1/ai301-unit1-starter/eval$ python3 run_eval.py --rubric /mnt/c/Users/Dinesh/.claude/skills/issue-select/rubric.md --only issue-09,issue
grading 4 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-13: reject
  issue-19: accept
  issue-15: accept
  issue-09: accept

item      gold    verdict  agree  note
issue-09  accept  accept   yes    
issue-13  reject  reject   yes    
issue-15  reject  accept   NO     graded accept
issue-19  accept  accept   yes    

agreement: 3/4 scored items
dinesh@DINESH-LAPTOP:/mnt/f/codepath/ai301/unit1/ai301-unit1-starter/eval$ python3 run_eval.py --rubric /mnt/c/Users/Dinesh/.claude/skills/issue-select/rubric.md --save-run ../beat-1-txt
grading 20 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-03: reject
  issue-01: accept
  issue-04: accept
  issue-02: reject
  issue-05: reject
  issue-06: accept
  issue-07: reject
  issue-08: reject
  issue-11: accept
  issue-10: reject
  issue-13: reject
  issue-12: reject
  issue-14: accept
  issue-09: accept
  issue-16: accept
  issue-17: reject
  issue-18: reject
  issue-15: accept
  issue-20: reject
  issue-19: accept

item      gold    verdict  agree  note
issue-01  accept  accept   yes    
issue-02  reject  reject   yes    
issue-03  reject  reject   yes    
issue-04  accept  accept   yes    
issue-05  reject  reject   yes    
issue-06  accept  accept   yes    
issue-07  reject  reject   yes    
issue-08  reject  reject   yes    
issue-09  accept  accept   yes    
issue-10  reject  reject   yes    
issue-11  accept  accept   yes    
issue-12  reject  reject   yes    
issue-13  reject  reject   yes    
issue-14  accept  accept   yes    
issue-15  reject  accept   NO     graded accept
issue-16  accept  accept   yes    
issue-17  reject  reject   yes    
issue-18  reject  reject   yes    
issue-19  accept  accept   yes    
issue-20  reject  reject   yes    

categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 3/4
agreement: 19/20 scored items  (bar: 18/20: PASS)
run written to ../beat-1-sandbox/unit-1/eval-run.txt

```
**Run history**
- Initial run: 10/20 agreement score (10/20 scored items)
- Second run: 16/20 agreement score (16/20 scored items)
- Final run: 19/20 agreement score (19/20 scored items)

**Issue analysis**
`issue-07`

Rubric Decision: `accept`
Gold Label: `accept`
Reasoning: `issue-07` presents clear steps to reproduce a backend bug, names the exact file location requiring a fix, and has no assignee or blocker labels. Both my rubric and the gold standard evaluated the scope as manageable for a tier-1 first issue with an active repository context, resulting in aligned accept verdicts.

**Check rationale**  
The issue is currently open, displays "No one assigned" in the assignees sidebar, and has no active claim comments or open pull requests submitted by external contributors in the comment thread.

Reasoning: I defined this check using objective GitHub API attributes (assignees array length `assignees: []` and comment text patterns) rather than vague subjective criteria like "seems open". This threshold guarantees zero ambiguity when determining whether another contributor has already claimed an issue.

**Trade-offs**  
In my rubric design, I prioritized high precision over high recall for beginner-friendly issues. By requiring strict evidence of clear reproduction steps or specific file references for `clear_requirements`, the rubric occasionally flags broad enhancement requests as ambiguous. This trade-off prevents contributors from taking on underspecified issues that lead to dead ends during implementation.

---

## Selection rationale

**Selection rationale**
1. Fit to interests & time: Issue #60 fits my interest in Python and RAG evaluation systems because it specifically targets a RAG evaluation module (`FaithfulnessChecker`) in `rag/evaluator/faithfulness_checker.py`. With a clear single-method scope and explicit reproduction steps, it fits well within the 3–5 hour effort window for Beat 1.
2. What verdict identified vs. weighed manually: The verdict correctly identified that the repository is active, the issue is unclaimed (`assignees: []`), and it contains clear reproduction code with a `TypeError`. Manually, I weighed the specific domain context—preferring a RAG bug over a generic health check (#62) or a broader API middleware task (#34)—to ensure it matches my AI engineering focus.
3. Anticipated difficulty in claiming: I anticipate low difficulty in claiming it. The issue has 0 comments and no assigned users, meaning it is completely open and ready for a claim comment in Unit 2.
