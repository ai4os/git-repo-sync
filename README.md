# Git Repo Sync

![build](https://github.com/wangchucheng/git-repo-sync/workflows/build/badge.svg)
![license](https://img.shields.io/github/license/wangchucheng/git-repo-sync)

Git Repo Sync enables you to synchronize code to **other code management platforms**, such as **GitLab**, **Gitee**, etc.

## Try Git Repo Sync

You can use the following example as a template to create a new file under `.github/workflows/`.

1. create two secrets: `secrets.TARGET_USERNAME` and `secrets.TARGET_TOKEN`
   * `secrets.TARGET_USERNAME` - store in this secret the username to access **other** code management platform, e.g. Gitlab
   * `secrets.TARGET_TOKEN` - store in this secret the token generated at **other** code management platoform, e.g. Gitlab
   
   :bulb: To add a new secret: in your github repository (you have to be admin) go to: <br>
`Settings` => `Secrets and variables` => `Actions` => `Repository secrets` => `New repository secret`
2. update field `target-url` in the template below
3. (optionally) add more branches to sync


```yaml
name: github-to-other

# Adjust for your needs, e.g. add your own <branch-to-sync>
# for more info: https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions
on:
  release:
    branches:
      - main
      - master
  push:
    branches:
      - main
      - master
      - dev
      - 'releases/**'
      # ADD ANY OTHER BRANCH IF NECESSARY
  delete:
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:


jobs:
  sync:
    runs-on: ubuntu-latest
    name: Git Repo Sync
    steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0
    - uses: ai4os/git-repo-sync@0.1.1
      # FORK of https://github.com/wangchucheng/git-repo-sync.git
      with:
        #########################################################
        # YOU SHOULD UPDATE "target-url" LINE below, e.g.
        # target-url: https://codebase.helmholtz.cloud/m-team/ai/ai4os-yolov8-torch
        #########################################################
        target-url: <target-url>
        # You can store secrets in your project's 'Setting > Secrets' and reference the names here. Such as ${{ secrets.TARGET_TOKEN }}
        target-username: ${{ secrets.TARGET_USERNAME }}
        target-token: ${{ secrets.TARGET_TOKEN }}
```
