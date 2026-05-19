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
