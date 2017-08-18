---
title: Linux Cli Cheatsheet
date: 2017-08-10 20:35:38
tags: [Linux, Cli]
---


# grep - search words in files

## The grep command syntax

```bash
grep 'word' filename
grep 'word' file1 file2 file3
grep 'string1 string2'  filename
cat otherfile | grep 'something'
command | grep 'something'
command option1 | grep 'data'
grep --color 'data' fileName
```

## Ignore the case

Use `-i` option

```bash
grep -i "boo" /etc/passwd
```

## Use grep recursively

```bash
grep -r "192.168.1.5" /etc/

or

grep -R "192.168.1.5" /etc/
```

### Suppress the file name

```bash
grep -hR "192.168.1.5" /etc/

or

grep -hR "192.168.1.5" /etc/
```

## Search for words only

### Search one word

```bash
grep -w "boo" file
```

### Use grep to search 2 different words

```bash
egrep -w 'word1|word2' /path/to/file
```

## Count line when words has been matched

The grep can report the number of times that the pattern has been matched for each file using -c (count) option:

```bash
grep -c 'word' /path/to/file
```

Pass the -n option to precede each line of output with the number of the line in the text file from which it was obtained:

```bash
grep -n 'root' /etc/passwd
```

## List the matching files

Use the -l option to list file name whose contents mention main():

```bash
grep -l 'main' *.c
```

Finally, you can force grep to display output in colors, enter:

```bash
grep --color vivek /etc/passwd
```

## Grep invert match

You can use -v option to print inverts the match; that is, it matches only those lines that do not contain the given word. For example print all line that do not contain the word bar:

```bash
grep -v bar /path/to/file
```

## Use pipe to grep

Display cpu model name:

```bash
cat /proc/cpuinfo | grep -i 'Model'
```


# find - find files in directories

Please refer this article if you want to get more details: 
[Find Files in Linux, Using the Command Line](https://www.linode.com/docs/tools-reference/tools/find-files-in-linux-using-the-command-line)

## Basic exmpales

Find a file called testfile.txt in current and sub-directories.

```bash
find . -name testfile.txt
```

Find all ·.jpg· files in the /home and sub-directories.

```bash
find /home -name '*.jpg
```

Find an empty file within the current directory.

```bash
find . -type f -empty
```

Find all `.db` files (ignoring text case) modified in the last 7 days by a user named exampleuser.

```bash
find /home -user exampleuser -mtime 7 -iname ".db"
```

## Use Grep to Find Files Based on Content

This searches every object in the current directory hierarchy (`.`) that is a file (`-type f`) and then runs the command `grep "example"` for every file that satisfies the conditions. The files that match are printed on the screen (`-print`). The curly braces (`{}`) are a placeholder for the find match results. The `{}` are enclosed in single quotes (`'`) to avoid handing grep a malformed file name. The `-exec` command is terminated with a semicolon (`;`), which should be escaped (`\;`) to avoid interpretation by the shell.

```bash
find . -type f -exec grep "example" '{}' \; -print
```

## How to Find and Process Files Using the Find Command

The `-exec` option runs commands against every object that matches the find expression. Consider the following example:


```bash
find . -name "rc.conf" -exec chmod o+r '{}' \;
```

# rsync

Please refer this article if you want to get more details:[Rsync (Remote Sync): 10 Practical Examples of Rsync Command in Linux](https://www.tecmint.com/rsync-local-remote-file-synchronization-commands/)

## Basic syntax of rsync command

```bash
rsync options source destination
```

## Some common options used with rsync commands

* -v : verbose
* -r : copies data recursively (but don’t preserve timestamps and permission while transferring data)
* -a : archive mode, archive mode allows copying files recursively and it also preserves symbolic links, file permissions, user & group ownerships and timestamps
* -z : compress file data
* -h : human-readable, output numbers in a human-readable format

## Copy a Directory from Local Server to a Remote Server

```bash
rsync -avz rpmpkgs/ root@192.168.0.101:/home/
```

## Copy/Sync a Remote Directory to a Local Machine

```bash
rsync -avzh root@192.168.0.100:/home/tarunika/rpmpkgs /tmp/myrpms
```

# Function

The function format is quite simple, but one thing need to be remembered. The args of function is "$@". This is all of the args and if you want to get each arg, you can get them by index but the this index starts from 1 but not 0.

Sync from remote

```bash
syncFromRemote () {
    rsync -avzh root@192.168.0.100:"$@" ~/reports/
}
```
Compare two number

```bash
compare () {
	if [ "$@[1]" -gt "$@[2]" ]
	then
		echo "larger"
	else
		echo "smaller"
	fi
}
```
