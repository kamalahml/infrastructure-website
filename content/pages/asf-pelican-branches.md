Title: ASF Pelican feature branches

For large changes to your project website it will often be necessary to make a preview feature branch, work on it with others, and stage the results so you can review them. Here is how to create `preview/feature` branches.

Note: useful information is available from GitHub on <a href="https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-and-deleting-branches-within-your-repository#creating-a-branch" target="_blank">creating and deleting branches</a>.

## Creating a feature or preview branch

Replace `feature` with a name of your choice. You can have multiple feature branches, each with its own name and purpose.

From `main` create a `preview/feature` branch.

## Building

After you make a commit to your `preview/feature` branch, the Pelican build should happen automatically. You will get an email sent to `id@apache.org`.

A successful build will be found at `https://www-feature.staged.apache.org/`.

## Merging the branch into the trunk

Once your feature is complete, submit a pull request (PR) from `preview/feature` to `main`. Once the PR is merged the site updates to include the updated features.

GitHub has further information on <a href="https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request#creating-the-pull-request" target="_blank">merging branches</a>. 

## Example

1. Create `preview/bootstrap5`

2. Work on `preview/bootstrap5` branch to update bootstrap to version 5 with preview builds staged at https://www-bootstrap5.staged.apache.org/

3. Submit PR to merge `preview/bootstrap` back to `main`

## .asf.yaml settings

These settings in your project's .asf.yaml file do the automatic staging of preview branches.

```yaml
staging:
  profile: ~
  autostage: preview/*
```

## GitHub Workflow
This GitHub workflow in the default branch of your repository will build the preview branch

```yaml
name: Build a Pelican Website
on:
  push:
    # This prevents the workflow from running automatically on a new branch
    # When creating a new site branch, please ensure that the push and checkout branches agree
    # and that the action/pelican destination value is updated accordingly
    branches:
      - preview/*
      - master
  workflow_dispatch:
jobs:
  build-pelican:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: apache/infrastructure-actions/pelican@main
        with:
          # This must be appropriate for the branch being built
          destination: 'DESTINATION_BRANCH'
          gfm: 'true'

