# Evidence Guide: where to find proof for each check

## The bundle: claim + repro report

When grading, you receive a markdown file with two sections:

```markdown
## Claim comment

<link to claim on GitHub>

[text of the claim comment pasted here]

## Repro report

<link to repro comment on GitHub>

[text of the repro report pasted here]
```

Both are plain text. Evidence comes from reading these sections.

---

## Where to look for each check

### `claim_names_issue`
**Location:** Claim comment body  
**What to look for:**  
- The issue number in the form `#42` or `#issue-42`
- OR the exact issue title mentioned (e.g. "add jest-axe accessibility tests")

**Pass condition:** Any mention of which specific issue the author is claiming. A claim that says "I'll work on this" without naming which issue fails.

---

### `claim_is_promise`
**Location:** Claim comment body  
**What to look for:**  
- Language: "I will", "I'll", "I plan to", "I'm going to", "I'll investigate"
- NOT: "I fixed", "I added", "I've completed", "done" (past tense = already did it)
- NOT: "I'll have this done by Friday" or "I'll fix it in 3 days" (no dates/promises of completion)

**Pass condition:** The claim uses future/investigation language ("I will report back", "I'll set up the environment and reproduce this"). Fails if it uses past tense or promises a fixed completion date.

---

### `claim_specifies_plan`
**Location:** Claim comment body  
**What to look for:**  
- Bullet points or numbered list of next steps
- Specific actions: "set up", "run", "test", "investigate", "document"
- NOT vague: "I'll look into this" or "I'll check it out" without saying what "checking" means

**Pass condition:** The claim lists 2+ concrete next steps. Examples:
- "1. Clone the repo and install dependencies. 2. Run the ReviewPage tests. 3. Document findings."
- "I'll set up jest-axe, run the tests, and report the accessibility violations."

Fails if it's vague ("I'll investigate") or just says "I'll do the work".

---

### `environment_documented`
**Location:** Repro report body  
**What to look for:**  
- Node version (e.g. "Node 18.x" or `node --version` output)
- npm version or package manager used
- Key dependencies (versions of jest, jest-axe, React, etc.)
- Setup commands run: `npm install`, `npm run build`, database migrations, environment variables, etc.
- The file path or directory structure used

**Pass condition:** A reader can follow the documented steps on their own machine and set up the same environment. Examples:
```
Node 18.17.0, npm 9.8.1
Ran: npm install
Installed: jest@29.7.0, jest-axe@8.0.0, @testing-library/react@14.0.0
```

Fails if environment is missing or only says "installed everything" without details.

---

### `steps_reproducible`
**Location:** Repro report body  
**What to look for:**  
- Numbered or bulleted steps
- Each step names the command, file, or action (e.g. `npm test`, `npm run lint`, open `ReviewPage.test.tsx`)
- Steps are in order and complete
- No jumps or missing context

**Pass condition:** A stranger can execute the steps in order and get the same result. Example:
```
1. npm run test -- ReviewPage.test.tsx
2. Observe test output
3. Check jest-axe violations reported
```

Fails if steps are vague ("run the tests"), skipped ("see earlier"), or command syntax is missing.

---

### `observed_behavior_clear`
**Location:** Repro report body  
**What to look for:**  
- Actual output: console logs, test output, error messages, screenshots
- Names the files or functions involved
- Describes state: "tests passed", "test failed with Error: ...", "ReviewPage component renders without violations"
- Uses quotes from actual output, not summaries

**Pass condition:** A reader can see exactly what happened. Example:
```
npm test -- ReviewPage.test.tsx

PASS src/pages/__tests__/ReviewPage.test.tsx
  ReviewPage
    ✓ renders (234 ms)
    ✓ navigation works (145 ms)

2 passed in 1.2s

jest-axe output showed 0 violations.
```

Fails if it only says "tests ran fine" without showing the actual output.

---

### `expected_vs_observed`
**Location:** Repro report body  
**What to look for:**  
- **For a task issue (like #42):**
  - Expected: "Current state has no accessibility tests checking X"
  - Observed: "After setting up the environment, ReviewPage.test.tsx does not include jest-axe checks"
  
- **For a bug issue:**
  - Expected: "The parser should handle a JSON array at the top level"
  - Observed: "Parser throws AttributeError when it encounters a top-level array"

**Pass condition:** The report explicitly states what the current state is vs. what needs to happen. Example:
```
**Current state:** ReviewPage tests check component rendering but do not validate accessibility (no jest-axe, no contrast checks, no label checks).

**What's needed:** Add jest-axe tests to check for contrast, missing labels, and heading structure.
```

Fails if it only shows what was observed, not why it matters or what should be different.

---

### `ai_disclosure_if_required`
**Location:** Repro report body; also check the repo's `docs/CONTRIBUTING.md` or README policy  
**What to look for:**  
- Does the repo's policy mention "AI-assisted" or "AI tools" or "disclose tool use"?
- If yes: Does the repro report mention that AI (Claude, ChatGPT, etc.) was used?
- If no policy mentioned: Pass by default.

**Pass condition:**  
- If repo policy **requires disclosure:** Report includes "I used AI (Claude) to help with investigation" or similar.
- If repo policy **does not mention disclosure:** Report passes regardless (silence is okay).

Fails only if repo requires disclosure and report does not mention it.

---

### `evidence_included` (preferred)
**Location:** Repro report body  
**What to look for:**  
- Console output (copy-pasted or screenshot)
- Test output (pass/fail, test names, durations)
- File excerpts (code showing the current state)
- Command output with actual data
- NOT just "tests passed" or "it works"

**Pass condition:** Report shows actual evidence the reader can see.

---

### `no_piggyback` (preferred)
**Location:** Repro report body; compare against other comments on the GitHub issue  
**What to look for:**  
- Is this the author's own investigation, with their own environment and steps?
- Does it say "same as X above" or "confirming what Y said"?
- Or does it describe the author's own reproduction?

**Pass condition:** Report uses the author's own words and describes their own work, even on a shared issue.

---

## Common pitfalls

| Mistake | Why it fails | Fix |
|---------|-------------|-----|
| "Claim: I'll work on this" (no issue number) | `claim_names_issue` fails | Add "#42" or the issue title |
| "Claim: I fixed the tests" (past tense) | `claim_is_promise` fails | Use "I will fix" or "I'll add" |
| "Claim: I'll investigate" (no plan) | `claim_specifies_plan` fails | List 2+ concrete steps |
| "Repro: Installed dependencies" (no versions) | `environment_documented` fails | Show `npm list` output or versions |
| "Repro: Run the tests" (no command) | `steps_reproducible` fails | Say `npm test -- ReviewPage.test.tsx` |
| "Repro: Tests passed" (no output shown) | `observed_behavior_clear` fails | Paste the actual test output |
| "Repro: This is a task that needs tests" (no state) | `expected_vs_observed` fails | Say "tests currently don't check X" |
| "Repro: Used Claude to write the investigation" (repo requires disclosure) | `ai_disclosure_if_required` fails | Add disclosure statement |
| "Same as #42, can confirm" | `no_piggyback` fails | Describe your own steps and findings |