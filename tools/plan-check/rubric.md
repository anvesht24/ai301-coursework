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
| diagnosis_grounded | Plan → Diagnosis section, read against repro evidence | Diagnosis clearly states what the current problem is (what works now, what doesn't). It is grounded in specific behavior from the repro evidence, not contradicting it. Example: "Tests exist but don't check X" (backed by repro showing no X checks). | required |
| scope_bounded | Plan → Scope section or any clear statement about boundaries | Scope clearly states what WILL be changed and what WON'T be changed. Can be explicit "will/won't" statements or clear enough from context that reader knows the boundaries. Example: "Add jest-axe tests. Won't refactor existing tests." | required |
| files_specific | Plan → Approach, Files section, or any mention of files | Plan mentions specific file paths or files to be touched somewhere in the plan (in approach, files section, or context). Not just "test files" but actual paths or clear file references. Can be mentioned in approach steps. | required |
| approach_executable | Plan → Approach section | Approach describes the steps to implement the fix in a way a reader could follow. Does not need perfect numbered lists, but should be clear enough that someone could start executing. Examples: step-by-step commands, or prose describing implementation order. | required |
| test_plan_decisive | Plan → Test Plan section, read against repro steps | Test plan shows how to verify the fix works. States what you'll run and what you expect to see before/after. Does not need to be identical to repro steps but should be tied to verifying the fix. | required |
| risks_acknowledged | Plan → anywhere (Risks, Approach, Unknowns sections, or mentioned in context) | Plan acknowledges at least one genuine risk or unknown related to this fix, even if not in a dedicated section. Example: "Jest-axe might find existing violations" or "I haven't used this library before". | required |

## Verdict rule

Accept (ready) if every `required` check passes. If any `required` check fails, the verdict is **reject** (hold).

If evidence is insufficient or missing for any `required` check, that check evaluates as `unclear`, which counts as **fail** and results in a **reject** verdict.