---
title: "Fixing up a Git Commit"
date: 2024-11-20T21:17:11Z
---

When working on a feature branch, I try to keep my commits coherent. One commit
should apply one particular change to the codebase that can ideally be
described with a concise commit message.

This often means that, as my understanding of the problem increases by working
on it, I want to modify past commits. If that's the most recent one, that's
easy, I can just do

```shell
git commit --amend
```
in order to add something to the last commit.

But if I want to modify an older commit, things get a little bit more
complicated. So far, what I did, was creating a temporary commit and then
squash it into the target commit using interactive rebase.

Recently I lerned from a [Stack Overflow
answer](https://stackoverflow.com/a/27721031/1225882) that there is a more
elegant method:

```shell
git add <whatever you want to commit>
git commit --fixup=OLDCOMMIT
git rebase --interactive --autosquash OLDCOMMIT^
```

To make this a little bit more efficient, I created an alias in my git config:

```
[alias]
  fixup = !git commit --fixup=\"$1\" \
      && git rebase --interactive --autosquash \"$1^\" \
      && :
```

