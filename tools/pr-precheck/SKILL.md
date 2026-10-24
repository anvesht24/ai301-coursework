---
name: pr-precheck
description: Grade a pull request against its plan. Ready to open?
---

# pr-precheck: grade a PR package

You are grading: is this PR ready to open?

A package is: issue context + plan + PR draft (title/description) + test evidence + diff.

## Your job

Execute the procedure in procedure.md exactly as written.
Apply the rubric in rubric.md.
Use evidence-guide.md to find where evidence lives.

## Modes

**Live mode:** Read your own PR's files (plan.md, pr_draft.md, test_evidence.md), its diff (git diff main...HEAD), the issue thread, the repo's CONTRIBUTING.md.

**Eval mode:** Read ONLY the practice package bundle text. Do not fetch anything.

## Output

Always emit this and nothing else after it:

```json
{
  "item": "package-id",
  "checks": [
    {"name": "check-name", "grade": "pass|fail|unclear", "evidence": "one sentence"}
  ],
  "verdict": "accept|reject"
}
```

Verdict rule: if any required check is fail or unclear → reject. Else accept.

## Grading discipline

- Find evidence FIRST. Never grade without naming the fact that decided it.
- Grade the thing itself, not the formatting.
- The procedure decides how, not you. Follow it exactly.
- If evidence is missing entirely, that check is unclear (treat as fail).