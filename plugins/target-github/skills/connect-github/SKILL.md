---
name: connect-github
description: Connect the GitHub account used to push Target files. Use when the user asks to connect GitHub, sign in to GitHub, link a repository, or says GitHub is not connected.
---

# Connect GitHub

Connect the `github` MCP server at `https://api.githubcopilot.com/mcp/` so later Target creates can be committed and pushed.

## Connect

1. Tell the user you are connecting GitHub.
2. Call a read-only GitHub tool, such as the one that returns the signed-in user. The first call opens GitHub sign-in. Wait for the user to approve access.
3. Do not ask the user to paste a token, and do not write a token into any file.
4. After sign-in succeeds, read the signed-in username and say GitHub is connected as that user.

If the GitHub tool is missing, say the **target-github** plugin has to be updated and reinstalled so the GitHub server is included. Do not invent a connection.

## Repository

If the user names a repository as `owner/repo`, check that the signed-in user can write to it. If they do not name one, ask which repository should receive Target files. Remember that repository for the next Target create in this chat.

Stop if sign-in fails or the repository is not writable. Report the error that came back.
