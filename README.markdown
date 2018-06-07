[TOC]

# June 2018

## 2018-06-06

Rebooting this `.plan` after a long absence.  Again.

More work on switching to Linux.

Switched to [pass](http://passwordstore.org) from 1Password so I can use it
everywhere.  1Password has been pushing the cloud version pretty hard, so it's
probably only a matter of time before they deprecate the real app.  This was
painful.  I had to hack apart the `1password2pass.rb` file to handle my naming
conventions, and of course the version of that script in the `pass` repo was out
of date.

Got `weechat` up and running.  I can communicate again.

Got `offlineimap` running, but didn't finish the syncing yet (I have a lot of
mail).

Tore Roswell out of my `lispindent` and `clhs` scripts so it just builds with
vanilla SBCL now.  So much easier and less brittle.

Backlight support (specifically `xbacklight`) required editing `xorg.conf` as
described in the Arch wiki.  The backlight keys on the keyboard still don't
work, but at least I can dim the screen.

`xcape` remains busted in stumpwm for now.  Will debug later.

## 2018-06-07

Getting VPN set up.  Mostly used the network manager GUI to handle the settings.
To disable saving of the password I had to click the silly little icon in the
right of each password field.

Got my `xrandr` bullshit mostly tamed, thanks to some Lisp code from katco.
It's really nice to be able to script my window manager to add hotkeys with
Common Lisp.
