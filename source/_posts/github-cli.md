---
title: Git Cheatsheet
date: 2017-08-09 18:22:30
tags: [Git]
---

## Terminology

1. working directory
2. staging environment
3. repository

## Create a git local repository and track to a remote repository

1. **create a local repository**
	- go to the folder that contain the files that we want to add to repository
	- `git init`: create a local repository
	- add some files into the current directory
	- `git add <filename>` or `git add .`: add a file or add all files to the staging environment
	- `git commit -m "<commit message>"`: commit the files into local repository
2. **build a remote repository**

<!-- more -->
	- sign in the github account
	- click **+ New repository** button
	- and create a repository as instruction
3. **track the local repository to remote**
	- `git remote add <alias> <url>`: add a remote, `<alias>` is always set as `origin` and `<url>` is the http url copied from github
	- `git push -u <alias> <branch>`: push the content in the local repository to the remote, here, `<alias>` is always set as `origin` and `<branch>` is the branch that we want to push e.g. `master`
	- after tracking the local repository to the remote one, we can just use `git push` to push the commit to the remote


## Clone a project from github and sync the branches

1. **clone the project from remote**
	- `git clone <url>`: to clone the remote repository to local the default setting is only cloning the `master` branch
2. **Sync the branches**
	- `git checkout -b <local branch name> <alias>/<remote branch name>` clone a branch from github, e.g. `git checkout -b sched_mutex origin/sched_mutex`
	- if we want to sync all the branch at one time we can use the following command

		```bash
		git clone --mirror https://github.com/NilGE/weenix.git .git
		git config --bool core.bare false
		git reset --hard
		```
3. **only clone one specific branch**
	- `git clone -b <branch_name> <url>`

## Fetch, merge and pull

1. `git fetch <alias>`: fetch from remote
2. `git merge <other branch>`: merge other branch to the current branch, the `other branch` can be a remote branch
	- how to solve the conflict:
		//TODO:
3. `git pull`: `git fetch` + `git merge`

## Recover
1. `git checkout <filename>`: if we modify some files and we do not stage it, we can use this command to go back to the file's previous staging version
2. `git reset HEAD <filename>`: unstage the file
3. `git checkout <branch/file/SHA1>`: make the working directory is look like what the repsository look like for the given parameter
4. `git checkout --index.html`: `--`means stay in current branch
5. `git ls-files --deleted -z | xargs -0 git rm`: remove all deleted files
6. `git reset --hard HEAD`: go back to last commit
7. `git reset --hard <SHA1>`: go back to specific commit
8. `git add -u`: update all your changes

## Amend
1. `git commit --amend`: Combine the staged changes with the previous commit and replace the previous commit with the resulting snapshot. Running this when there is nothing staged lets you edit the previous commit’s message without altering its snapshot.

## Diff
1. `git diff <filename>`: check the different between staging and working directory
2. `git diff [file_name] --staged`: check the different between repository and staging
3. `git diff branch1..branch2`: compare the difference between two branches

## Rebase
1. first we have serval commits

	```vim
	e19a59e change 3
	5c02763 change 2
	9cc0c67 change 1
	5f71846 second commit
	8e2e1ee change six
	e8b2bfe change total five
	dc2da89 first commit
	```
2. we want to merge the last three use command `git rebase -i HEAD~3`
3. A file popup with the content

	```vim
	pick 9cc0c67 change 1
	pick 5c02763 change 2
	pick e19a59e change 3

	# Rebase 5f71846..e19a59e onto 5f71846 (3 command(s))
	#
	# Commands:
	# p, pick = use commit
	# r, reword = use commit, but edit the commit message
	# e, edit = use commit, but stop for amending
	# s, squash = use commit, but meld into previous commit
	# f, fixup = like "squash", but discard this commit's log message
	# x, exec = run command (the rest of the line) using shell
	# d, drop = remove commit
	#
	# These lines can be re-ordered; they are executed from top to bottom.
	#
	# If you remove a line here THAT COMMIT WILL BE LOST.
	#
	# However, if you remove everything, the rebase will be aborted.
	#
	# Note that empty commits are commented out
	```
4. we change the commands with direction, so that we can squash all three commits to one and rename the commit

	```vim
	reword 9cc0c67 change 1
	squash 5c02763 change 2
	squash e19a59e change 3
	```
5. Another file popup and we can rename the commit here

	change

	```vim
	change 1
	```
	to

	```vim
	total change three
	```
6. The confirmation file popup and after we close it, we finish rebasing

	```vim
	38e2f09 total change three
	5f71846 second commit
	8e2e1ee change six
	e8b2bfe change total five
	dc2da89 first commit
	```


## Patch
The goal of patching is patch serveral commits from one branch and apply the patch to another branch

1. We first have several commits in master branch

	```vim
	38e2f09 total change three
	5f71846 second commit
	8e2e1ee change six
	e8b2bfe change total five
	dc2da89 first commit
	```
2. Then we create a new branch 'newbranch' and make several commits

	```bash
	git checkout -b newbranch
	```
	```vim
	6700a4d change 3
	c345e71 change 2
	fac8e80 change 1
	38e2f09 total change three
	5f71846 second commit
	8e2e1ee change six
	e8b2bfe change total five
	dc2da89 first commit
	```
3. we patch the last three commits with command

	```bash
	git format-patch master --stdout > last_three.patch
	```
	* 	The above command means we patch the result of diff between current branch and master branch and combine all the commits into one patches
	* 	If we only write `git format-patch master`, we will create three patches
	*  We can change master with SHA1, so that we can make the patch from any commit

4. Check the content of the patch

	```bash
	git apply --stat last_three.patch
	```
	If we don’t get any errors, the patch can be applied cleanly. Otherwise we may see what trouble we'll run into.

5. Checkout to master branch and apply this patch

	```bash
	git checkout master
	git am --signoff < last_three.patch
	```
	```vim
	Applying: change 1
	Applying: change 2
	Applying: change 3
	```



## Log and Status

1. **Log**
	
	```bash
	git log
	git log --oneline
	git log --graph
	```

2. **status**
	
	```bash
	git status
	```


## Ignore changes to committed files

### Temporarily ignore changes
During development it's convenient to stop tracking file changes to a file committed into your git repo. This is very convenient when customizing settings or configuration files that are part of your project source for your own work environment.

```bash
> git update-index --assume-unchanged <file>
```

Resume tracking files with:

```bash
> git update-index --no-assume-unchanged <file>
```

### Permanently ignore changes to a file
If a file is already tracked by Git, adding that file to your .gitignore is not enough to ignore changes to the file. You also need to remove the information about the file from Git's index:

> These steps will not delete the file from your system. They just tell Git to ignore future updates to the file.

1. Add the file in your .gitignore.
2. Run the following:
	
	```bash
	> git rm --cached <file>
	```
	
3. Commit the removal of the file and the updated .gitignore to your repo.

This will be helpful when we **accidentally commit a file taht should be ignored**

## How to track a remote branch to local branch

## How to solve `fatal: refusing to merge unrelated histories`
