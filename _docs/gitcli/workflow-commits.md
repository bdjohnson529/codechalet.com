---
title: "Commits"
layout: blog
topic: git-workflow
order: 0
parent: Git CLI
parent_path: gitcli/
---

Initialize a local repo
```
git init
```

Add files to the staging area
```
git add -A
git add Recipes\SecretRecipe.txt
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