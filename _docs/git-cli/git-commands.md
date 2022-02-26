---
title: "Git Commands"
layout: blog
topic: Git CLI
topic_path: /docs/git-cli/index.html
---

Test Git installation
```
git
```

Cache your credentials
```
git config --global credential.helper cache
```

Initialize a local repo
```
git init
```

Confirm files in staging area
```
git status
```

Commit the staging area to the repository.
```
git commit -m "Customize this commit message"
```

Push your local changes to the remote repository.
```
git push origin HEAD
```

Undo a local commit
```bash
git reset --hard HASH
```

Reset a file to a specific version
```bash
git checkout HASH -- Path/To/File
```

Delete local branch
```bash
git branch -D BRANCHNAME
```

Rebasing
```bash
git checkout FEATURE
git rebase master
```

Remove untracked local files
```bash
git clean -n
git clean -f
```

Unstage all files
```bash
git reset
```