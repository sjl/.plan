[TOC]

# January 2020

## 2020-01-03

Converted `paste.stevelosh.com` to HTTPS.  Forgot it in the previous conversion.

## 2020-01-14

Moved all my repositories from Source Hut to `hg.stevelosh.com`.  Wasn't
expecting to have to shave this yak so soon, but such is life.  On the plus
side: pushing is *so much faster* now.  Rough timing for an empty push was ~5
seconds on Source Hut, down to around a second now.  No more sitting and
staring at the command line waiting to get back to work.

## 2020-01-15

Finished (mostly) reskinning `hg.stevelosh.com`.  Had to shave a couple of yaks
in Mercurial itself (diff headers getting truncated) and the hgweb Markdown
extension.  Ended up just completely forking the extension and tearing out
almost all of its guts.  The result should (hopefully) be easier to maintain as
Mercurial breaks internal shit over time.

Still need to finish the CSS for the rendered Markdown, but that can wait for
now.

## 2020-01-17

Got the RIT VPN set up on my Linux machine so I can connect for class.  I was
worried I'd have to install some horrible Cisco VPN client thing, but it turns
out you can use the `openconnect` client to connect, so `sudo apt install
openconnect` and then `sudo openconnect vpn.rit.edu` just magically works.
Fantastic.

Finished the `hg.stevelosh.com` reskin on my lunch break.  Just had to get the
`README`s looking decent.
