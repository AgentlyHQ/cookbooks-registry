## Summary

Describe the CLI(s) you added or changed and why they belong in the registry.

## Checklist

Please confirm the following before requesting review:

- [ ] This PR updates `clis.json`
- [ ] The CLI is a real command-line tool, not just a library
- [ ] The GitHub repository is public and canonical
- [ ] The `slug` is stable and matches the repo path where appropriate
- [ ] The description is concise, factual, and non-marketing
- [ ] Install metadata is included only if it is known and verified
- [ ] The entry is relevant to agent, automation, or terminal-native workflows
- [ ] I validated the file against `schema.json`
- [ ] I checked that this is not a duplicate entry

## Agent-fit notes

If useful, explain briefly how an agent might use this CLI in practice.

Examples:

- machine-readable output
- non-interactive scripting support
- automation or CI usage
- API, infra, developer, or workflow integration

## Validation

Paste the command you ran locally, if any:

```bash
ajv validate -s schema.json -d clis.json
```

## Additional context

Add links, screenshots, docs, or caveats only if they help reviewers evaluate the entry.
