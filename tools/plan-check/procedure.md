# Procedure: how to grade a plan package

## Read order

1. Read the issue context first (understand what issue this plan is for)
2. Read the repro evidence second (understand what behavior the issue shows)
3. Read the plan and plan comment last (see what they're proposing to fix)

Why: You can't judge if a plan is grounded without knowing what it's grounding itself in.

## Evidence gathering

For each evidence family, gather this:

**Diagnosis evidence:**
1. Find the Diagnosis section in the plan (or where diagnosis is stated)
2. Find the repro evidence on GitHub (the student's unit 2 repro comment)
3. Record: What does the repro evidence actually show happened?
4. Record: What does the plan say is wrong?
5. Check: Does the plan's diagnosis match what the repro showed?

**Scope evidence:**
1. Find the Scope section OR any statement about what will/won't change
2. Record: What does the plan say it will modify?
3. Record: What does it say it won't modify?
4. Scope can be in a dedicated section OR clear from the approach

**Files evidence:**
1. Find mention of specific files (in Approach, Files section, or anywhere)
2. Record: Are actual file paths or file names listed?
3. Files can be mentioned in approach steps, not just in a dedicated section

**Approach evidence:**
1. Find the Approach section (or where implementation steps are described)
2. Record: Can a reader follow the steps to implement?
3. Approach can be numbered steps OR clear prose description
4. Does NOT need perfect formatting, just needs to be followable

**Test plan evidence:**
1. Find the Test Plan section
2. Record: What will be run to verify?
3. Record: What before/after behavior is expected?
4. Should relate to verifying the fix works

**Risks evidence:**
1. Look ANYWHERE in the plan for risk/unknown mentions (Risks section, Approach, Unknowns, or embedded)
2. Record: Are specific, genuine risks mentioned?
3. Risks do NOT need a dedicated section - can be mentioned anywhere

## Check execution

Run checks in this order:

1. **diagnosis_grounded**
   - Look at diagnosis evidence gathered above
   - PASS if: diagnosis matches what repro evidence shows AND explains the root cause
   - FAIL if: diagnosis contradicts the repro evidence OR is too vague

2. **scope_bounded**
   - Look at scope evidence gathered above
   - PASS if: explicit will/won't statements with specific areas
   - FAIL if: vague or missing scope boundaries

3. **files_specific**
   - Look at files evidence gathered above
   - PASS if: actual file paths listed (not categories)
   - FAIL if: only vague references like "test files"

4. **approach_executable**
   - Look at approach evidence gathered above
   - PASS if: numbered steps with specific commands/files
   - FAIL if: too vague or missing step details

5. **test_plan_decisive**
   - Look at test plan evidence gathered above
   - PASS if: shows before/after AND tied to repro steps
   - FAIL if: vague or doesn't connect to repro

6. **risks_acknowledged**
   - Look at risks evidence gathered above
   - PASS if: at least one specific, genuine risk mentioned
   - FAIL if: no risks mentioned OR only generic "might be hard"

## Verdict assembly

1. Count the checks:
   - If ANY required check is FAIL or UNCLEAR → verdict = **REJECT** (hold)
   - If ALL required checks are PASS → verdict = **ACCEPT** (ready)

2. State which check decided the verdict:
   - If rejecting: name the check that failed
   - If accepting: confirm all checks passed

3. Output the verdict as `accept` or `reject` in the JSON block