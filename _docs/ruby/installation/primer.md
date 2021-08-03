---
title: "Ruby Primer"
layout: blog
topic: ruby-installation
order: 1
parent: Ruby
parent_path: ruby/
---


## Ruby Gems
Gem is the package manager for Ruby. Each language has one or more package managers - Python uses *pip*, and Javascript uses *npm*. Ruby packages are called *gems*. To install the rubocop gem, for example, you can type the following into the command line.
```bash
gem install rubocop
```

Verify installation
```bash
which rubocop
```

## Bundler
*Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed.* **- [Bundler.io](https://bundler.io/)**

Using Bundler you can install a list of Ruby gems from a *Gemfile*. Bundler tries to make sure that you have the proper version of all dependencies. Using bundler is *usually* as simple as

```bash
bundle install
```


## Yarn
Yarn is a package manager for NodeJS. Check out [this article](https://linuxize.com/post/how-to-install-yarn-on-ubuntu-18-04/) to install Yarn on Ubuntu 18.04. To install and upgrade node modules,
```bash
yarn install
yarn upgrade
```