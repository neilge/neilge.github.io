---
title: Vi Cheatsheet
date: 2017-08-16 13:25:20
tags: [Vi]
---

Please refer to this article if you want to get more details: [Vim Cheat Sheet](https://vim.rtorr.com/)

# Commands

## Moving Cusor

* `w`: jump forwards to the start of a word
* `e`: jump forwards to the end of a word
* `b`: jump backwards to the start of a word
* `0`: jump to the start of the line
* `$`: jump to the end of the line
* `gg`: go to the first line of the document
* `G`: go to the last line of the document
* `5G`: go to line 5
* `Ctrl + b`: move back one full screen
* `Ctrl + f`: move forward one full screen
* `Ctrl + d`: move forward 1/2 a screen
* `Ctrl + u`: move back 1/2 a screen

## Editing

* `u`: undo
* `Ctrl + r`: redo

# Settings

## Make vi editor display line number

1. Press the `Esc` key if you are currently in insert or append mode.
2. Press `:` (the colon). The cursor should reappear at the lower left corner of the screen next to a `:` prompt.
3. Enter the following command: `set number`.