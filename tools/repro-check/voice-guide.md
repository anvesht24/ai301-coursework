# Voice guide: how I talk upstream

# Voice Guide: how to write claim and repro comments

## Overview

This is not a checklist of what to say. It's how to say it — the tone, structure, and habits that make a claim and a repro report feel professional, honest, and clear.

**Core principle:** You are promising investigation and evidence, not a fix.

---

## Part 1: The Claim Comment

### What a claim is

A claim comment goes up **before you reproduce**. It is short and names your issue, what you will do, and that you will report back. It's a promise, not a report.

### Structure

```
I'll work on [issue name/number].

Here's what I'll do:
1. [First concrete step]
2. [Second concrete step]
3. [Third concrete step: will report back]

Investigating now.
```

### Voice

- **Promise, don't assert.** "I will investigate" not "I found the bug" or "I fixed it".
- **Specific, not vague.** "Set up jest-axe and run the tests" not "I'll look into it".
- **Short.** 3-5 sentences or a short bullet list. The proof comes in the repro report.
- **Professional.** You are a peer contributor. Be clear and courteous.

### Good example (for issue #42)

```
I'll work on #42: add jest-axe accessibility tests for the review page.

Here's my plan:
1. Set up the project environment and review the existing ReviewPage tests
2. Install jest-axe and configure it in the test suite
3. Run the tests to identify accessibility issues (contrast, labels, heading structure)
4. Post a reproduction report with my findings

I'll report back soon.
```

### What to avoid

