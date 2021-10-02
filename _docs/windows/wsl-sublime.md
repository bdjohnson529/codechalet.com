---
title: "Sublime on WSL"
layout: blog
topic: Windows
topic_path: /docs/windows/index.html
---

Presumably you will need some sort of text editor to edit your code. You can use VisualStudio, which reportedly has a nice integration with WSL2. I prefer to use Sublime Text, as it is a lighter application. To launch Sublime text from the Linux command line, you'll need to configure the `~/.bashrc` file, which defines aliases for the Linux command line.

First, make sure Sublime Text is installed on Windows. Likely it is installed at the following location : `C:/Program Files/Sublime Text 3/subl.exe`. You'll need to find where the Sublime executable lives, so that we can alias it in Linux. 

1. Launch Ubuntu.
2. Edit the `~/.bashrc` file.
```bash
sudo nano ~/.bashrc
```
3. At the bottom of the file, add the following line, where the path is the proper path to your sublime installation.
```bash
alias subl='/mnt/c/Program\ Files/Sublime\ Text\ 3/subl.exe'
```
4. Source the `bashrc` file.
```bash
source ~/.bashrc
```

Now you can launch sublime by typing `subl .` within any folder.