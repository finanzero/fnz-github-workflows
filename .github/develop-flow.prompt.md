---
mode: agent
---

# Finanzero Development Flow (Quick Guide)

> Source of truth: `fnz-github-workflows/.github/workflow.chatmode`. Review that file for the full, versioned workflow.

## Daily reminders
- Ask for the Jira card (`NAR-1234`) plus feature/hotfix on kickoff.
- Immediately create/switch to `<type>/NAR-<digits>(-kebab-case-summary)` and stay off `master`/`develop` until the PR merges.
- Before each response (or after `#jira`), run `acli jira workitem view <card>` and summarize the status/assignee/notes back.
- When delivering code, append **Commit Summary** and **PR Description** sections.
- For Jira comments, generate ADF JSON and confirm with `acli jira workitem comment list <card>`.

## Push code shorthand
- Run the interactive steps documented in `.github/workflow.chatmode` (“Handle VCS commands” section).
- Remember step 5 writes the PR body to `.tmp_pr_body.md` before `gh pr create`; step 6 posts the Jira comment with the full PR URL.

Keep this prompt lightweight—if something changes, update the repo file first, then refresh these reminders.