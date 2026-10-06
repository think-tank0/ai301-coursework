# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

- Where it lives: it lives in the repro evidence (https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5852187596 for live mode), and the candidate plan.

- What good looks like: the stated cause in the candidate plan explicitly matches to behavior identified in the repro-evidence block. 

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

- Where it lives: it lives in the candidate plan.

- What good looks like: it is bounded, it describes a single issue it is trying to solve. It states what is and not is in scope, might mention specific files to change. i.e. 
  modifying regex expression for email addresses, in scope: scrubber.py, not in scope: parser.py.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

- Where it lives: it lives in the candidate plan.

- What good looks like: it contains discrete sequence of steps needed to fix the issue. i.e. modify ../router.py -> replace route in ln 88 with (/comments) -> run unit test ../unit/test00.py

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

- Where it lives: it lives in the repro evidence (https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5852187596 for live mode), and the candidate plan.

- What good looks like: it states what steps to follow to validate that the fix was successful, it is grounded in the expected behavior described in the repro evidence. The command or test steps should match the ones descrribed on the repro evidence block.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

- Where it lives: candidate plan comment, Thread highlights (Issue comment thread in live mode).

- What good looks like: the candidate plan accounts for directions given by the repo owner or maintainer.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

- Where it lives: it lives in the candidate plan comment and the "contribution policy" line under Repo facts for the eval bundle. When running in live mode, the related info for contribution policy can be found in CONTRIBUTING.md in the repo root or .github/, and any contributor docs it links out to; the policy often hides one click away from the repo. Also, check files such as AI_POLICY.md or AI_USAGE_POLICY.md when live mode runs. PR and issue templates.

- What good looks like: the candidate plan comment contains disclosure of AI usage when requested by contribution policy and AI policy. It follows repo stated templates if present. It is specific and sets up expectations around next steps. i.e. Picking this up: --style is ignored on v1.20.0, exactly as described. I'm writing a repro report with my environment, steps, and log, then I'll attempt a fix. This is my first contribution, so flagging that.
