---
title: EC2 Setup
layout: blog
order: 2
topic: Databases
topic_path: /docs/databases/index.html
---
Note : eventually migrate this to the terraform repo workflow.

# Install asdf
```
sudo apt install curl git gcc
```

```bash
mkdir install
cd install
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.10.0

echo ". $HOME/.asdf/asdf.sh" >> ~/.bashrc
echo ". $HOME/.asdf/completions/asdf.bash" >> ~/.bashrc
source ~/.bashrc
```

# Install Ruby
```bash
asdf plugin add ruby
asdf install ruby 3.1.0
asdf local ruby 3.1.0
```

# Install postgres
```bash
sudo apt install postgresql-client-common
sudo apt-get install postgresql-client
```