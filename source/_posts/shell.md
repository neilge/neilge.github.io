---
title: Shell
date: 2017-08-10 20:42:46
tags: [Shell,Zsh,Bash,Cli]
---


I have been using shell for quite a while, but sometimes I still need to search on google to find some very basic settings for shell, like adding a application to environment varibale. It is quite time consuming and unefficient. Therefore, I decided to make a cheatsheet to move these fragment knowledge into one place,  so that I can easily find them in the future.

# Cli For Shell

## Get current shell

```bash
$ echo $SHELL
```
<!-- more -->
## Change default shell

### List all installed shell
e
`chsh -l` does not work for me, so I choose another way:

```bash
cat /etc/shells
```

### Change the default shell

```bash
chsh /full/path/to/shell

chsh /bin/zsh
```

# Config Shell

## Start files

### Set environment variables

## History search