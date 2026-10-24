# Unit 4 — Test and Submit

## PR link

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/239

## Branch

fix/42-jest-axe-tests

## Run history

First full run: 13/20 agreement
Second full run: 14/20 agreement
Third full run: 18/20 (category floor unmet: standards-wall 0/2)
Final full run: 20/20 agreement (PASS)

## Package analysis

pkg-02 (clear-accept): My rubric accepted it, gold label accepted it. PR had clear description matching diff, testing evidence shown, all template sections filled, and repo conventions followed (CHANGELOG entry added as repo requires). All required checks passed.

## Check rationale

"repo_conventions_followed | pr_draft.md read against repo-facts block (PR template requirements, contribution policy) | PR description addresses what the repo's PR template and contribution policy specifically require. FAIL if the repo-facts block names specific template requirements and the PR description ignores them entirely. PASS if the PR addresses or acknowledges the repo's stated requirements."

Added this check after standards-wall packages were incorrectly accepted. These PRs skip repo-specific requirements (like whatsnew entries or checklists). This check catches PRs that ignore what the repo explicitly asks for.

## Trade-offs

Making ai_disclosed preferred instead of required means PRs without AI disclosure can still be accepted. This was necessary because clear-accept packages don't all have explicit AI mentions, but the trade-off is that a PR missing disclosure won't be flagged. The repo_conventions_followed check compensates by catching PRs that skip repo-specific requirements.
