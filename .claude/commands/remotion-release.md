---
name: release
description: Release a new Remotion version
---

- Kill any `turbo` processes that might be running with SIGKILL
- Codex-specific: Before running release commands, make sure rbenv wins over the macOS system Ruby. Run release commands that may invoke Ruby/Bundler with:
  `PATH="$HOME/.rbenv/shims:$HOME/.rbenv/bin:$PATH" <command>`
- Run `npm login` (manual 2FA in the browser)
- Use `op item get "Npmjs" --fields password --reveal --account remotiondev.1password.com` to get the password for NPM.
- Use `op item get "Npmjs" --otp --account remotiondev.1password.com` to get a one-time password for 2FA.
- Run `npm token create --name="PublishRemotionXXXXXXXX" --packages "remotion" --packages "create-video" --packages-and-scopes-permission read-write --bypass-2fa --scopes "@remotion" --otp=<otp>`. Replace XXXXXXXX with a random string.
- Run `bun i`
- Run `bun run build`
- Run `npm view remotion version` to get the current version number
- Run `bun set-version.ts <version>`, where `<version>` is the current version plus 1. If the exit code is not 0, abort immediately.
- Run `cd packages/example && sh runlambda.sh && cd ../../..`. If this fails, abort the release.
- Run `NPM_CONFIG_TOKEN=<token> bun run release`
- Generate a changelog in markdown and save it to `/tmp/release-<version>.md`:
  - Run `git log v<previous_version>..v<new_version> --oneline` to get all commits
  - Extract PR numbers from merge commits
  - For each PR, run `gh pr view <number> --json title,author,number,url --jq '"* \(.title) by @\(.author.login) in \(.url)"'`
  - Categorize PRs into sections: "What's Changed", "Templates", "Docs", "Internal"
  - In "What's Changed", sort items so entries for the same package are adjacent. Changes to the `remotion` core package should appear first.
  - Strip redundant prefixes from PR titles
  - Linkify items whose PR added a new documentation page
  - Check for genuinely new contributors
  - Add `**Full Changelog**: https://github.com/remotion-dev/remotion/compare/v<previous_version>...v<new_version>` at the bottom
  - Use the same format as previous GitHub releases (check with `gh release view v<previous_version>`)
- **Don't release until you get approval. Allow me to edit it before.**
