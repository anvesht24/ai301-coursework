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
| maintains_activity | `repo-facts` block -> `last_commit_date` on default branch; comment thread author associations | Last commit on the default branch within 180 days OR at least one maintainer/collaborator comment in the thread within 90 days. | required |
| is_unclaimed | `assignees` list, linked pull requests, comment thread | `assignees` is empty AND no linked PRs (open or merged) AND no non-maintainer comment in the past 30 days claiming the work. | required |
| no_blocking_state_labels | Issue metadata -> `labels` array | Issue does NOT contain any of: `blocked`, `in-progress`, `claimed`, `wontfix`, `wont-fix`, `duplicate`, `invalid`, `needs-spec`, `needs-design`, `needs-triage`, `on-hold`, `rfc`. | required |
| contribution_welcome | Issue body AND all comments, with special attention to any comment where `author_association` is OWNER, MEMBER, or COLLABORATOR | PASS by default — contributions are welcome unless the maintainers say otherwise. FAIL only if the issue body or a maintainer comment contains one of these gate patterns: (a) asks contributors to wait to be assigned, comment to be assigned, or get approval before working ("please wait", "comment to claim", "ask before working", "do not start without assignment"); (b) states the issue is for the core team, maintainers, specific people, or a specific program only; (c) says a design, spec, RFC, triage, or further discussion must happen first before any PR; (d) says "do not submit a PR", "no PRs please", or the issue is on hold, deferred, or reserved; (e) a maintainer has told a previous commenter to stop or wait. If no such statement appears anywhere, this check PASSES — treat silence as welcome, not as unclear. | required |
| clear_task | Issue body | PASS if the issue describes a task a newcomer could understand and scope — this includes bug reports (with observed vs expected behavior OR a clear symptom), documentation fixes, typo and grammar corrections, small UI tweaks, test additions, dependency bumps, small features, and enhancements with a defined deliverable. The issue does not have to include repro steps or acceptance criteria to pass. FAIL only if the issue is: an open-ended discussion or question with no concrete deliverable ("what should we do about X?", "thoughts on Y?"), a sweeping refactor or redesign spanning many unrelated areas, or so vague that it is impossible to tell what "done" would look like. | required |
| beginner_friendly_label | Issue metadata -> `labels` array | Issue contains at least one of: `good first issue`, `help wanted`, `easy`, `documentation`, `starter-task`, `beginner-friendly`, `good-first-issue`, `e-easy`, `low-hanging-fruit`. | preferred |
| low_comment_density | Issue metadata -> `comments` count | Total comments <= 10. | preferred |

## Verdict rule

Accept if every `required` check passes. If any `required` check fails, the verdict is **reject**.

`preferred` checks never change the verdict; they are used only to rank accepted issues.

If evidence is insufficient, ambiguous, or missing for a `required` check, that check evaluates as `unclear`, which counts as **fail** and results in a **reject** verdict. **Exception:** `contribution_welcome` defaults to PASS when no gating language appears anywhere — absence of a policy statement is not unclear, it is welcome.