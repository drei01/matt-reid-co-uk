---
layout: post
title: Homebrew Install Jekyll
---

So you want to create a static website (or blog) using [Jekyll](https://jekyllrb.com/) but don't know how to install is on your Mac (OS X) with homebrew.

The good news is it's super simple, in fact you don't even need homebrew for most of it.

Start by installing Ruby, in a terminal enter:

```
brew install ruby
```

Once this is done you should be ready to install the Jekyll Ruby Gem

```
gem install jekyll
```

> You might need to `sudo` this command

Finally you can confirm Jekyll is installed with 

```
jekyll -v
```