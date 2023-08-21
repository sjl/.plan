[TOC]

# June 2023

Time to reboot this thing once again.

## 2023-06-18

Spilled coffee on my keyboard (Keebio Sinc Rev2), so I took the caps off to wash
them & it.  While they're drying I figured I should try using the new keyboard
I got to use at school (Keebio Sinc Rev3), to get used to it and discover any
issues.

Had to remember (again) how to flash this new one with a fresh QMK
configuration, because of course the process completely changed between r2 and
r3 so I need to keep track of two different methods.  Figured it out and added
a note in my repo so I'll remember for next time.

Once I was able to flash it, I had to figure out how to disable the RGB Gamer
Crud™ the stupid thing has enabled by default.  Googled around and found plenty
about how to enable the RGB crap, but less about how to disable it.  Eventually
I figured out the correct incantation to put into `rules.mk` and got it to look
like a normal keyboard.

Wanted to push those changes to GitHub but my GH personal access token seems to
have expired some time recently.  Went to create a new one and somehow the list
of permissions doesn't manage to make it clear which goddamn box you have to
check to say "just let me push and pull code".  For future reference: it's
`Contents`.

## 2023-06-21

Pushed some changes to `cl-digraph` I've had sitting around for a while after
writing up a couple of quick tests.

# August 2023

First day of orientation as a PhD student.  Here we go again, back to school one
final time.

Figured out the campus wifi despite the Linux jankery.  Had to:

1. Register as a special device, the laptop registration link redirected to
   nothing useful.
2. Use `nm-connection-editor` from `gnome-network-manager` to edit the
   connection and manually set up the WPA2+PEAP+user/pass for the connection.
