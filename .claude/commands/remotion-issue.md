---
name: issue
description: Create or update GitHub issues with correct Remotion naming and safe multiline Markdown handling
---

Use this skill when creating, editing, or commenting on GitHub issues.

## Issue title format

Use concise, action-oriented titles.

If the issue primarily affects a package, prefix the title with the package name:

```text
`@remotion/package`: Change description
```

Examples:

```text
`@remotion/player`: Support keyboard shortcuts for fullscreen
`@remotion/lambda`: Improve retry message for failed renders
`@remotion/docs`: Add examples contribution guide
```

If the issue affects the website/docs broadly, use:

```text
Docs: Change description
```

If the issue affects the Studio broadly, use:

```text
Studio: Change description
```

If the issue affects the monorepo or infrastructure broadly, use:

```text
Build: Change description
CI: Change description
Repo: Change description
```

Avoid vague titles such as `Bug`, `Fix issue`, `Examples follow-up`.

## Never pass multiline Markdown inline

Do not pass issue bodies, PR bodies, or long comments inline through shell arguments.

Avoid:

```bash
gh issue create --title "Docs: Add examples skill" --body "Line one\n\nLine two"
```

Instead, always write Markdown to a temporary file and pass it with `--body-file`.

## Creating an issue

1. Write the issue body to a temp Markdown file:

```bash
cat > /tmp/remotion-issue-body.md <<'EOF'
Summary of the issue.

## Tasks

- [ ] First task
- [ ] Second task
EOF
```

2. Create the issue using `--body-file`:

```bash
gh issue create \
  --title '`@remotion/package`: Change description' \
  --body-file /tmp/remotion-issue-body.md
```

## Editing an issue body

```bash
gh issue edit 1234 --body-file /tmp/remotion-issue-body.md
```

After editing, verify:

```bash
gh issue view 1234 --json body --jq .body
```

## Adding an issue comment

```bash
gh issue comment 1234 --body-file /tmp/remotion-issue-comment.md
```

## Final verification checklist

After creating or editing an issue:

- [ ] View the issue body with `gh issue view <number> --json body --jq .body`
- [ ] Confirm Markdown has real newlines
- [ ] Confirm the title follows the package/docs/studio naming convention
- [ ] Confirm issue references such as `#1234` are correct
