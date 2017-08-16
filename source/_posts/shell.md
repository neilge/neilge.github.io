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

### Determine if it is a login shell

```bash
  if [[ -o login ]]; then
    print yes
  else
    print no
  fi
```

# Config Shell

## Start files

When starting Zsh, it will source the following files in this order by default:

* `/etc/zsh/zshenv`: Used for setting system-wide environment variables; it should not contain commands that produce output or assume the shell is attached to a tty. This file will ***always*** be sourced, this cannot be overridden.
* `$ZDOTDIR/.zshenv`: Used for setting user's environment variables; it should not contain commands that produce output or assume the shell is attached to a tty. This file will ***always*** be sourced.
* `/etc/zsh/zprofile`: Used for executing commands at start, will be sourced when starting as a ***login shell***. Please note that on Arch Linux, by default it contains one line which source the `/etc/profile`
	* /`etc/profile`: This file should be sourced by all Bourne-compatible shells upon login: it sets up `$PATH` and other environment variables and application-specific (`/etc/profile.d/*.sh`) settings upon login.
* `$ZDOTDIR/.zprofile`: Used for executing user's commands at start, will be sourced when starting as a ***login shell***.
* `/etc/zsh/zshrc`: Used for setting interactive shell configuration and executing commands, will be sourced when starting as an ***interactive shell***.
* `$ZDOTDIR/.zshrc`: Used for setting user's interactive shell configuration and executing commands, will be sourced when starting as an ***interactive shell***.
* `/etc/zsh/zlogin`: Used for executing commands at ending of initial progress, will be sourced when starting as a ***login shell***.
* `$ZDOTDIR/.zlogin`: Used for executing user's commands at ending of initial progress, will be sourced when starting as a ***login shell***.
* `$ZDOTDIR/.zlogout`: Will be sourced when a ***login shell exits***.
* `/etc/zsh/zlogout`: Will be sourced when a ***login shell exits***.

### Config `$PATH `

Normally, the path should be set in `~/.zshenv`, but Arch Linux sources `/etc/profile` after sourcing `~/.zshenv`.
To prevent your `$PATH` being overwritten, set it in `~/.zprofile`.

```bash
export PATH=/home/david/pear/bin:$PATH
```

### Set environment variables

Actually you can directly run 

```bash
JAVA_HOME = /path/to/jdk
```
to set JAVA_HOME as env virable and call it by

```bash
$JAVA_HOME

e.g. 

echo $JAVA_HOME
```

However, the env virable is temperary in this way and if we want to set a permanent env virable. we need to set it in `.zprofile`

### Get where is the command come from

Take `ls` as example

```bash
whereis ls
```

and 

```bash
/bin/ls
```

will be returned.

If we try to use `type` command

```bash
type ls
```

it will return 

```bash
ls is an alias for ls -G
```

to us

## Set up alias

## History search