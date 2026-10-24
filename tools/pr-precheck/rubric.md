# Rubric: is this PR ready to open?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| no_silent_drift | Diff vs plan vs description | Every change in diff is in plan or Deviations section. Description matches what diff actually does. No unrelated cleanup. | required |
| tested | test_evidence.md | Testing evidence shown (before/after output OR repo check results). Doesn't need every check, just proof it was tested. | required |
| description_complete | pr_draft.md | At least 3 of 4 key sections filled: Summary, Issue, Changes, Testing. Only 1 can be missing. | required |
| repo_conventions_followed | pr_draft.md read against repo-facts block (PR template requirements, contribution policy) | PR description addresses what the repo's PR template and contribution policy specifically require (e.g. checklist items, changelog entry, type annotations, whatsnew entry). FAIL if the repo-facts block names specific template requirements and the PR description ignores them entirely. PASS if the PR addresses or acknowledges the repo's stated requirements. | required |
| ai_disclosed | Anywhere in package | AI use mentioned somewhere. Any acknowledgment. | preferred |
| diff_clean | git diff main...HEAD | No debug lines, commented code, or unrelated edits. Only files the fix needs. | preferred |

## Verdict rule

Accept (ready) if every `required` check passes.

Reject (hold) if any `required` check is fail or unclear.

Unclear counts as fail.