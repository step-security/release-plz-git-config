[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# git-config

GitHub action to configure the git user corresponding to the `GITHUB_TOKEN` environment variable.

The action configures the git user name and email:

```
git config --global user.name <name>
git config --global user.email <email>
```

## Usage

Here's an example of how to use the action in a workflow to configure the git user.
After you configure the user, you can make changes and push them.

```yaml
name: Create new file

permissions:
  contents: write

on:
  workflow_dispatch: # Allow manual triggers

jobs:
  my-job:
    name: My job
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v7
      - id: git-author
        name: Configure git user from GitHub token
        uses: step-security/release-plz-git-config@v0
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      - name: Commit changes
        run: |
          echo "${{ steps.git-author.outputs.email }}"
          echo "${{ steps.git-author.outputs.name }}"
          touch new-file
          git add .
          git commit -m "Create new file"
          git push
```

<br>
