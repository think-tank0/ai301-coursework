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

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Single candidate this time, re-verified live against today (2026-09-20); state is unchanged from the batch run above.

- mantainer-replies-to-issues (preferred) — pass: Aburke225 (COLLABORATOR) replied on #52 and #43 on 2026-09-16, six days after those issues opened.
- active-repo (required) — unclear → pass by the verdict rule: the repo has zero releases and zero tags, so no release date exists.
- active-branches (required) — pass: pushed_at 2026-09-16T21:48:27Z, four days ago; not archived.
- present-technical-details (required) — pass: body names pii_scrubber.py and the exact gap between the dashed and parenthesized patterns.
- present-repro-steps (preferred) — pass: runnable snippet with observed scrub() / detect() output.
- issue-is-not-claimed (required) — pass: assignees: [], 0 comments.
- no-linked-pr (required) — pass: timeline holds only the four label events; the repo has 0 PRs in any state.
- ai-welcomed (required) — pass: docs/CONTRIBUTING.md, the PR template and the issue templates impose no AI restriction, and there is no AI policy file.

Every required check passes → accept. Same caveat as before: the fit profile in scope.md is still the placeholder, but with one candidate there is nothing to rank, so it doesn't affect this result.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
  "checks": [
    {"name": "mantainer-replies-to-issues", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) replied on #52 and #43 on 2026-09-16, 6 days after they opened 2026-09-10 — within 30 days"},
    {"name": "active-repo", "grade": "unclear", "evidence": "/releases and /tags both return 0 entries — no release date available; verdict rule counts this unclear as a pass"},
    {"name": "active-branches", "grade": "pass", "evidence": "repo pushed_at 2026-09-16T21:48:27Z, 4 days before grading; archived: false"},
    {"name": "present-technical-details", "grade": "pass", "evidence": "body names the file and the gap: phone pattern in pii_scrubber.py \"matches dashed formats like 555-123-4567 but not the parenthesized format (555) 123-4567\""},
    {"name": "present-repro-steps", "grade": "pass", "evidence": "\"**Steps to reproduce:**\" snippet with observed scrub() and detect() output, plus four named failing tests"},
    {"name": "issue-is-not-claimed", "grade": "pass", "evidence": "assignees: [] and 0 comments as of 2026-09-20"},
    {"name": "no-linked-pr", "grade": "pass", "evidence": "timeline has only 4 labeled events; repo has 0 PRs in any state"},
    {"name": "ai-welcomed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md, PR template and issue templates state no AI restriction; no AI policy file"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

agreement: 2/3 scored items
agreement: 12/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in clear-accept)
agreement: 12/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in clear-accept)
agreement: 1/4 scored items
agreement: 2/2 scored items
agreement: 13/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)
agreement: 4/5 scored items
agreement: 1/1 scored items
agreement: 17/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)
agreement: 0/1 scored items
agreement: 1/1 scored items
agreement: 17/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)
agreement: 0/1 scored items
agreement: 1/1 scored items
agreement: 18/20 scored items  (bar: 18/20: PASS)

**Issue analysis**

issue-07
rubric decision: reject
gold label: reject
reasoning: The issue itself is well-described with a clear repro and root-cause pointer, and it's unclaimed with no competing PR — but `active-branches` is a required check and fails clearly: the repo hasn't seen a push to any branch in ~17 months, well past the 6-month bar, and that alone is enough to reject regardless of the other required passes.

**Check rationale**

check: | no-linked-pr | this issue section under repo-facts block | no open linked PRs  | required |

The check's initial pass condition was "no linked PRs", but that wasn't enough because it even filtered out issues with linked PRs that were not open. 

**Trade-offs**

This check in its final version made it so that issue-09 was accepted, it didn't impact any of the other results as it treated Open PRs as a signal that the issue was taken.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. The issue's fit to your interests and to the time available: yes.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not: The verdict correctly identified the scope of the issue, the one thing I was able to assess that the rubric doesn't account for is the estimated effort to complete a fix.
3. The anticipated difficulty in claiming it: I think it should be moderately difficult to claim the issue.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
