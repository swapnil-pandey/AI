---
name: review-changes
description: Review committed and uncommitted changes on the current branch against an optional base branch. Invoke with /change-review [base-branch]; defaults to master.
disable-model-invocation: true
---

# Change review

Review only. Do not edit files, commit, reset, switch branches, push, build, or run tests.

Use the base branch supplied as `$ARGUMENTS`; if none is supplied, use `master`.

1. Verify the base branch resolves to a commit. If it does not, stop and ask for a valid base branch.
2. Find the merge base between the base branch and `HEAD`.
3. Review these three non-overlapping change sets:
   - Committed branch changes: `git diff <merge-base> HEAD`
   - Staged changes: `git diff --cached`
   - Unstaged changes: `git diff`
4. Use `git status --short` to state the reviewed scope.
5. Report only actionable findings, ordered by severity:
   - `Critical`, `High`, `Medium`, `Low`
   - Include file and line reference where possible.
   - Explain the impact and give the smallest practical fix.
6. End with a short summary of reviewed changes. If there are no findings, state that clearly and mention remaining review limitations.
