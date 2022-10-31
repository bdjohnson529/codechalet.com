---
title: "Changing Prompt Color"
layout: blog
order: 1
topic: Terminal
topic_path: /docs/terminal/index.html
---

ZSH is a UNIX shell. To change color in ZSH, modify the `.zshrc` file in your home directory. You can navigate to the home directory using
```bash
cd ~
```

Add the following line to your `.zshrc` file.
```bash
PROMPT='%F{cyan}%n%  %f @ %1~ $ '
```

* `%n`                 : name
* `%1~`                : folder name
* `%F{cyan} ... %f`    : changes the enclosed string to cyan