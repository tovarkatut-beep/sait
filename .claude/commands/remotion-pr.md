---
name: pr
description: Open a pull request for the current feature
---

Ensure we are not on the main branch, make a branch if necessary.

For all packages affected, run Oxfmt to format the code:

```bash
bunx oxfmt src --write
```

Then run:

```bash
bun run build
bun run stylecheck
```

to ensure we compile and CI linting/formatting passes.

Commit the changes. The title of the PR must be according to the [`pr-name`](./remotion-pr-name.md) skill.

Push the changes to the remote branch.

Use the `gh` CLI to create a pull request and use the same format as above for the title.

When creating the PR, do not pass the PR body inline through a shell command. Instead:

1. Write the PR body to a temporary Markdown file in the system temp directory (for example `/tmp/remotion-pr-body.md`).
2. Create the PR with `gh pr create --title "<title>" --body-file <path-to-temp-md-file>`.

Example:

```bash
gh pr create --title '`@remotion/package`: Add feature' --body-file /tmp/remotion-pr-body.md
```
