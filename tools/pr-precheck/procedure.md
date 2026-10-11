# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

1. Read the whole package before grading anything: read the repo facts 
(from here collect any policies and standards that the maintainer or repo
expect contributors to follow), the plan context (from here focus on 
repro evidence and plan as they contain directions that should be followed
by the PR, the info is mainly in repro evidence, plan, test plan, and deviation 
notes), lastly read the candidate PR (focus in the format, the files present 
in the diff, the description, and the test evidence). It is important to make sure 
that the description and test plan mentioned in the PR are grounded 
in the plan context's plan and repro evidence. 
The deciding evidence is usually if the candidate PR's is grounded in the plan context, that's why it 
is important to read the plan context first as it is the source of truth the candidate PR will be checked against.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->
1. For each check, gather exactly the evidence the rubric names, using
   the evidence guide's map.
   - Live mode: gather issue-side evidence from the locations the
     guide names; the drafts are the candidate side.
   - Eval mode: quote the relevant lines from the bundle.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Grade each check `pass`, `fail`, or `unclear`, with a one-line
   evidence quote or fact for each grade. `unclear` means the evidence
   needed is genuinely absent, not that you did not look.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->


1. Apply the rubric's verdict rule to produce the final verdict:
   `accept` (ready to post) or `reject` (hold). There is no third
   verdict.