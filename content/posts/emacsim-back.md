+++
title = "Emacs,I'm back!"
date = 2022-12-20T00:00:00+08:00
draft = false
+++

I change from Emacs and vim so many times.
And use SpaceVim and SpaceEmacs.
After a little try my own config,I found it's have to use SpaceEmacs.
So I start to read SpaceEmacs' doc.

This blog will record any thing I learn how to use Emacs.


## Open emacs in terminal {#open-emacs-in-terminal}

It's quite easy to open emacs in terminal

```bash
emacs -nw
```

but if you load a lot of plugin, it's a little slow to start.
so I aways run emacs as deamon

```bash
emacs --deamon
```

and use a client in terminal

```bash
emacsclient -nw somefile
```


## Searching and Replacing in Multiple Files {#searching-and-replacing-in-multiple-files}

A cool trick I learned recently is the ability to search and replace in multiple files.

1.  With helm-ag you can search through all files in your projectile project with SPC / or SPC s p.
2.  Enter your search query and a list of files with that occurrence will show up
3.  Then hit C-c C-e and Spacemacs will create a helm-ag-edit buffer
4.  Now you can use any command you’d normally be able to run on a buffer. For example, a simple Vim search and replace %s/alice/bob/g.
5.  Then hit C-c C-c to save the changes.


## How to run an emacs lisp program in the **scratch** buffer {#how-to-run-an-emacs-lisp-program-in-the-scratch-buffer}

1.  start emacs
2.  in the scratch buffer, type:(+ 2 2)
3.  press\`CTRL-X CTRL-E\`

you should get\`4\`in the echo area at the bottom of the screen
See also the Run a Program section in An Introduction to Emacs Lisp Programming


## Delete file in Emacs {#delete-file-in-emacs}

In Dired

d
Flag this file for deletion (dired-flag-file-deletion).
u
Remove the deletion flag (dired-unmark).
DEL
Move point to previous line and remove the deletion flag on that line (dired-unmark-backward).
x
Delete files flagged for deletion (dired-do-flagged-delete).


## Toggle Show Image in org-mode {#toggle-show-image-in-org-mode}

C-c C-x C-v (org-toggle-inline-images)
Toggle the inline display of linked images. When called with a prefix argument, also display images that do have a link description. You can ask for inline images to be displayed at startup by configuring the variable org-startup-with-inline-images119.


## Format Json {#format-json}

Emacs 24.4+ has built-in json-pretty-print and json-pretty-print-buffer functions.


## Spacemacs {#spacemacs}

| key   | remark  |
|-------|---------|
| SPC w | windows |
| SPC b | buffer  |
| SPC p | project |
