---
title: "SCP"
layout: blog
order: 2
topic: Terminal
topic_path: /docs/terminal/index.html
---
SCP is a file transfer utility.

<hr><br>

# Commands
Transfer directory from local to remote
```
scp -r -i key.pem local_directory/ user@192.0.0.1:remote_directory/
```