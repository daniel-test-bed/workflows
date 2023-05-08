# Set Commit Status GitHub Action

This GitHub Action sets the status of a commit using the GitHub API. The action can be used in a workflow to automatically update the status of a commit based on the results of a build, test, or other process.

## Inputs

### `github_token`

**Required** Personal access token used to authenticate with the GitHub API.

### `state`

**Required** The state of the commit status. Must be one of `"pending"`, `"success"`, `"failure"`, `"error"`.

### `description`

The description of the commit status. Optional.

### `context`

The context of the commit status. Optional. Default: `"default"`.

### `sha`

**Required** The SHA of the commit to set the status for.

### `target_url`

The URL of the target of the status update. Optional.

## Example Usage

```yaml
name: Set Commit Status

on:
  workflow_dispatch:
    inputs:
      state:
        description: 'The state of the commit status'
        required: true
        default: 'pending'
        # other inputs omitted for brevity

jobs:
  set-commit-status:
    runs-on: ubuntu-latest
    steps:
      - name: Set Commit Status
        uses: daniel-test-bed/workflows@main
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          state: ${{ github.event.inputs.state }}
          description: ${{ github.event.inputs.description }}
          context: ${{ github.event.inputs.context }}
          sha: ${{ github.event.inputs.sha }}
          target_url: ${{ github.event.inputs.target_url }}
