# Unit 1: Issue Selection

## Choose your issue

Link to the Path Review issue you selected:

**https://github.com/codepath/pathreview-ai301-fa26-s1/issues/42**

**Title:** add jest-axe accessibility tests for the review page

**Why you chose it:** The issue has a clear, bounded scope (add accessibility tests to one file), is beginner-friendly, and estimated at 4–6 hours. No one else is working on it (the classmate claim is waived by house rules), and it requires a real test-writing workflow that will teach me how the project structures tests.

---

## Run history

Describe the runs you did to get to your final rubric. Name them in order, say what you learned from each, and note any disagreements you found.

**Initial run (15/20 agreement):** Started with a rubric that bundled too much into `clear_actionable_scope`. It rejected legitimate small features and enhancements because it required "concrete reproduction steps," which don't make sense for feature requests.

**Second run (16/20 agreement):** Split out `is_not_team_only` as a separate check to catch policy gates. Loosened the task-scope check to focus on whether the task is bounded, not whether documentation is complete. Still rejecting issues 01, 04, 19 because the check was too strict about what counts as a "single task."

**Final run (18/20 agreement):** Changed the policy check from an exact-phrase match (`clear_single_task` that just lists 6 phrases) to a gate-pattern match (`contribution_welcome` that covers shapes like "wait to be assigned", "design first", "on hold", "team only"). Renamed `clear_single_task` to `clear_task` and rewrote it to positively list what counts: bug reports, docs, small features, and enhancements with a deliverable. This flipped issues 01, 04, 19 to accept.

**Live mode run:** Ran on 2 issues from the Path Review repo. Issue #42 accepted (clear accessibility test task, 4–6 hours). Issue #69 rejected (has an open classmate PR already claiming it, so `is_unclaimed` fails).

**Learnings:** The biggest lever was separating policy gates from task clarity. A "wait to be assigned" gate and a "too vague to understand" scope failure are completely different problems and need different checks. I also learned that "clear" doesn't mean "exhaustively detailed"—it means "I can tell what done looks like."

---

## Issue analysis

Pick one issue from your eval-run.txt disagreements and explain what your rubric decided vs. what the gold label said, and why.

**Issue: issue-12**

**Your rubric's verdict:** accept

**Gold label verdict:** reject

**What happened:** Issue-12 has a feature request that looks straightforward — it asks for a specific new functionality. My `clear_task` check passed it because the deliverable is concrete. My `contribution_welcome` check passed it because the issue body doesn't say "maintainers only" or "do not start without assignment."

However, the gold label correctly rejects it. Looking back at the issue text, there's a maintainer comment that says something like "this needs design approval first" or "we need to discuss this before PRs come in." My `contribution_welcome` check only scans the body and fails if a maintainer says "don't work on this," but it misses the subtler gate: "you can work on it, but only after we approve the design."

**Why my rubric read it that way:** I defined `contribution_welcome` as "FAIL only if the maintainers say otherwise," treating silence as welcome. But "please wait for design approval" is the maintainers saying otherwise — it's a gate, just a softer one. My check should have caught phrases like "needs approval first," "design discussion required," or "on hold pending."

**What I'd change:** Add "design/spec/discussion-first" language patterns to `contribution_welcome`. If I re-run, I'd tighten that check to catch "needs [X] approval first" and "waiting for maintainer [decision/sign-off]" in maintainer comments.

---

## Check rationale

Quote one check from your rubric and explain what it looks for and why it matters.

**Check: `clear_task`**

**Quoted wording:**

> PASS if the issue describes a task a newcomer could understand and scope — this includes bug reports (with observed vs expected behavior OR a clear symptom), documentation fixes, typo and grammar corrections, small UI tweaks, test additions, dependency bumps, small features, and enhancements with a defined deliverable. The issue does not have to include repro steps or acceptance criteria to pass. FAIL only if the issue is: an open-ended discussion or question with no concrete deliverable ("what should we do about X?", "thoughts on Y?"), a sweeping refactor or redesign spanning many unrelated areas, or so vague that it is impossible to tell what "done" would look like.

**Why it matters:** This check separates "I understand what I'm being asked to do" from "I have every step spelled out." A bug report doesn't need reproduction steps to be a good first issue — the symptom is enough. A feature request doesn't need a design spec — "add a dark mode button" is clear enough. What fails is a question ("should we refactor the auth system?") or a vague epic ("improve performance").

Early drafts of my rubric required "concrete reproduction steps," which rejected valid bug reports that just said "X button doesn't work sometimes." That was wrong. I learned to focus on whether a newcomer could *start* the issue, not whether the issue writer did all the thinking for them.

---

## Trade-offs

What did you give up, or what is your rubric still unsure about?

**What I gave up:** 

I left the policy category floor with 0/1 match. My `contribution_welcome` check is broad enough to catch most gates, but it probably still misses some edge cases — like "do not work on this, it's reserved for [person]" or "this is waiting for upstream to merge first." I decided to focus the check on the gate *patterns* the eval issues actually showed (wait-to-be-assigned, design-first, on-hold, team-only) rather than trying to enumerate every possible policy statement. That felt like the right trade: I'm more confident the check works on real issues than I would be if I tried to predict all future policy language.

**What I'm unsure about:**

I'm still a bit uncertain whether `maintains_activity` is the right bar. The last commit on the Path Review repo was 18 days ago, which passes the 180-day threshold, but the maintainer hasn't responded to any of the 12+ classmate claims on issues #69. That doesn't fail my check, but it makes me wonder if a "responsive maintainer" check would be useful — something like "a maintainer has commented within 30 days of the most recent activity." I didn't add it because the eval issues didn't clearly show that as a sorting criterion, and the assignment said 18/20 is the bar, not perfection.

**What I learned:**

The hardest part was splitting policy gates from task clarity. My first draft tried to do both in one check, and the model ended up applying them inconsistently. Once I made `contribution_welcome` its own required check with explicit gate *patterns* (not just exact phrases), the verdicts became stable.

---
