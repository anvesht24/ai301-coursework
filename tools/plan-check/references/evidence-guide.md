# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:**
- In the plan file: the "Diagnosis" section
- On GitHub: the student's posted repro comment from unit 2 (the proof they posted on the issue)
- Compare the two: does the plan's diagnosis match what the repro actually showed?

**What good looks like:**
- The diagnosis states exactly what behavior the repro evidence showed
- It identifies the root cause that would explain that behavior
- It does not contradict the repro evidence
- Example: Repro shows "ReviewPage tests exist but don't check accessibility" → Diagnosis says "Current state: tests exist but have no jest-axe checks"

---

## Scope

**Where it lives:**
- In the plan file: the "Scope" section or "Scope statement"
- Look for explicit "WILL" and "WON'T" language

**What good looks like:**
- Clear boundary: "I WILL add jest-axe tests. I WON'T refactor existing tests."
- Specific areas named (not just "improve things")
- Reader knows exactly what will and won't change
- Example good: "Will add 1 new test to ReviewPage.test.tsx checking contrast, labels, headings. Won't modify ReviewPage component itself."
- Example bad: "Will improve accessibility testing."

---

## Executability

**Where it lives:**
- In the plan file: the "Approach" or "Implementation" section
- Look for numbered steps with specific commands or file names

**What good looks like:**
- Each step names the actual command (`npm install jest-axe`, `npm test`, etc.)
- Each step names the file (`ReviewPage.test.tsx`, not just "test file")
- Steps are in order and someone could follow them without asking
- Example good: "1. npm install jest-axe. 2. Import { axe, toHaveNoViolations } in ReviewPage.test.tsx. 3. Add test function. 4. Run npm test."
- Example bad: "Add jest-axe and write tests."

---

## Test plan

**Where it lives:**
- In the plan file: the "Test Plan" section
- Compare to the repro evidence: the student's unit 2 repro steps

**What good looks like:**
- States what will be run to verify the fix (the command)
- States what the current behavior is (before fix)
- States what the expected behavior is (after fix)
- Tied to the repro: uses the same reproduction steps or similar verification
- Example good: "Before: npm test ReviewPage.test.tsx → 3 tests pass (no jest-axe checks). After: npm test ReviewPage.test.tsx → 4 tests pass (new jest-axe test passes)."
- Example bad: "I'll test it and make sure it works."

---

## Honesty

**Where it lives:**
- In the plan file: the "Risks", "Unknowns", or "Challenges" section
- Also in any caveats or assumptions in other sections

**What good looks like:**
- Names specific, genuine risks (not generic "might be hard")
- Related to THIS fix, not generic software risks
- Acknowledges what the student is unsure about
- Example good: "Jest-axe might find existing accessibility violations in ReviewPage that I'll need to fix first" or "I haven't used jest-axe before, so I may need to read the docs"
- Example bad: "Might encounter bugs" or no risks section at all

---

## Comms (thread-aware)

**Where it lives:**
- The plan comment (what will be posted on GitHub)
- The issue thread (are there existing plans, maintainer hints, or conventions?)
- The repo's CONTRIBUTING.md or README

**What good looks like:**
- Plan comment names the issue and describes the approach in plain language
- Comment is honest and uses future tense ("I will", "I'll")
- Comment is the student's own words, not copied from a classmate
- If repo requires AI disclosure, it's mentioned
- Example good: "I'll add jest-axe accessibility tests to ReviewPage.test.tsx, checking for contrast, label, and heading violations. I'll report back with my findings."
- Example bad: "Same approach as above" or "Fixing accessibility tests" (no approach stated)