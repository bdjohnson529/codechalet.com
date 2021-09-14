---
title: "Azure Devops"
layout: blog
parent: Windows
parent_path: windows/
---
To get access to Azure Devops from linux, you will need to set up ssh keys. To generate an ssh key:
```bash
ssh-keygen -t rsa
```

View the public key
```bash
cat ~/.ssh/id_rsa.pub
```

Paste the public key in the devops settings.