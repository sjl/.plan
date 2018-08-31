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

## 2018-07-03

The quest to make my new Linux machine usable continues.  Finally managed to
build Weechat from source after screwing around in dependency hell for a while
(apparently there's no `libgnutls30-dev` for Ubuntu 18.04?).  Also managed to
get the sound coming out the right ports after some dark incantation with
`pactl`.  Not using Gnome as a WM apparently means I'm going to be perpetually
confused about how to configure anything on this damn machine, I guess.

Catching up in the Prolog class.  Thankfully tomorrow is a holiday so I can
hopefully make some good progress there too.

## 2018-07-04

Managed to get Weechat to work with Unicode support.  I had installed
`libncursesw` and reran `cmake ..` but apparently that wasn't enough, I had to
fully blow away the `build/` directory and redo the `cmake` from scratch to get
it to link against `libncursesw` (rather than `libncurses`).  What a shitshow.
I really need to take a month off and write my own IRC client in CL.

Looked into an SBCL bug, but it turns out the standard is just kind of
ambiguous, and the current behavior is probably fine.

## 2018-07-07

Did the [Prolog modules tutorial][] for the Prolog class.  This made me really
appreciate Common Lisp's package system... the Prolog module system seems really
crufty in comparison.

Fixed a display issue for my blog, but I don't have Hugo set up on this machine
yet, so it'll have to wait to be deployed.

[Prolog modules tutorial]: http://chiselapp.com/user/ttmrichter/repository/gng/doc/trunk/output/tutorials/swiplmodtut.html

## 2018-07-08

Got mutt running on the new Linux machine.  The quest to convert my dotfiles
fully over to Linux continues.

Got ABCL, ECL, SBCL, and CCL all installed and working on the Linux machine.
I had originally installed SBCL (for bootstrapping a new build of it) and
StumpWM through the package manager and forgotten about them.  This meant I had
a `/usr/share/common-lisp` laying around which was getting loaded for other
installs too, which borked a few things.  I had to remove the old packages, blow
away `~/.cache/common-lisp`, and everything works now.  ECL is still installed
through the package manager, the rest aren't.

Started getting my Lisp test infrastructure up and running on the Linux box.
Previously I used [figlet][] and [lolcat][] to print nice headers during the
test runs.  I don't want to install Ruby on this machine if possible, so
I looked for a replacement for lolcat and found [toilet][], which includes the
functionality of both.  Great!  Had to download the figlet contrib fonts
manually, which was annoying (Homebrew on OS X did it automatically, but the
Ubuntu package doesn't).  Toilet's rainbows aren't as nice as lolcat's, but the
tradeoff of not needing ruby is worth it.

Got Hugo installed on the Linux box and made a build of my site.  I hope
I didn't break anything.  Made a couple of tweaks to fix a couple of issues
I noticed in Firefox on Linux.  Hand-compiled the LessCSS to avoid having to
install NodeJS on the machine.  Removed the timeago jQuery plugin -- the quest
to exterminate all JS on my website continues.

Wrote a blog post.  Will post it tomorrow.

Looked into why StumpWM's `remove` command is making the widths weird.  Gotta
dive in more when my mind is fresh.

[figlet]: http://www.figlet.org/
[lolcat]: https://github.com/busyloop/lolcat
[toilet]: http://caca.zoy.org/wiki/toilet
## 2018-07-10

Figured out why StumpWM wasn't noticing my timezone changes.  I tracked it down
to SBCL itself not noticing the timzeone changes — e.g. you can run
`(get-decoded-time)`, change your timezone, and run `(get-decoded-time)` again
and SBCL will still return the old timezone until you restart it.  Eventually
I narrowed this down to `get_timezone` in SBCL's
[`time.c`](https://github.com/sbcl/sbcl/blob/master/src/runtime/time.c), which
uses `localtime_r`.  The problem is that `localtime` and `localtime_r` don't
check for a timezone change, you have to call `tzset` yourself, according to
`man 3 localtime`.  So the solution is to run `(cffi:foreign-funcall "tzset")`
in your StumpWM process whenever you change your timezone.

Watched the Prolog class presentation from a couple days ago.  I'm still
a little bit behind, gotta hopefully catch up this weekend.

## 2018-07-14

Got `notmuch` set up on the new box.  Forgot how dang fast it is.

## 2018-07-15

Got `pass` sharing sanely on my phone and desktop.

## 2018-07-16

Installed the Arduino IDE on my desktop.  The quest to switch fully to Linux
continues.

## 2018-07-18

Started setting up my new Yubikeys.  The process is... not friendly.  I'm mostly
following [this guide](https://www.palkeo.com/sys/perfect-password-manager.html).

## 2018-07-19

Finished setting up the Yubikeys.  I think.

There's still a few fiddly bits -- handling multiple different Yubikeys seems
like it's gonna take a bit of scripting grease, and I don't think there's a way
to time out the PIN on the Yubikey after a certain amount of inactivity.
I think this should mostly be alright, since the only one I'll leave plugged in
is the Nano: that's plugged into my desktop monitor that I use for a KVM, so
whenever I switch the computers or turn off the monitor it'll lock.  I think
that's a good enough mix of practicality and security for what I need.

## 2018-07-20

Finally got around to fixing StumpWM's frame splitting/removing/balancing.  Got
a work-in-progress/proof-of-concept PR at https://github.com/stumpwm/stumpwm/pull/481

Debugged why my `scrot` keyboard shortcuts that work fine on Debian weren't
working on my Ubuntu machine.  It took a while because shell commands you run
through StumpWM's key mappings have their output blackholed to god only knows
where.  Eventually I split the commands into a separate shell script and
redirected all the output to a file (I should have done this much earlier),
which let me see giblib complaining about the keyboard being busy.  Once I found
that error it led me to https://bbs.archlinux.org/viewtopic.php?id=86507 which
shows a solution: add a `sleep 0.2` before the call to `scrot`.  Jesus.

## 2018-07-21

Did some coding interview-style programming exercises.  I'm rusty at this stuff.

Started writing a blog post.  It's turning out to be longer than I expected it
would be.  By now I should expect this.

## 2018-07-23

Cleaned up my Vim bundle folder.  Removed a bunch of things I never use.

Figured out how to do wildcard blocking in uBlock.  Again.  Here's for my future
self: the uBlock rule should look like `##[class^="prefix-"]` or
`##[class*="part"]`.

I think I found a setting to eliminate the screen tearing I've been seeing in
Ubuntu with my Radeon card.  It was described
[here](https://cubethethird.wordpress.com/2016/06/14/eliminate-screen-tearing-with-amd-gpu-on-ubuntu/).

Got Inkscape installed in preparation for setting up my AxiDraw again this
weekend.  Used the PPA to install the latest version (0.92).  EMSL recommends
0.91, but apparently I can use the prerelease version on one file for the
AxiDraw (`plot_utils.py`) and it should work okay.  I went ahead and version
controlled `.config/inkscape/extensions` this time for when I inevitably have to
dick around with the source again — I learned my lesson last time.

## 2018-07-25

Got `stumpish` set up so I can poke at stumpwm from within scripts.  Hacked my
`pass` binary to pop up the copied message with `stumpish` so it's a little less
opaque when I use the stumpwm shortcut to grab a pass.

## 2018-07-28

Finally got my VPN setup on the Linux machine.  Had to disable IPv6 at the
router because PIA doesn't support it, and leaving it enabled will leak my
actual IP, and I wanted to use OpenVPN instead of PIA's custom app thing.
Networking is a mess.

Got Project 1999 set up on Linux.  Fonts are a mess, but otherwise it's working
fine.  Had to add this to `~/.wine/user.reg` to get it to stop fucking up my
gamma:

    [Software\\Wine\\X11 Driver] 1269299093
    "UseXVidMode"="N"

# August 2018

## 2018-08-10

Tried to get Folding at Home working, but after about an hour of screwing around
with GPU drivers on Linux I gave up.  Sorry, I'd like to help, but I can't
invest the time to debug a basic install process.

Set up my own lightweight personal pastebin as outlined
[here](https://pinafore.social/statuses/100475132430233694).  The hardest part
was getting a working `pbcopy` and `pbpaste` inside a bash script.  I was using
`xsel` which works at my main shell but wouldn't work at all from inside a bash
script.  I assume this has something to do with `$DISPLAY`, but then I tried
`xclip` and it worked just fine, so fuck it.  Clipboards on Linux are such
a mess.

## 2018-08-12

Traveling.  Trying to use my second Yubikey on my work machine, and of course
it's a fucking mess because why would anyone ever possibly want to use more than
ONE single smartcard in their life, right?

The problem is that even though the secret keys for decrypting my `pass`
archives are on this second Yubikey, GPG always wants me to insert the original
Yubikey and pops up the "Please insert smartcard with serial number ..." dialog.
Even after I run `gpg --card-status` to forcibly tell its dumb ass to notice the
new card.

I tried the usual "delete the secret key and reimport the pubkey, then run
`--card-status` to make it notice" dance, but this time even *that* didn't work.
I ended up having to delete some files by hand:
https://donncha.is/2014/07/problems-using-an-openpgp-smartcard-for-ssh-with-gpg-agent/

How is any normal person supposed to actually *use* this software?

## 2018-08-13

At the office, trying to get my Thinkpad set up again.  Linux is a Journey.

Had trouble getting the external monitor to work.  Again.  First attempt: used
a USB-C to MiniDP dongle to a MiniDP to DP cable.  It saw the correct
resolution, but something in the dongle prevented it from calculating the
correct timing, and the monitor wouldn't work.

Second attempt: scavenged a raw USB-C to DP cable.  This actually worked.

Also had to scavenge a mouse.  Took a while to find the not-bluetooth USB
dongle.  I checked in all the USB ports on the monitors but didn't see it, til
a coworker pointed out the Apple keyboards also have a spare USB port and that's
where it was.

## 2018-08-20

Back in Rochester, and GPG is being an asshole once again.  Much the same
problem as on 8/12 — I'm trying to switch back to my normal Yubikey.  The
problem:

* I have two Yubikeys, A and B, which hold my GPG key K.
* I normally use A.
* I want to switch to using B.
* GPG still thinks the private keys for K are stored only on A, even when I plug
  in B.

The solution is:

1. Blow away the "keygrip" files in `~/.gnupg/private-keys-v1.d` corresponding
   to the keys on the Yubikeys, but **not** other keygrip files.  An easy way to
   do this is something like `grep -rl shadowed-private-key ~/.gnupg/private-keys-v1.d/ | xargs rm`.
2. Run `gpg --card-status` so GPG will notice the missing keygrips and realize
   they're on this *new* Yubikey.

I should probably wrap this up into a script.

## 2018-08-27

Tad says I need some kind of "udev rule" for my Switch controller under Linux:

    KERNEL=="hidraw*", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="2009", MODE="0666"

I don't know what this means, but I'm dumping it in here for later.

Published http://stevelosh.com/blog/2018/08/a-road-to-common-lisp/ after many
plane rides and weekends.

## 2018-08-30

Another Ubuntu setup.  Practice makes perfect I guess.

Things I needed to `apt install` to get something usable:

* `arandr`
* `aspell-en`
* `aspell-is`
* `autoconf`
* `build-essential`
* `chromium-browser`
* `cmake`
* `curl`
* `dunst`
* `exfat-fuse`
* `exfat-utils`
* `fish`
* `git`
* `gnupg-agent`
* `htop`
* `hugo`
* `inkscape`
* `libx11-dev`
* `mmv`
* `msmtp`
* `neomutt`
* `neovim`
* `network-manager-openvpn-gnome`
* `notmuch`
* `offlineimap`
* `pcscd`
* `python-neovim`
* `python3-pip`
* `restic`
* `rlwrap`
* `scdaemon`
* `scrot`
* `slock`
* `texinfo`
* `tmux`
* `toilet`
* `tree`
* `vlc`
* `w3m`
* `wget`
* `xautolock`
* `xcape`
* `xclip`

Updated my dotfiles bootstrap script to include the new linux symlinks.

Bootstrapping the system is still an uphill fight.


## 2018-08-31

Continuing bootstrapping.

Installing Dropbox makes things a lot easier because I can easily sync little
bits of state between computers.  But the Dropbox site sure doesn't make it
easy.  To my future self: here's how to install Dropbox on Ubuntu:

* Download the `.deb` file from their site.
* `sudo dpkg -i thefile.deb`
* `dropbox start -i`

Important: **do not run the last command with sudo**, because if you do your
entire installation will be totally fucked (`~/Dropbox` will be owned by root)
and you'll have to start all over.

Building Mercurial from source.  Had to install `python-dev` first.

As always, `hg-git` is fucking broken on install.  Had to symlink
`dulwich/dulwich` into the Mercurial directory, but it was still broken.
[This](https://bitbucket.org/durin42/hg-git/issues/252/hg-47-error) is the
problem.  Mercurial's lack of a stable plugin API is why I no longer really
maintain my hg plugins.  It sucks.  For now I'm just gonna downgrade Mercurial.
