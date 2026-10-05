# Unit 2: Claim and Reproduce

## Claim comment

**Link:** https://github.com/codepath/pathreview-ai301-fa26-s1/issues/42

I'll work on #42: add jest-axe accessibility tests for the review page.

Here's my plan:
1. Set up the project environment and review the existing ReviewPage tests
2. Install jest-axe and understand what accessibility checks it provides
3. Document the current test setup and identify what jest-axe checks are needed
4. Post a reproduction report with my findings

Investigating now.

---

## Repro report

**Link:** https://github.com/codepath/pathreview-ai301-fa26-s1/issues/42

### Reproduction Report

**Environment:**
Node v24.11.0
npm 11.6.1
vitest 1.6.1
jest-axe not installed

Setup: Cloned fork of pathreview-ai301-fa26-s1, ran `npm install` in frontend folder, no errors.

**Steps to reproduce:**
1. Navigate to frontend directory
2. Run `npm test -- ReviewPage.test.tsx`
3. Check src/pages/ for ReviewPage component and tests

**Observed behavior:**

ReviewPage component exists but test file does not exist. The __tests__ folder doesn't exist.

Running the test command returns:
```
No test files found, exiting with code 1
```

**Expected behavior / Next steps:**

Once this issue is fixed, there should be a test file with jest-axe checks for:
- Color contrast
- Form labels
- Heading structure

**Evidence:**

ReviewPage component exists at `src/pages/ReviewPage.tsx` but has no corresponding test file.

---

## Run history

I ran the full eval harness on 20 packages and achieved 20/20 agreement. The key was loosening the claim checks to focus on whether the plan was understandable rather than perfectly structured. The `claim_names_issue` check now allows any reference to the issue (number, title, or context), and `claim_specifies_plan` accepts prose plans, not just numbered lists. After fixing these two checks, I ran canary tests on 5 packages from different categories to ensure the loosened checks didn't break previous agreements, then did a full run and got perfect agreement.

---

## Package analysis

From eval-run.txt, I analyzed pkg-12.

**My rubric's verdict:** accept

**Gold label verdict:** accept

**Why it passed:** Package pkg-12 had a claim that clearly named the issue, used future language ("I will investigate"), and listed specific next steps. The repro report documented the environment, showed actual command output, and explained what was expected vs. observed. All required checks passed.

---

## Check rationale

My `environment_documented` check reads:

"Report documents the environment setup: which Node version, npm version, key dependencies installed, and commands run to prepare (e.g. `npm install`, build steps, setup scripts). A reader could follow these steps."

This check matters because someone else needs to be able to reproduce your setup on their machine. If you only say "I installed dependencies" without versions or the actual commands, they can't follow your steps. My check focuses on whether a reader could recreate the exact environment, not on exhaustive detail — Node version, npm version, and the setup commands are enough.

---

## Trade-offs

I focused the rubric on what a claim and repro report actually need: proof that you did the work and clear steps someone else could follow. I didn't add checks for politeness or writing style, even though the voice guide emphasizes those. I also kept the AI disclosure check as a defaults-to-pass rule (silence is okay if the repo doesn't require it), which means some borderline cases might slip through — but I prioritized avoiding false positives over catching every edge case.
