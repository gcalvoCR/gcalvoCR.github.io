---
title: Ruby setup macOS
author: gcalvoCR
date: 2023-06-28 12:00:00 -0600
categories: [concepts, ruby, setup]
tags: [concepts, ruby, setup] # tag names should always be lowercase
---

# Setup

MacOS does come with Ruby pre-installed. However, the version of Ruby that is included with macOS may vary depending on the specific version of macOS you are using.

It's recommended to check the version of Ruby installed on your specific macOS version by opening a terminal and running the command ruby -v

## Steps to run other versions

Install chruby and ruby-install with Homebrew
```sh
brew install ruby-install chruby

```

To install specific version of ruby
```sh
ruby-install ruby 2.7.1
ruby-install ruby 3.1.3
```

Make sure you're chruby works properly. If it shows a command not found exception.
Add following to ~/.bash_profile or ~/.zshrc:
```sh
# Make sure one of the paths exist:

# option 1
source /usr/local/opt/chruby/share/chruby/chruby.sh
source /usr/local/opt/chruby/share/chruby/auto.sh

# option 2
source /opt/homebrew/opt/chruby/share/chruby/chruby.sh
source /opt/homebrew/opt/chruby/share/chruby/auto.sh
```
*auto.sh above enables auto-switching if Rubies specified by .ruby-version files

Save your file and source it
```sh
source ~/.bash_profile
source ~/.zshrc
```

To list available Ruby versions:
```sh
chruby
```

To change ruby version
```sh
# to change it:
chruby 3.1.3
# to check version changed:
ruby -v
```

## Useful links
[Ruby on Rails](https://guides.rubyonrails.org/v5.1/getting_started.html)
[Ruby DOCs](https://www.ruby-lang.org/en/documentation/)

[GO RAILS](https://gorails.com/setup/macos/13-ventura)