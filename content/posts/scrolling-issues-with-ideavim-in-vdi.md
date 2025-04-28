---
title: "Scrolling issues with IdeaVim in VDI"
date: 2025-04-29T09:43:14+02:00
draft: true
---

For a client I had to work with IntelliJ IDEA on a VDI-Windows machine with
Citrix. The IdeaVim plugin for IntelliJ was acting really strange when in comes
to scrolling the editor view:

- When moving the cursor down line by line with `j` past the last visible line
  in the editor view, the cursor would move further down without the editor
  view scrolling with it, so that the cursor would be outside of the view. This
  didn't happen consistently, but often enough to be very irritating.

- Moving up and down with `Ctrl-u` and `Ctrl-d` would stop working properly as
  soon as reaching the upper or lower edge of the view and only move forward or
  backward one line instead of one page.

- Using `G` and `gg` to go to the last/first line in the file would move the
  cursor properly, but the view wouldn't scroll accordingly and instead stay
  whereever it was before issuing the command.

These are just the major issues I observed, I'm sure there are more.

I don't know if this might be something that is fixed in the most recent
versions of IntelliJ/IdeaVim as the one I was provided (and couldn't update) is
IntelliJ IDEA 2024.3.2.2 and IdeaVim 2.19.0.

Gladly I found that switching of "smooth scrolling" (_Settings / Editor /
General / Scrolling_) remedies all of the strange scrolling behavior.

