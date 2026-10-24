# Evidence guide: where evidence lives

## no_silent_drift evidence

**In practice package:**
- Diff section lists all changed files and changed lines
- Plan section has Approach subsection listing what will change
- Plan section has Deviations subsection (if any changes from plan)
- PR draft Summary says what changed

**What good looks like:**
Every line in diff is explained in plan Approach OR Deviations.
Summary describes exactly what diff shows.
No random unrelated files changed.

---

## tested evidence

**In practice package:**
- test_evidence.md section with "Before:" and "After:" headers
- OR results of "make test-unit", "make lint", "make typecheck"
- Actual command output pasted

**What good looks like:**
Before output shows original problem.
After output shows problem fixed.
OR check commands run with actual results (pass/fail shown).
Not just "tested it" with no output.

---

## description_complete evidence

**In practice package:**
- PR draft section with template sections
- Look for: Summary, Issue, Changes, Testing, Screenshots, Notes

**What good looks like:**
Summary: describes what change does (not empty, not "TBD")
Issue: has "Closes #42" or issue number
Changes: has bullet list of actual changes
Testing: has checkboxes marked and results pasted
Notes: has AI disclosure

---
## ai_disclosed evidence

**In practice package:** 
- Anywhere at all in the text

**What good looks like:**
ANYTHING hinting a tool was used or help was gotten:
"used a tool", "an assistant helped", "consulted the docs", "looked at source code"
Literally any mention of not doing it alone with no help.

---

## diff_clean evidence

**In practice package:**
- Diff section showing all changes

**What good looks like:**
No console.log, print, debug statements.
No commented-out code.
No unrelated cleanup.
Only files needed for fix.