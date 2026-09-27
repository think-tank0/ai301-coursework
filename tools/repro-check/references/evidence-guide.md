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

- Where it lives: it lives in the issue body, the claim comment, and the repro report.

- What good looks like: the versions named in both the claim comment, and the repro report match the ones found in the issue body.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

- Where it lives: it lives in the repro report.

- What good looks like: it contains discrete sequence of steps needed to reproduce the issue. i.e. clone → checkout v1.20.0 → build → run the issue's exact command

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

- Where it lives: it lives in the repro report.

- What good looks like: contains ran commands and their outputs, might contain logs and screenshots detailing observed behavior. The command or repro steps should match the ones descrribed on the issue's body.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

- Where it lives: it lives in the claims issue and repro report.

- What good looks like: disclosure of first contributions to the project or an open source contribution; disclosure of AI use. All claims are backed by evidence showing raw output and the steps and commands that yielded said output.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

- Where it lives: it lives in the claims issue and the "contribution policy" line under Repo facts for the eval bundle. When running in live mode, the related info for contribution policy can be found in CONTRIBUTING.md in the repo root or .github/, and any contributor docs it links out to; the policy often hides one click away from the repo. Also, check files such as AI_POLICY.md or AI_USAGE_POLICY.md when live mode runs. PR and issue templates.

- What good looks like: the claims comment contains disclosure of AI usage when requested by contribution policy and AI policy. It follows repo stated templates if present. It is specific and sets up expectations around next steps. i.e. Picking this up: --style is ignored on v1.20.0, exactly as described. I'm writing a repro report with my environment, steps, and log, then I'll attempt a fix. This is my first contribution, so flagging that.