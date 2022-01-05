---
title: "Installation"
layout: blog
topic: Haskell
topic_path: /docs/haskell/index.html
---
Notes taken from building a Yesod blog application on WSL - Ubuntu 18.04. To have a fully functioning Haskell toolchain, we will need to install the following tools:
* [Stack](https://docs.haskellstack.org/en/stable/README/), a build tool for Haskell
* [Yesod](https://www.yesodweb.com/), a web framework for Haskell
* [Cabal](https://www.haskell.org/cabal/), a packaging system for Haskell

## Setup
Install Stack.
```bash
curl -sSL https://get.haskellstack.org/ | sh
```
Next install Yesod.
```bash
stack install yesod-bin --install-ghc
```
Next install Cabal.
```bash
sudo apt-get install -y cabal-install
```
Test the Cabal installation.
```bash
cabal --version
```

## Install extensions for sublime
* Download the `.tmlanguage` files from the repo on [Bitbucket](https://bitbucket.org/dpwiz/sublime-yesod-git/src/master/)
* Follow the [instructions here](https://stackoverflow.com/a/29566977/9080991) to add the `.tmlanguage` files to package control.

### References
* [Making a Blog with Yesod](https://www.yesodweb.com/page/screencasts)
* [Don't Fear the Monad - Brian Beckman](https://www.youtube.com/watch?v=ZhuHCtR3xq8&list=LLO6sYggPZMleSdzNQmlc3Ew)