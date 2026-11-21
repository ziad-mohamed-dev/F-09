# Issue tracker: GitHub

Use `gh` for issues and specs in `ziad-mohamed-dev/F-09`. Run commands from this repository.

- Publish an issue or spec: `gh issue create --title "..." --body "..."`. For a multiline body, use `--body-file`.
- Fetch a ticket: `gh issue view <number> --comments`. Fetch labels with `gh issue view <number> --json labels`.
- List tickets: `gh issue list --state open`. Apply `--label` and `--state` filters as needed.
- Comment: `gh issue comment <number> --body "..."`.
- Apply or remove a label: `gh issue edit <number> --add-label "..."` or `--remove-label "..."`.
- Close: `gh issue close <number> --comment "..."`.

## Pull requests as a triage surface

**PRs as a request surface: no.**

If enabled, use the same labels and states for external PRs. Use `gh pr view --comments` and `gh pr diff` to read them, and `gh pr comment`, `gh pr edit`, and `gh pr close` to update them. List candidates with `gh pr list --state open --json number,title,body,labels,author,authorAssociation,comments`. Keep only `CONTRIBUTOR`, `FIRST_TIME_CONTRIBUTOR`, and `NONE`. For a bare number, try `gh pr view` before `gh issue view`.

## Wayfinding

- Store the map in an issue labeled `wayfinder:map`. Keep Notes, Decisions-so-far, and Fog in the body.
- Link child tickets as GitHub sub-issues. If unavailable, list children in the map's task list and put `Part of #<map>` in each child. Label each child `wayfinder:<type>` (`research`, `prototype`, `grilling`, or `task`).
- Use native dependencies. Add a blocker with `gh api --method POST repos/{owner}/{repo}/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`. Fetch the blocker's database ID with `gh api repos/{owner}/{repo}/issues/<blocker> --jq .id`. If dependencies are unavailable, put `Blocked by: #<n>, ...` in the child.
- Pick the first open, unassigned child in map order with no open blockers. Check `issue_dependencies_summary.blocked_by` or the fallback list.
- Claim with `gh issue edit <number> --add-assignee @me` as the session's first write. To resolve, comment with the answer, close the ticket, and append a summary and link to Decisions-so-far.
