# Sync Repos Action

Sync Repos Action is a GitHub Action designed to synchronize files or directories across multiple repositories. This action is particularly useful for maintaining consistency across various repos by automatically propagating changes from a source path to a target path in different repositories.

## Usage

This action can be referenced in your workflow file with:

```yaml
- uses: FedericoGarza/sync-repos@main
  with:
    target-repo: target/repo
    target-path: target/path
    source-path: source/path
    branch-name: new-branch
    github-token: ${{ secrets.GITHUB_TOKEN }}
    commit-message: 'Commit message'
    base-branch: main
    label: documentation
    user-email: user@example.com
    user-name: username
```
Replace parameters as needed.

## Inputs

This action requires the following inputs:

- `target-repo`: The GitHub repository where the files or directories need to be updated. _(required)_

- `target-path`: The path of the target file or directory in the target repository where the changes need to be reflected. This can be a file or a directory. _(required)_

- `source-path`: The local path of the file or directory that contains the changes to be propagated. This can be a file or a directory. _(required)_

- `branch-name`: The name of the new branch to be created for the changes. _(required)_

- `github-token`: A GitHub token with appropriate permissions to create and manage PRs. Typically, you would use the GitHub provided `secrets.GITHUB_TOKEN`. _(required)_

- `commit-message`: The message for the commit that includes the changes. _(required)_

- `base-branch`: The branch that the changes should be based off of. If not provided, defaults to 'main'. _(optional)_

- `label`: The labels to be applied to the PR for better categorization. Defaults to 'documentation' if not provided. _(optional)_

- `user-email`: The email address associated with the GitHub account performing the action. This will be used to associate the commits and pull request with this user. _(required)_

- `user-name`: The username of the GitHub account performing the action. This will be reflected in the commits and pull request. _(required)_

## Outputs

This action does not have any outputs. However, successful execution will result in a pull request being created on the target repository with the propagated changes.

## Example Workflow

Here's an example of how you might use this action in a workflow:

```yaml
name: Sync Repos Workflow
on:
  push:
    branches:
      - main

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Sync Repos
        uses: FedericoGarza/sync-repos@main
        with:
          target-repo: target/repo
          target-path: target/path
          source-path: source/path
          branch-name: sync-branch
          github-token: ${{ secrets.GITHUB_TOKEN }}
          commit-message: 'Sync files'
          base-branch: main
          label: sync
          user-email: user@example.com
          user-name: username
```

Remember to replace the placeholders with actual values.

## Questions or Issues

If you have any questions or face any issues, please open a new issue in the action repository.
