# Rubric: is this reproduction package ready to post?


## Checks
 
| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| claim_names_issue | Claim comment body | Claim comment references the issue in some way (issue number, title, or clear context that makes which issue is being claimed obvious). NOT vague like "I'll work on this" with no context. | required |
| claim_is_promise | Claim comment body | Claim comment uses language of promise and investigation ("I will", "I'll", "I plan to", "I'll report back"), NOT assertions or completed work ("I fixed", "I added", "done"). No promised dates or "I'll fix it in X days". | required |
| claim_specifies_plan | Claim comment body | Claim comment indicates what the author will investigate or do next. Can be bullets, numbered, or prose ("I'll set up the environment and run the tests"). Does NOT need to be a detailed plan, just shows intent. | required |
| environment_documented | Repro report body | Report documents the environment setup: which Node version, npm version, key dependencies installed, and commands run to prepare (e.g. `npm install`, build steps, setup scripts). A reader could follow these steps. | required |
| steps_reproducible | Repro report body | Report gives numbered or clear steps to reproduce that name the files or commands involved. A reader could follow the major steps, even if some details are implicit. | required |
| expected_vs_observed | Repro report body | Report explains what was expected vs. what was observed. For a task issue (like adding tests), this is "tests currently do not check X" vs. "after this we should check Y". For a bug, it's the symptom vs. expected behavior. | required |
| ai_disclosure_if_required | Repro report body; repo's CONTRIBUTING.md policy | If the repo's stated policy requires disclosing AI assistance in the PR/commit, the repro report mentions that AI was used in the investigation. If the policy does not require disclosure, this check passes by default (silence = okay). | required |
| evidence_included | Repro report body | Report includes evidence: console output, test output, file excerpts, or screenshots showing the observed behavior. Not just "it works" or "tests passed", but actual output the reader can see. | preferred |
| no_piggyback | Repro report body; check against prior comments on issue | Report is written in the author's own words and describes their own investigation/setup, even on a shared issue. Does not say "same as X above" or "can confirm what Y said". | preferred |
 
## Verdict rule
 
Accept if every `required` check passes. If any `required` check fails, the verdict is **reject**.
 
`preferred` checks never change the verdict; they rank accepted reports.
 
If evidence is insufficient, ambiguous, or missing for any `required` check, that check evaluates as `unclear`, which counts as **fail** and results in a **reject** verdict. **Exception:** `ai_disclosure_if_required` defaults to PASS when the repo's policy does not mention AI disclosure — absence of a policy is not unclear, it is okay.