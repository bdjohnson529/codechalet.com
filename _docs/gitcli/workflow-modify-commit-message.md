---
title: "Modify commit messages"
layout: blog
topic: git-workflow
order: 2
parent: Git CLI
parent_path: gitcli/
---

Suppose you have made some commits, pushed them to remote, and now realize that you want to change the title of the commit message. To do this, you will first need to check out the old commit
```bash
git checkout COMMITHASH
```

Modify the commit message
```bash
git commit ammend
```

Push to remote
```bash
git push -f origin HEAD:BRANCHNAME
```