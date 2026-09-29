# pr-description

A Claude Code skill that writes pull request titles and descriptions from the branch diff, using a fixed template: Why, What changed, Validation and proof.

The agent only checks a validation box when it actually ran that step, and gives a reason for each box left unchecked.

## Install

```bash
claude plugin marketplace add la-kiks/pr-description
claude plugin install pr-description@pr-description
```

Claude loads the skill on its own when you ask it to open or describe a PR. You can also run it with `/pr-description`.

To enable it for one project only, add `--scope project` to the install command.

## Update

```bash
claude plugin marketplace update pr-description
claude plugin update pr-description@pr-description
```

## Use a repo-specific template

If a repo has `.github/pull_request_template.md`, the skill uses it instead of the bundled `template.md`.

## Include it in another marketplace

Add this entry to the `plugins` array of the other marketplace's `.claude-plugin/marketplace.json`:

```json
{
  "name": "pr-description",
  "source": { "source": "github", "repo": "la-kiks/pr-description" }
}
```

## Files

```
.claude-plugin/plugin.json        plugin manifest
.claude-plugin/marketplace.json   lets this repo be added as a marketplace on its own
SKILL.md                          instructions for the agent
template.md                       the PR template
```

## License

MIT
