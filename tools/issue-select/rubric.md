# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| mantainer-replies-to-issues  | maintainer first-response sample, repo-facts block | ignore issues opened 3 months before the repo-facts were captured, maintainer replied within 30 days | preferred |
| active-repo | latest release date | released a new version in the last 6 months, ignore if no date is available | required |
| active-branches | last push to any branch | PR pushed within the last 6 months, ignore if no date is available | required |
| present-technical-details | issue body | contains issue description, might contain suggestions and other technical details | required |
| present-repro-steps | issue body | provides reproduction steps | preferred |
| issue-is-not-claimed | this issue section under repo-facts block | no assignees  | required |
| no-linked-pr | this issue section under repo-facts block | no open linked PRs  | required |
| ai-welcomed | contribution policy section under repo-facts block | AI usage not prohibited or discouraged | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
accept if every required check passes, preferred do not change the verdict, they
rank accepted issues; unclear counts as fail, except for the mantainer-replies-to-issues check and active-repo check where it will count as a pass.