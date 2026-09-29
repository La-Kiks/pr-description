---
name: pr-description
description: Writes a pull request title and description from the branch diff, using the PR template. Use when opening a PR, running gh pr create, or when asked to write or update a PR description.
---

# PR description

1. Pick the template. If the repo has `.github/pull_request_template.md`, use it. Otherwise use [template.md](template.md).
2. Gather the sources:
   - Why: the linked issue, spec, or the conversation that led to the change. The diff shows what changed, not why.
   - What changed: `git log --oneline <base>..HEAD` and `git diff <base>...HEAD`. Get `<base>` from the existing PR (`gh pr view --json baseRefName`) or the repo's default branch (`gh repo view --json defaultBranchRef`).
3. Fill every section. [example.md](example.md) shows a finished PR: match its level of detail, not its content.
   - Why: the problem in one or two sentences. Link the issue if one exists.
   - What changed: short bullets on what the diff does. Under "Intentionally left unchanged", list what you deliberately did not touch (related code, known bugs, follow-ups). Write "Nothing notable" if the list is empty.
   - Validation and proof: check a box only if you ran that step in this session and saw it pass, and name the command and its result on the same line. After each unchecked box, add a short reason on the same line, for example "N/A, no UI change" or "not run, needs the staging database".
   - Rollback: "easy" or "hard", with the reason. Hard means the change is costly to undo once merged: a database migration, deleted data, a public API change, a sent email.
4. Leave "A fresh reviewer or agent reviewed the diff" unchecked unless a separate subagent, with no context from this session, reviewed the full diff. Say who reviewed it.
5. Replace secrets in pasted output (tokens, passwords, keys, connection strings) with `<REDACTED>`.
6. Delete the template's HTML comments.
7. Write the title in the imperative, under 70 characters.
8. Publish with a body file, so the Markdown survives shell quoting: write the body to a temporary file, then run `gh pr edit --body-file <file>` if the branch already has a PR, or `gh pr create --title "..." --body-file <file>` if not.
