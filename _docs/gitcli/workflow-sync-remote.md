---
title: "Sync with Remote"
layout: blog
topic: git-workflow
order: 1
parent: Git CLI
parent_path: gitcli/
---
Most times you will configure Git with a remote repository. After you make changes, you will push those changes to the remote. Similarly, after the remote is updated, you will pull the remote changes onto your local machine.

## Pulling from remote
```
git pull origin BRANCH
```

## Pushing to remote
```
git push origin BRANCH
```

If you want to push the branch you are currently on, you can use:
```
git push origin HEAD
```