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

## 2018-06-21

More math review.  I'm rusty.

More homework from the Prolog class.  This time it was the classic Family Tree
style exercise.  Wasn't too tough, even though my Prolog is *really* rusty.

Still on OS X for personal stuff until the rest of the parts for my
Linux/Windows machine arrive.

## 2018-06-22

Math review.

## 2018-06-23

Finished the Trains exercise for the Prolog class.  It was harder than
I expected — my Prolog skills definitely need work.  But I guess that's what the
class is for, right?

# July 2018

## 2018-07-01

The quest to make my new Linux machine usable continues.  Finally managed to
build Weechat from source after screwing around in dependency hell for a while
(apparently there's no `libgnutls30-dev` for Ubuntu 18.04?).  Also managed to
get the sound coming out the right ports after some dark incantation with
`pactl`.  Not using Gnome as a WM apparently means I'm going to be perpetually
confused about how to configure anything on this damn machine, I guess.

Catching up in the Prolog class.  Thankfully tomorrow is a holiday so I can
hopefully make some good progress there too.
