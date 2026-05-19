# AGENTS.md

For all Aquis context/documentation tasks, Google Drive is the only source of truth.

## Aquis Context Workflow

This repository is only a runner for Codex Cloud.

The local repository and `/workspace/acquis` are not the source of truth for project context.

The source of truth is Google Drive.

## Google Drive Context Files

Use only these existing Google Drive Markdown files:

- PROJECT_CONTEXT.md
- ROADMAP.md
- DECISIONS.md
- BACKLOG.md

Do not create new Google Drive files.

Do not use local Markdown files in `/workspace/acquis` for context updates.

Do not use GitHub for context updates.

Do not create pull requests for context updates.

## How To Access Google Drive

Use:

- `GOOGLE_DRIVE_FOLDER_ID` from the environment
- `~/.config/aquis/google-service-account.json` as the service account credentials file
- `google-auth`
- `google.auth.transport.requests.AuthorizedSession`
- Google Drive API v3

Do not use:

- `google-api-python-client`
- raw sockets
- local repository files as source of truth

## Default Behavior For Context Tasks

When asked to update project context:

1. List files in the configured Google Drive folder.
2. Match one of the existing allowed Markdown files by exact name.
3. Read the current content of the target Google Drive file.
4. Update the existing file content.
5. Report which file was updated.

If the needed file does not exist in Google Drive, stop and report:

`MISSING_IN_GOOGLE_DRIVE`

Do not create a replacement file.

## Completion Response

At the end of every task, reply with a concise completion summary.

The summary must include:

- Status: completed, blocked, or needs review
- Files updated: list Google Drive Markdown files changed
- What changed: 2-5 bullet points
- Validation: what was checked
- Next step: only if user action is required

For Slack responses:
- Keep the final message short and readable.
- Do not include long code blocks unless explicitly requested.
- Do not print secrets, credentials, file IDs, or environment variable values.
- If the task updated Google Drive, explicitly say that Google Drive was updated.
- If the task could not update Google Drive, state the exact blocker.

Example:

Status: completed

Files updated:
- PROJECT_CONTEXT.md

What changed:
- Added the new Slack/Codex workflow.
- Clarified that Google Drive is the source of truth.

Validation:
- Confirmed the file was found in Google Drive.
- Confirmed the update request returned success.

Next step:
- None.

## Final Slack Summary

After every task, provide a final Slack-friendly summary with:
1. status
2. changed Google Drive files
3. brief change summary
4. validation performed
5. blocker or next step, if any

Keep it under 10 lines unless the user asks for details.
