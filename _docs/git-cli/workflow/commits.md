---
title: "Commits"
layout: blog
order: 0
topic: Git CLI
topic_path: /docs/git-cli/index.html
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