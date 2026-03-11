# cookbooks-registry

Open registry of CLIs that are useful for agents.

This repository is the source of truth for the Cookbooks registry data consumed by the Cookbooks app. It exists to catalog command-line tools that agents can discover, evaluate, and use in real workflows.

The focus is not "every CLI on GitHub." The focus is CLIs that are practical for agent use.

## Why this exists

Agents need tools they can reliably call from a terminal or automation environment. In practice, many CLIs are still built mainly for humans:

- interactive by default
- inconsistent output formats
- weak scripting support
- poor machine-readable errors
- unclear install paths
- undocumented auth flows

This registry highlights CLIs that are relevant to agent workflows, while making room for the ecosystem to improve over time.

Not every CLI works well with agents today. That is fine. The registry is meant to be open, evolving infrastructure for tracking the tools that do, and the ones that are getting there.

## What lives here

- [`clis.json`](./clis.json): registry entries
- [`schema.json`](./schema.json): validation schema for registry entries
- [`.github/workflows/validate.yml`](./.github/workflows/validate.yml): validates changes to `clis.json`
- [`.github/workflows/notify-app.yml`](./.github/workflows/notify-app.yml): notifies `cookbooks-app` when the registry changes

## Registry format

The registry is a JSON array of CLI entries.

Each entry currently supports:

- `slug` (required): stable identifier, usually `<owner>/<repo>`
- `name` (required): display name of the CLI
- `github` (required by schema): GitHub repository in `<owner>/<repo>` format
- `description` (optional): short summary of what the CLI does
- `install` (optional): package metadata
  - `npm`
  - `pip`
  - `brew`
  - `cargo`

Example:

```json
{
  "slug": "googleworkspace/cli",
  "name": "gws",
  "description": "Unified CLI for Google Workspace APIs.",
  "github": "googleworkspace/cli",
  "install": {
    "npm": "@googleworkspace/cli"
  }
}
```

## What belongs in the registry

This is an open source registry for CLIs that agents may use.

A strong candidate usually has some of the following:

- real command-line functionality, not just a library
- a public GitHub repository
- clear installation steps
- stable commands and flags
- useful behavior in non-interactive environments
- output that can be parsed or scripted
- workflows relevant to automation, agents, or terminal-native tooling

Examples include:

- developer tooling
- infrastructure and cloud CLIs
- data and API clients
- AI and agent tooling
- productivity or workflow automation tools
- domain-specific CLIs that are scriptable and operationally useful

## Contribution guidelines

Contributions are welcome.

If you know a CLI that agents can use, or should be able to use, open a pull request.

### Before submitting

Please make sure the entry:

- points to a real CLI project
- links to the canonical GitHub repository
- uses a stable `slug`
- has a concise, factual description
- includes install metadata when it is easy to verify
- is not already listed

### Editing rules

- Keep entries valid against [`schema.json`](./schema.json)
- Do not add extra fields unless the schema is updated in the same PR
- Keep descriptions short, neutral, and useful
- Prefer canonical package names
- Avoid marketing language
- Avoid duplicates

### Quality bar

We are especially interested in CLIs that are good fits for agents, but imperfect tools are still worth tracking if they are directionally useful.

A CLI does not need to be perfect to be included.

If a tool is promising for agent use but still has rough edges, that is still relevant. The broader goal is to map the ecosystem, not pretend the ecosystem is already finished.

## How to contribute

1. Fork the repository.
2. Edit [`clis.json`](./clis.json).
3. Validate the file locally.
4. Open a pull request.

## Local validation

GitHub Actions validates `clis.json` using `ajv-cli`.

Run the same check locally:

```bash
npm install -g ajv-cli
ajv validate -s schema.json -d clis.json
```

## Merge flow

- Pull requests touching `clis.json` run schema validation.
- Merges to `main` that update `clis.json` trigger a dispatch to `AgentlyHQ/cookbooks-app`.
- The app can then refresh against the latest registry data.

## For maintainers

If the registry format changes:

1. Update [`schema.json`](./schema.json)
2. Update the consuming app in `cookbooks-app`
3. Update this README

## License

MIT. See [`LICENSE`](./LICENSE).
