# Procedure: grade a PR package

## Read order

1. Read the issue context section (understand the issue)
2. Read the plan section (understand what was promised)
3. Read the test evidence section (what testing happened)
4. Read the PR draft section (the title, description, all fields)
5. Read the diff section (what actually changed)

## Evidence gathering

### For no_silent_drift check:

1. In the diff section, list every file that changed and every function/section modified
2. In the plan section, find the "Approach" subsection
3. For EACH change in the diff, search the plan for that change
4. Record: is every change mentioned in plan Approach OR in plan Deviations?
5. In PR draft, find Summary section
6. Record: does Summary describe what the diff actually does?

### For tested check:

1. Find the "test_evidence.md" or "Testing" section in the package
2. Look for "Before:" section with repro output
3. Look for "After:" section with repro output showing fix working
4. Look for any of: "make test-unit", "make lint", "make typecheck" with results
5. Record: is SOMETHING shown? Before output + after? OR check results?
6. PASS if at least before/after OR at least one check result shown
### For description_complete check:

1. In PR draft section, read the entire PR template 
2. Record: does it have at least 3 of these 4 sections filled?
   - Summary (what changed)
   - Issue (issue number)
   - Changes (bullet list)  
   - Testing (results)
3. PASS if 3 or more are filled (max 1 missing)

### For ai_disclosed check:

1. Combine ALL text sections into one string: issue + plan + diff + test_evidence + pr_draft
2. Search the combined text for ANY of these terms:
   "AI", "ML", "LLM", "GPT", "Claude", "Anthropic", "OpenAI", "assistant", "help", "tool", "consult", "document", "source", "generat", "suggest", "recommend"
3. Record: were ANY of those terms found ANYWHERE in the combined text? Even one match counts.
4. If NOTHING relevant found, manually skim all text sections one last time for ANY hint of tools/assistance/docs
5. PASS if ANYTHING relevant found in combined search OR manual skim. Only FAIL if nothing found after searching AND skimming.

### For repo_conventions_followed check:

1. In repo-facts block, find "pull requests:" and "contribution policy:" lines
2. Record: what does the repo specifically require? (checklist items, changelog, type annotations, whatsnew, etc.)
3. In PR draft, search for evidence that those requirements are addressed
4. PASS if the PR description addresses the repo's stated requirements (mentions the checklist items, includes required entries)
5. FAIL if the repo names specific requirements and the PR completely ignores them

### For diff_clean check:

1. Read the diff section line by line
2. Look for: console.log, print, debug, commented-out code (// or /* */)
3. Look for: unrelated file changes not in plan
4. Record: any of these found?

## Check execution (run in this order)

1. **no_silent_drift**: PASS if every diff change is in plan OR Deviations, AND description matches diff
2. **tested**: PASS if test evidence shown (before/after OR check results)
3. **description_complete**: PASS if Summary, Issue, Changes, Testing all filled
4. **ai_disclosed**: PASS if AI mentioned somewhere in PR
5. **diff_clean**: PASS if no debris found

## Verdict assembly

1. Count required checks that PASS vs FAIL/UNCLEAR
2. If ANY required is FAIL/UNCLEAR → verdict = reject
3. Else → verdict = accept
4. Quote the deciding evidence in each check's evidence field