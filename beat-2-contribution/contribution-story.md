# Contribution: [Issue Title]

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Wilman Rodriguez
**GitHub Username:** think-tank0
**Issue:** https://github.com/nvaccess/nvda/issues/20478
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: worked on building the issue-scout skill to retrieve and grade GitHub issues based on issue quality and my fit profile.**

I added queries and ranking filters to search-strategy.md. While running the skill, I realized there were a couple of edge cases that needed to be patched. Namely, I updated the issue-is-not-claimed check to also consider comments in the issue body, allowing it to catch cases where the issue author is already working on a fix. I also added a rubric check to discard issues that call out open issues as dependencies.

**Unit 6: worked on updating repro-check skill so that it will work with repos in the wild**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

The voice-guard installation steps did not work reliably for Windows, I troubleshooted the issue and realized that Claude did not always use the bash tool when using it on VS Code. I ended up adding a PowerShell specific hook to solve it. The repro-check tool itself did not break.

Did not run into any issues with the memory file.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I chose this issue after browsing through all of the Python project issues the course tool returned with a "good first issue" label. The thing that sold me on it was its practicality and narrow scope. I hope to learn more about the project itself, as I've never interacted with similar software in the past. The issue scout tool recommended the issue based on my experience with Python and the fact that the issue scope was well defined by the maintainer. Additionally, it prompted me to confirm that the two previous attempts on the PR were abandoned.

https://github.com/nvaccess/nvda/issues/20478#issuecomment-6479200335

**Toolkit**

- Tool: issue-scout, I used it to process and grade the two issues I short listed after browsing through the course issue browsing tool.
- What it produced: nvaccess/nvda#20478 — accept. Difficulty: straightforward.
- Difficulties: none.
- What changed: Replaced present-technical-details check for more robust scope-feasible check as directed by the assignment.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**
Environment: Python 3.13.15, Windows 11 (x64), Microsoft Edge Version 155.0.4283.45 (Official build) (64-bit), Google Chrome Version 155.0.8059.79 (Official Build) (64-bit), latest master, uv 0.13.6.

Steps: followed steps on contributing.md(projectDocs/dev/contributing.md) for dev environment setup -> create longParagraph.html file with the snippet below -> run source code -> open longParagraph.html on your favorite browser

contributing.md steps
1. Fork repository
2. Clone: git clone --recursive https://github.com/YOUR-USERNAME/nvda.git
3. Keep fork in sync
    # Add a remote for the NV Access repository.
    git remote add nvaccess https://github.com/nvaccess/nvda.git
    # Fetch the NV Access branches.
    git fetch nvaccess
    # Switch to the local master branch.
    git checkout master
    # Set the local master to use the NV Access master as its upstream.
    git branch -u nvaccess/master
    # Update the local master.
    git pull 
4. Install Microsoft Visual Studio
    Microsoft Visual Studio 2022 or 2026
    To replicate the production build environment, use the version of Visual Studio 2022 that GitHub Actions is using.
    If you don't use the Visual Studio IDE itself, you can download the build tools.
    If you do intend to use the Visual Studio IDE (not required for NVDA development), you can download the community version.
    The Professional and Enterprise versions are also supported.
    Preview or insiders versions are not supported.
    When installing Visual Studio, additional components must be included:
    You can automatically fetch these using NVDAs .vsconfig using the import feature of the VS installer.
    In the list on the Workloads tab, in the Desktop grouping:
    Desktop development with C++.
    Once selected, ensure "C++ Clang tools for Windows" is included under the optional grouping.
    On the Individual components tab, ensure the following items are selected:
    Windows 11 SDK (10.0.26100.x)
    MSVC v143 - VS 2022 C++ ARM64/ARM64EC build tools
    MSVC v143 - VS 2022 C++ x64/x86 build tools
    C++ ATL for v143 build tools (x86 & x64)
    C++ ATL for v143 build tools (ARM64/ARM64EC)
5. Build nvda from source: scons source
6. Execute runnvda.bat in the root directory

longParagraph.html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Long Paragraph Test</title>
</head>
<body>

<h1>Long Paragraph Test</h1>

<p id="target">
This is a single paragraph intentionally constructed to exceed two hundred fifty characters. The goal is to verify whether NVDA browse mode splits the content into multiple virtual lines based solely on the maximum line length setting rather than preserving the paragraph as a single continuous reading unit. Additional filler text continues here so that the paragraph exceeds two hundred and fifty characters and clearly triggers any configured wrapping behavior.
</p>

</body>
</html>

**Steps to Reproduce**
Manual test
runnvda.bat
NVDA + Ctrl + B
Set Maximum number of characters on one line to 300. It will be capped at 250.
NVDA + N -> Tools -> Speech viewer
Open longParagraph.html on browser
NVDA + space
downArrow + downArrow + downArrow

You should hear the following sentences after following the steps above. (Copied from Speech Viewer output)
heading    level 1  Long Paragraph Test
This is a single paragraph intentionally constructed to exceed two hundred fifty characters. The goal is to verify whether NVDA browse mode splits the content into multiple virtual lines based solely on the maximum line length setting rather than 
preserving the paragraph as a single continuous reading unit. Additional filler text continues here so that the paragraph exceeds two hundred and fifty characters and clearly triggers any configured wrapping behavior.

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** Speech viewer logs
This is a single paragraph intentionally constructed to exceed two hundred fifty characters. The goal is to verify whether NVDA browse mode splits the content into multiple virtual lines based solely on the maximum line length setting rather than 
preserving the paragraph as a single continuous reading unit. Additional filler text continues here so that the paragraph exceeds two hundred and fifty characters and clearly triggers any configured wrapping behavior.
- **My findings:** I tested the current Behavior of the Browser Mode while reading paragraphs and validated the 250 character limit.

**Toolkit**

- Tool: repro-check, I used the tool to grade the claim comment and repro report draft for the issue.
- What it produced: it accepted both the comment and the repro report.
- Difficulties: setting up the hooks to work on Windows OS.
- What changed: nothing besides the additions to the voice guide.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
