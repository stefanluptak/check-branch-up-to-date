# Check if the branch is up to date with another branch

## Motivation

## Note

* defaults only on PR events

## Usage

### When closing pull request

```yaml
name: PR CI

on:
  pull_request:
    types: [opened]

jobs:
  check_pr_up_to_date:
    runs-on: ubuntu-latest
    steps:
      - uses: stefanluptak/check-branch-up-to-date@v1
      - name: CI
        run: echo "Running CI only when branch is up-to-date"
```

## Inputs

| Input | Description | Required | Default |
| - | - | - | - |
| `head_branch` | Filename of the workflow that generated artifacts you want to delete  | ❌ | `github.head_ref` |
| `base_branch` | GitHub repository you want to delete the artifact in | ❌ | `github.base_ref` |
| `github_token` | GitHub token used to authenticate you GitHub API calls | ❌ | `github.token` |

## Outputs

| Output | Description |
| -------| ----------- |
| `up_to_date` | `"true"` if the `head_branch` is up-to-date with the `base_branch`, otherwise `"false"` |