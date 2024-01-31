# Post PR Comment from Artifact

This GitHub Action allows you to post a pull request comment from an artifact.

## Inputs

- `GITHUB_TOKEN`: Github token of the repository - (default: `${{ github.token }}` [automatically created by Github])
- `artifact`: Name of the artifact - (default: "pr")

## Outputs

- `id`: ID of the comment
- `body`: Body of the comment
- `html_url`: HTML URL of the comment

## Usage

```yaml
name: Comment on pull request

on:
  workflow_run:
    workflows: ["create-artifact"] # the workflow that created the artifact
    types:
      - completed

jobs:
  upload:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
    if: >
      github.event.workflow_run.event == 'pull_request' &&
      github.event.workflow_run.conclusion == 'success'

    steps:
      - name: Post comment
        uses: hatemhosny/gh-action-example2@main
        with:
          GITHUB_TOKEN: ${{ github.token }}
```

## Credits

Based on:

- https://securitylab.github.com/research/github-actions-preventing-pwn-requests/
- https://github.com/thollander/actions-comment-pull-request

## License

MIT License
