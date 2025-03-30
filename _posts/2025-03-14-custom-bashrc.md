---
layout: single
title: "Customizing Git Prompt"
subtitle: "testing blog post!"
background: '/assets/images/background.jpg'

categories:
  - TEST-CATEGOTY
tags:
  - linux
---

# Customizing Git Prompt: Ubuntu vs Mac

When working with Git, having an informative and colorful terminal prompt can improve productivity. Both Ubuntu (using Bash) and Mac (using Zsh) allow customization of the terminal prompt, specifically to display the current Git branch. Here’s how I set it up for each.

## Ubuntu (Bash)

On the `~/.bashrc` file. Add the following
```
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
export PROMPT_DIRTRIM=2
export PS1="\[\e[34m\]\u \[\e[32m\]\w \[\e[91m\]\$(parse_git_branch) \[\e[33m\]$ \[\e[00m\]"

```
Save and reload the file:
```
source ~/.bashrc
```

## Mac (Zsh)

In Mac, you’ll need to modify the `~/.zshrc` file:

```
parse_git_branch() {
    git rev-parse --abbrev-ref HEAD 2>/dev/null
    }
export PS1="%F{blue}%n %F{green}%2~ %F{red}$(parse_git_branch) %F{yellow}$ %f"
```

Save and reload the file:
```
source ~/.zshrc
```
