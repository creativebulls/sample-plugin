---
name: sync-target-to-github
description: Connect Adobe Target to a GitHub repository and export activities, audiences, and offers into that repo. Use when the user wants Target data synced, snapshotted, or written to GitHub.
---

# Sync Adobe Target to GitHub

Read Adobe Target through the `adobe-target` MCP server and write a snapshot into the GitHub repository the user names.

## Confirm the destination

Ask for the repository as `owner/repo` if the user did not give one. Use the folder `target/` at the repo root unless the user names another folder. Do not create or change Target activities, offers, or audiences unless the user explicitly asks for a Target change.

## Read Target

On the first Target call, the user must complete the Adobe sign-in and pick the organization. Read only what that account is allowed to see.

Collect:

- Active and inactive activities, with id, name, type, state, and last modified time when the tool returns them
- Audiences referenced by those activities
- Offers referenced by those activities

If a tool fails, report the error and stop. Do not invent activities, metrics, or ids.

## Write the repository

Create or replace these files in the destination folder:

- `index.md` — a table of activities with links to the detail files
- `activities/<activity-id>.md` — one file per activity, using only fields returned by Target
- `audiences.md` and `offers.md` — lists of the audiences and offers that were returned

Do not commit access tokens, cookies, or client secrets.

If GitHub write access is available, commit the files on a branch named `target-sync` and open a pull request. If it is not, show the file contents so the user can commit them.
