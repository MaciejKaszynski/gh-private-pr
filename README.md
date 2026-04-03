# gh-private-pr

A `gh` CLI extension for managing PRs between private and public GitHub repositories.

## Installation

```sh
gh extension install MaciejKaszynski/gh-private-pr
```

## Workflow

### 1. Set up remotes (once per repo)

```sh
gh private-pr private <remote>
gh private-pr public <remote>
```

`<remote>` can be a remote name already in your git config (e.g. `origin`) or a full GitHub URL.

```sh
gh private-pr private git@github.com:org/private-repo.git
gh private-pr public git@github.com:org/public-repo.git
```

Config is saved to `.git/gh-private-pr-config` and is never committed.

### 2. Add a branch

```sh
gh private-pr add <branch-name>
```

Creates two branches from your current HEAD and pushes both to the private remote:

- `<branch-name>-verified` — reviewed/verified changes
- `<branch-name>-unverified` — work in progress (you are left on this branch)

### 3. Open a PR on the private repo

```sh
gh private-pr create-pr
```

Opens the GitHub PR creation page in your browser with `<branch-name>-unverified` as the head and `<branch-name>-verified` as the base, ready to fill in the title and description.

### 4. Publish to the public repo

Once the PR is merged into the verified branch on the private repo:

```sh
gh private-pr publish
```

Pushes `<branch-name>-verified` to the public remote as `<branch-name>` (without the `-verified` suffix).

### Check current config

```sh
gh private-pr status
```

## Commands

| Command | Description |
|---|---|
| `private <remote>` | Set the private remote (name or URL) |
| `public <remote>` | Set the public remote (name or URL) |
| `add <branch-name>` | Create branches and push to private remote |
| `create-pr` | Open GitHub PR creation page in browser |
| `publish` | Push verified branch to public remote as `<branch-name>` |
| `status` | Show current config |

Note: This tool was created using claude code
