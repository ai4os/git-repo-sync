# Git Repo Sync

![build](https://github.com/wangchucheng/git-repo-sync/workflows/build/badge.svg)
![license](https://img.shields.io/github/license/wangchucheng/git-repo-sync)

Git Repo Sync enables you to synchronize code to other code management platforms, such as GitLab, Gitee, etc.

## Try Git Repo Sync

You can use the following example as a template to create a new file with any name under `.github/workflows/`.

```yaml
name: <action-name>

# Adjust for your needs, e.g. add your <branch-to-sync>
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
      - <branch-to-sync>
      - 'releases/**'
  delete:


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
        # Such as e.g. https://codebase.helmholtz.cloud/m-team/ai/ai4os-yolov8-torch
        target-url: <target-url>
        # You can store secrets in your project's 'Setting > Secrets' and reference the names here. Such as ${{ secrets.TARGET_TOKEN }}
        target-username: ${{ secrets.TARGET_USERNAME }}
        target-token: ${{ secrets.TARGET_TOKEN }}
```
