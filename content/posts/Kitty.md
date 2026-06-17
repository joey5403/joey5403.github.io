---
id: Kitty
aliases: []
tags:
  - kitty
  - terminal
  - copy-paste
Category: Tech
date: 2022-10-08T18:50:00.000Z
title: Kitty
excerpt: 记录 Kitty 终端中 Emacs 或 Vim 场景下复制粘贴的问题，说明如何用 Shift 加鼠标选择绕开终端应用的选择模式。
---
# Kitty

## can't copy in emacs -nw
If you're trying to copy from vim launched in an SSH session, selecting with mouse drag will enter visual mode - so CTRL+SHIFT+C won't have any effect, because you're selecting in vim, not kitty. To select in kitty, use SHIFT+left mouse button drag 

from [stackexchange](https://unix.stackexchange.com/questions/500072/how-do-i-copy-and-paste-with-kitty) 
by [walnut-salami](https://unix.stackexchange.com/users/359008/walnut-salami)
