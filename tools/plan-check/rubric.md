# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | candidate plan, repro-evidence | stated cause for the issue, it is grounded on repro evidence from repro report | required |
| scope | candidate plan | indicates what is in scope and what is not in scope. The scope is bounded to a single goal | required |
| files-to-modify | candidate plan | states at least a file that will be modified | required |
| approach-to-follow | candidate plan | states what will be done, it contains at least one explicit step that can be run by a stranger to start implementing the plan | required |
| test-plan | candidate plan, repro-evidence | the test is grounded on the repro-evidence steps and it describes the expected behavior that should be observed to declare success, the behavior must match the one described in the Expected section of the repro-evidence block | required |
| disclose-ai-usage | candidate plan comment, contribution policy | disclose AI usage if requested by policy | required |
| thread-highlights | candidate plan comment, Thread highlights | the plan accounts and follows thread directions given by the owner, pass if no directions are provided by repo owner/maintainer | required |



## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail, except for expected-vs-actual-result.