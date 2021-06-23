# Check if the PR is up to date with base branch

## Motivation

Sometimes there's no point in running CI on a branch/PR that is not up-to-date with base branch.
## Notes

Default inputs (`base_branch` and `head_branch`) works only on PR events, otherwise you have to specify the branches explicitly.

## Usage

```yaml
name: PR CI

on:
  pull_request:
    types: [synchronize]

jobs:
  check:
    if: startsWith(github.head_ref, 'releases') != true
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0 # needed to have the base branch available for the action below
      - uses: stefanluptak/check-branch-up-to-date@v1

  ci:
    needs: check
    if: needs.check.outputs.up_to_date == 'true'
    runs-on: ubuntu-18.04
    steps:
      run: echo "This will run only when this PR is up-to-date with base branch"
    
    
```

## Inputs

| Input | Description | Required | Default |
| - | - | - | - |
| `head_branch` | Filename of the workflow that generated artifacts you want to delete  | ❌ | `github.head_ref` (only with `pull_request` event) |
| `base_branch` | GitHub repository you want to delete the artifact in | ❌ | `github.base_ref` (only with `pull_request` event) |
| `github_token` | GitHub token used to authenticate you GitHub API calls | ❌ | `github.token` |

## Outputs

| Output | Description |
| -------| ----------- |
| `up_to_date` | `"true"` if the `head_branch` is up-to-date with the `base_branch`, otherwise `"false"` |