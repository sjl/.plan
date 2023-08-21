[TOC]

# August 2023

## 2023-08-21

First day of orientation as a PhD student.  Here we go again, back to school one
final time.

Figured out the campus wifi despite the Linux jankery.  Had to:

1. Register as a special device, the laptop registration link redirected to
   nothing useful.
2. Use `nm-connection-editor` from `gnome-network-manager` to edit the
   connection and manually set up the WPA2+PEAP+user/pass for the connection.

Finally fixed the dulwich errors from hg-git.  Since I'm using Debian's hg now
instead of building from source, I needed to install dulwich somewhere that the
system python can find it.  I almost installed `python3-pip` to do that, but
then realized I could just install `python3-dulwich` and be done.  Cool.
