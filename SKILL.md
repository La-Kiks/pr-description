---
name: pr-description
description: Writes a pull request title and description from the branch diff, using the PR template. Use when opening a PR, running gh pr create, or when asked to write or update a PR description.
---

# PR description

1. Pick the template. If the repo has `.github/pull_request_template.md`, use it. Otherwise use [template.md](template.md).
2. Read the changes with `git log --oneline <base>..HEAD` and `git diff <base>...HEAD`. The base is the branch the PR targets, usually `main`.
3. Fill every section. [example.md](example.md) shows a finished PR: match its level of detail, not its content.
   - Why: the problem in one or two sentences. Link the issue if one exists.
   - What changed: short bullets on what the diff does. Under "Intentionally left unchanged", list what you deliberately did not touch (related code, known bugs, follow-ups). Write "Nothing notable" if the list is empty.
   - Validation and proof: check a box only if you ran that step in this session and saw it pass. After each unchecked box, add a short reason on the same line, for example "N/A, no UI change" or "not run, needs the staging database".
4. Leave "A fresh reviewer or agent reviewed the diff" unchecked unless a separate subagent, with no context from this session, reviewed the full diff. Say who reviewed it.
5. Delete the template's HTML comments.
6. Write the title in the imperative, under 70 characters.
7. When creating the PR with `gh pr create`, write the body to a temporary file and pass it with `--body-file`, so the Markdown survives shell quoting.
