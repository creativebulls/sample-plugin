---
name: sync-target-to-github
description: Version-control Adobe Target in GitHub. Use when the user creates or changes an activity, offer, or HTML offer, or asks to connect Target to a GitHub repository. Commit the definition to GitHub before creating or updating it in Target.
---

# Version-control Target in GitHub

GitHub is the source of truth. Adobe Target is updated only after the matching files are pushed.

The `adobe-target` server is `https://targetmcp.adobe.io/mcp`. The first Target call asks the user to sign in to Adobe and choose the organization. GitHub writes use the `github` server. If GitHub is not connected, run the `connect-github` skill before the first push. Do not store tokens, cookies, or client secrets in the repository.

## Destination

If the user did not give a repository, ask for it as `owner/repo`. Keep files under `target/` at the repo root unless the user names another folder.

| What the user creates | File |
| --- | --- |
| Activity | `target/activities/<slug>.json` |
| Offer | `target/offers/<slug>.json` |
| HTML offer | `target/html/<slug>.html` plus `target/html/<slug>.json` for the offer name and Target id |

`<slug>` is the name in lowercase with spaces replaced by hyphens.

## Create or change

Follow this order. Stop if a step fails.

1. Write the activity, offer, or HTML into the file above. Include the name and the content the user asked for. Leave `targetId` empty on a new item.
2. Commit and push that file to the default branch. Use a message such as `Add Target activity homepage-banner`.
3. After the push succeeds, create or update the item in Target with the `adobe-target` tools.
4. Write the id Target returns into `targetId` in the same file, then commit and push again with a message such as `Record Target id for homepage-banner`.

Do not call a Target create or update tool before the first push succeeds. Do not invent ids, metrics, or HTML.

A create made directly in the Target website is not sent to GitHub by this plugin. When the user asks to backfill those items, read them from Target and commit one file per item using the same paths.
