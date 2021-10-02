---
title: "rbenv"
layout: blog
order: 0
topic: Ruby
topic_path: /docs/ruby/index.html
---
[Rbenv](https://github.com/rbenv/rbenv) is a great Linux tool for managing Ruby environments.  A counterpart in Python might be *Anaconda*. Rbenv uses [ruby-build](https://github.com/rbenv/ruby-build) to install Ruby. Using Rbenv, we can install a specific version of Ruby:
```bash
rbenv install -v 2.6.6
rbenv global 2.6.6
```

Rbenv uses *shims* - bash programs which route the commands to the correct Ruby installation. That way, we can have and use multiple Ruby installations on the same machine.

## Rbenv Setup
Install rbenv
```bash
sudo apt update
sudo apt install rbenv

# may not need these packages
sudo apt install git curl libssl-dev libreadline-dev zlib1g-dev autoconf bison build-essential libyaml-dev libreadline-dev libncurses5-dev libffi-dev libgdbm-dev

echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
```

Notice the last three lines. We add `.rbenv/bin` to the PATH, using `~/.bashrc`. We also add a command to initialize `rbenv`. When you open a terminal, the contents of the `~/.bashrc` are executed, and now `rbenv` will initialize when we open a terminal.


## Commands
Check Ruby version
```bash
ruby -v
```

## Resources
* [Install ruby on rails with rbenv, Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-with-rbenv-on-ubuntu-18-04)