❌ **"I fixed the accessibility tests."** (Past tense; says you're done before you start.)

❌ **"I'll fix this in 3 days."** (Commits to a date; repro might take longer or be impossible.)

❌ **"I'll work on this issue."** (No issue name; maintainers can't tell which one.)

❌ **"I'll investigate and do whatever is needed."** (Vague; maintainers can't tell your plan.)

❌ **"Same as #42, can confirm."** (Piggyback; write your own plan even on a shared issue.)

---

## Part 2: The Repro Report

### What a repro report is

A repro report goes up **after you reproduce**. It documents what you did, the environment, the steps, and what you found. A stranger should be able to follow it.

### Structure

```markdown
### Reproduction Report

**Environment:**
[Node, npm, key dependencies, setup commands]

**Steps to reproduce:**
1. [First step with command/file]
2. [Second step with command/file]
3. [Third step with command/file]

**Observed behavior:**
[What actually happened, with console output/evidence]

**Expected behavior / Next steps:**
[What should happen OR what needs to be done]

**Evidence:**
[Console output, test results, screenshots, or file excerpts]
```

### Voice

- **Evidence first.** Show what you saw: output, logs, screenshots, file state.
- **Numbered steps.** A reader should be able to follow them in order on their own machine.
- **Honest about blockers.** If you couldn't reproduce, say so with evidence. "I followed steps 1-3 but step 4 failed with error: X" is a valid repro.
- **Your own words.** Even on a shared issue, describe your own investigation.
- **Clear, not fancy.** Use code blocks for commands and output. Name files and functions.

### Good example (for issue #42, a task issue)

```markdown
### Reproduction Report

**Environment:**
```
Node v18.17.0
npm 9.8.1
jest 29.7.0
jest-axe 8.0.0
@testing-library/react 14.0.0
@testing-library/jest-dom 6.1.4
```

Setup: cloned repo, ran `npm install`, no errors.
```

**Steps to reproduce:**
1. Navigate to the project root
2. Run `npm test -- ReviewPage.test.tsx` to see the current tests
3. Check `frontend/src/pages/__tests__/ReviewPage.test.tsx` to see what accessibility tests exist
4. Install jest-axe: `npm install --save-dev jest-axe` (if not already installed)
5. Review jest-axe docs to understand contrast, label, and heading checks

**Observed behavior:**

Current tests pass but do not include accessibility checks:
```
PASS src/pages/__tests__/ReviewPage.test.tsx
  ReviewPage
    ✓ renders without crashing (234 ms)
    ✓ navigation buttons work (145 ms)
    ✓ form submission works (189 ms)

Test Suites: 1 passed, 1 total
Tests: 3 passed, 3 total
```

The test file does not import jest-axe or run any accessibility validation.

**Expected behavior / Next steps:**

After this issue is fixed, the test file should:
- Import jest-axe
- Run `axe()` validation on the rendered ReviewPage component
- Check for: color contrast violations, missing form labels, incorrect heading hierarchy
- Fail the test if violations are found

Example of what the check should look like:
```javascript
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

test('ReviewPage has no accessibility violations', async () => {
  const { container } = render(<ReviewPage {...props} />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

**Evidence:**

Current ReviewPage test file (excerpt):
```javascript
// frontend/src/pages/__tests__/ReviewPage.test.tsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import ReviewPage from '../ReviewPage';

describe('ReviewPage', () => {
  it('renders without crashing', () => {
    render(<ReviewPage />);
    expect(screen.getByRole('heading', { name: /reviews/i })).toBeInTheDocument();
  });
});
```

No jest-axe imports or calls.

---
```

### What to avoid

❌ **"I ran the tests and they passed."** (No evidence; what tests? What output?)

❌ **"Same as #69, can confirm it's broken."** (Piggyback; describe your own investigation.)

❌ **"The issue is clear from the code."** (Show the code, don't just say it's clear.)

❌ **"I fixed this already."** (This is a repro report, not a fix. You're documenting the current state, not changing it.)

❌ **"Unable to reproduce but I'll try harder next time."** (Still honest, but show what you tried. "I cloned the repo, ran step 1-4, but step 5 failed with error X" is better.)

---

## Part 3: Tone across both comments

### Be professional
- Use full sentences, not slang.
- "I'll investigate" not "I'mma look into this".
- "Set up the environment" not "get the env set up lol".

### Be honest
- If you used AI to help with the investigation, say so (if the repo requires it).
- If you couldn't reproduce, say that with evidence.
- If you're blocked, explain why.

### Be specific
- Name the files: `ReviewPage.test.tsx`, not "the test file".
- Name the commands: `npm test -- ReviewPage.test.tsx`, not "run the tests".
- Quote output: show what you saw, don't summarize it.

### Be concise
- Claim: 3-5 sentences + a short plan.
- Repro: Long enough to be clear, short enough to skim.
- No marketing language, no flowery prose.

### Be kind
- You're a peer, not a customer complaining.
- Maintainers are volunteers. Help them help you by being clear.
- "I found a potential issue" not "this code is broken and nobody noticed".

---

## Checklist for your comments

### Before posting your claim:
- [ ] Claim names the issue (#42 or "add jest-axe tests")
- [ ] Claim uses future language ("I will", "I'll")
- [ ] Claim lists 2+ concrete next steps
- [ ] Claim promises to report back
- [ ] No promised dates or fixes, just investigation
- [ ] 3-5 sentences, easy to skim

### Before posting your repro:
- [ ] Environment is documented (Node, npm, dependencies, setup)
- [ ] Steps are numbered and use actual commands/file names
- [ ] Observed behavior shows actual output (copy-pasted, not summarized)
- [ ] Expected behavior / next steps explains what comes next
- [ ] Evidence includes console output, test results, or code snippets
- [ ] Written in your own words, even on a shared issue
- [ ] If repo requires AI disclosure, it's mentioned

---

## Example: Full claim + repro for issue #42

### Claim comment (posted first)

```
I'll work on #42: add jest-axe accessibility tests for the review page.

Here's my plan:
1. Set up the project environment and review the existing ReviewPage tests
2. Install jest-axe and identify the accessibility checks needed (contrast, labels, headings)
3. Document the current test setup and what jest-axe checks would catch
4. Post a reproduction report with my findings

Investigating now.
```

### Repro comment (posted after you reproduce)

```
### Reproduction Report

**Environment:**
```
Node v18.17.0
npm 9.8.1
jest 29.7.0
jest-axe 8.0.0
```
Cloned repo, ran `npm install`, no errors.

**Steps to reproduce:**
1. Run `npm test -- ReviewPage.test.tsx` to see current tests
2. Check `frontend/src/pages/__tests__/ReviewPage.test.tsx`
3. Note: no jest-axe imports or calls

**Observed behavior:**
Tests pass (3/3) but do not include accessibility checks:
```
PASS src/pages/__tests__/ReviewPage.test.tsx
  ReviewPage
    ✓ renders without crashing (234 ms)
    ✓ navigation buttons work (145 ms)
    ✓ form submission works (189 ms)
Tests: 3 passed, 3 total
```

**Expected behavior / Next steps:**
Once this issue is resolved, the tests should:
- Import jest-axe
- Run accessibility checks on contrast, form labels, heading hierarchy
- Example pattern:
```javascript
import { axe, toHaveNoViolations } from 'jest-axe';
expect.extend(toHaveNoViolations);

test('ReviewPage has no accessibility violations', async () => {
  const { container } = render(<ReviewPage {...props} />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

**Evidence:**
Current test file does not include jest-axe:
```javascript
import React from 'react';
import { render, screen } from '@testing-library/react';
import ReviewPage from '../ReviewPage';

describe('ReviewPage', () => {
  it('renders without crashing', () => {
    render(<ReviewPage />);
    expect(screen.getByRole('heading')).toBeInTheDocument();
  });
});
```
```

---

That's the voice. Now go use it!