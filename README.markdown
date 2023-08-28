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

## 2023-08-22

Day 2.  Lots of getting talked at, meeting with advisors, etc.  Still trying to
get all the moving parts settled down — hopefully it'll be a lot clearer once
classes and rotations start (though I'm sure it'll be busy in a different way).

First time trying the Ann Arbor bus system, the bus was 20 minutes late.  This
bodes well.

## 2023-08-23

Got a presentation about things to do/see/eat in Ann Arbor.  Lots of things to
try.

Advice from existing student panel:

* Keep in touch and make connections with folks in your cohort/community who are
  going through the same stuff as you.
* Rotate with anyone your want, don't let anyone tell you not to.
* Don't forget to have a life.  Don't spend every weekend in the lab.
* Don't compare yourself to each other.  Lots of variety in the incoming people.
* Ask for help.

What to ask/think about when looking for a lab:

* Do you have funding to support me?
* Do you have plans to stay at the university?
* Talk to current and previous students (and where those ended up).
* Talk to multiple students (people have different experiences).
* Work ethic.
* Mentoring style.
* What are your expectations of me?
* Priorities toward students (high/low?).
* How did they handle difficult situations in the lab?
* Find a good PI, because they're the one that will be there the entire time
  (students/etc can and will leave).
* Tell them what you want to do (e.g. go to conferences), and based on their
  responses you'll know whether they're a good fit.
* Switching labs is possible (not ideal though).
* Listen when people tell you a place sucks.
* Alumni are great because they don't have the power dynamic to worry about and
  can actually be honest.
* You can change rotations if you really need to, even if it's the second week
  in.
* Ask how many slots there are vs how many rotations they're taking to judge how
  competitive joining the lab will be.

## 2023-08-24

Did the Python pre-test so I don't have to take the introductory programming
class.

Did more online training.

More talks.  Lots of meeting people after.

## 2023-08-25

Lost power last night because of the storms and DTE says I won't get it back til
tomorrow.  This is… not great.

Doing more trainings and paperwork at a school building so I can plug in my
laptop.

## 2023-08-28

Turns out I didn't get power until *last night*, i.e. three of God's own full
days after it went out.  Ann Arbor is… not feeling great right now.

Also, yesterday around 14:00 the university's network went down, entirely.
Unable to get online from the wifi, and any services hosted on the university
network are down, which is… not great.  Of course, many of the services used
(e.g. Canvas) are third-party services not hosted on the university network.
Except they all use the university SSO (because Security™), which *is* hosted on
the network.  So you can only use them if you're already logged in.  And of
course sessions expire super quickly (because Security™) so, in summary: lol.

Starting to use my HP-15C clone(s) from Swissmicros again.  Was getting
misleading results when trying to do some stuff with logarithms: it seemed like
it only had two digits of precision.  But after some digging around I realized
I must have configured the *display* precision to 2 SD's at some point in the
past and forgotten about it.  The full precision is there, it was only rounding
to display.  I set it to 6 to avoid this, but also the `PREFIX` key will show
the full precision temporarily.

Figured out (again) how to program the calculator to do logs of arbitrary bases.
Essentially:

    logₓ(y) = ln(y)/ln(x)

              stack
    LBL C     x y
    LN        x ln(y)
    x<->y     ln(y) x
    LN        ln(y) ln(x)
    ÷         ln(y)/ln(x) = logₓ(y)
    RTN

Got my budget scripts working and synced via syncthing (also shaved a couple of
yaks by making scripts to archive/create new hosts while I was at it).  Seems to
work okay at the moment.  Will gradually transition other stuff over time.
