---
layout: post
title: Vim -> Emacs
date: 2012-12-30
comments: true
categories: vim emacs
---

As you probably know I'm active Vim user, I use Vim daily for
about 3 years. I've started with a vimconfig of my friend
[@kossnocorp](https://github.com/kossnocorp)
then I tried Vim distribution called "Janus",
but it was complex and I decided to
create my own small [vimconfig](https://github.com/edtsech/dotvim),
now it's about 200 LOC and I'm always trying to keep it as simple as possible.
I've not written any single Vim plugin in the three years,
I have a small one ([vim-railsapi](https://github.com/edtsech/vim-railsapi),
but it's not really smth serious, one of the reasons is VimL, I think :)

## A few days ago

I've decided to try Emacs.

Why?

- EmacsLisp instead of VimL
- Built-in package manager from version 24
- Good support for Lisps including Clojure
- And of course just for fun

## What do I really need?

- Of course Vi motions
- Relative numbers
- Supertab auto completion
- Buffer explorer
- Ack for files

Support for langauges it's not really a problem in editors like Emacs, I think,
that is why I'm not counting it here.

I stared with my own empty [.emacs.d](https://github.com/edtsech/.emacs.d)
First thing I added was [evil-mode](http://emacswiki.org/emacs/Evil), because
my fingers can't live w/o vi-motions. Evil-mode works really perfect without any problems
and helped me to reduce amount of Ctrl clicks.

Next step is relative numbers and I was surprised to find mode for that [linum-relative](https://github.com/coldnew/linum-relative)
which is good and customizable.

For auto completion I've stared with [auto-complete](http://emacswiki.org/emacs/AutoComplete) which works great,
but popup window doesn't look beautiful.
![emacs popup](http://dl.dropbox.com/u/2428018/Screenshots/07.png)

*Buffer List* is kind of built-in buffer explorer in Emacs you can open it with `C-x b`
![buffer list](http://dl.dropbox.com/u/2428018/Screenshots/09.png)

And for Ack I've just installed ack plugin via elpa.
![list-packages](http://dl.dropbox.com/u/2428018/Screenshots/0a.png)

Basically you have mode/packages for everything:

- Rails with rinari
- Clojure mode
- Paredit mode
- Ruby mode
- YAML mode
- SML mode
- Haskell mode
- Cucumber with feature-mode
- Zencoding mode
- ...

I've spent one single day to setup my Emacs environment
and I feel myself pretty comfortabe. Which is amazing.
Let's see if it helps me to increase my productivity.

## PS: Emacs crash course

- Close Emacs: `C-x C-c`
- Open file: `C-x C-f`
- Swith "split": `C-x o`
- Make horizontal "split": `C-x 2`
- Make vertical "split": `C-x 3`
- Kill buffer: `C-x k`

## Peace!
