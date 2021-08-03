---
title: "SSH Keys for Azure Devops"
layout: blog
parent: Windows
parent_path: windows/
---

SSH keys are a verification method which you can use to clone repos from Azure Devops onto the WSL.

Generate ssh key
```bash
ssh-keygen -C "user@email.com"
```

View public key
```bash
cat ~/.ssh/id_rsa.pub
```

Add the public key to Azure DevOps. Make sure when you clone repos, that you are selecting the URL configured for SSH, rather than HTTPS.