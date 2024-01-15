This is my personal notebook where I dump thoughts and notes for my future self.

**I make no guarantees about the accuracy of anything in here.  Read at your own
risk!**

[TOC]

# January 2024

## 2024-01-08

Back from break.  Started a new rotation (classes don't start for another
couple of days).  Feels good to be back.

## 2024-01-09

Another day of rotation before classes start.  Getting my laptop set up to do
actual work again.

Looked around a little bit in Canvas.  One of my classes doesn't seem to have
posted anything yet, but I'm definitely registered so I think I should be good.

Did a couple of tasks to get ready for classes tomorrow (though they don't
*really* start til Thursday).

Need to remember to bring things into the lab tomorrow:

* Something to put my laptop on to raise it.
* Headphones.

## 2024-01-10

Cleaned up my schedule and sketched out my TODO list, found all the rooms for my
classes.  Got one new building to find/learn: USB, the "Undergraduate Science
Building".  I think I've seen it before, never been inside though.

First day of journal club.  Main things I'll need to do are:

* Ask two questions during the semester.
* Two review sessions for particular papers.
* Read over the rest of the papers.

## 2024-01-11

First two actual classes.

BS521.  Fairly straightforward.  8:30 AM sucks.  Tried to change lab sections to
something that works better with my schedule, but the class registration system
is awful and won't let me swap things out for some reason, despite there being
open seats.

BI529.  Need to watch videos (and do the embedded quizzes) before classes.
Really awful high-pitched whine from something in the ceiling in the spot I sat
in the room — need to move around and find a spot that isn't going to destroy my
ears. Got both Great Lakes and my VM set up with Jupyter (I think) and
accessibly by SSH port forwarding (e.g. `ssh -NAL 8888:localhost:8888
slosh@gl1234 -J gl`) so we'll see how this goes during the next class I guess.

Poked around at running `make docs` in a Lisp project with my new laptop and
something in `d`'s Python dependency shitpile broke since I last built it, so
I had to screw around with the guts of `d` to get it rendering again.  I really
need to rewrite `d` in a sane language.

Attempted to set up printing in the lab, but of course it doesn't work on Linux.

Downloaded the first 3 papers for journal club.  Need to print them and start
reading soon, at least for next week's.

After going back and forth with someone about the BS522 lab section stuff, they
realized they needed to grant me permission for that section.  Once they did
that I was able to swap it, so that's all set now.

Read through chapter 1 of the BS522 textbook.  It's… meh.

## 2024-01-12

Reinstalled Figlet and the `figlet-fonts` repo yet again on this new computer.
Finally got around to writing a script to do the stupid install so I don't have
to manually do it every time.

Reinstalled ABCL on the new machine.  Changed my scripts so they invoke `java
-jar /usr/local/bin/abcl.jar` directly instead of requiring
a `/usr/local/bin/abcl` wrapper for no reason, so now all I have to do is
download the binary distribution and move the two jars to `/usr/local/bin/`.

Reinstalled ECL on the new machine.  Trivial thanks to my notes, except the git
tagging convention switched from `ECL-1.2.3` to just a bare `1.2.3`.  My kingdom
for consistency.

Downloaded the textbook and marked down important dates for BI545 today so I'll
be prepared for class.

Running some of my project tests on the new machine resulted in `make: time: No
such file or directory` because… apparently Debian doesn't include
a `/usr/bin/time` by default?  Wow.  `apt install time` to get it.

Read chapter 2 of the BS522 book.  Mostly meh again.

One thing I'd like to do some weekend that's been on my mind for a while is
a small proof of concept web app with Lisp and HTMX.  Would be good to poke
around at it and see if I can make something reasonably easy to get up and
running, in case I want to do something like that in the future.  Stuff I'm
probably going to need to choose:

* Web server (almost certainly just boring old Hunchentoot)
* Router
* DB interface (probably Postmodern)
* DB migrations (will write my own)
* Template library (Djula is the obvious choice but has a shitload of deps)
* Monocss style

Also really need to write a simple FASTQ parser and bio seq library in Lisp, so
I don't have to do everything with janky UNIX tools.  Name idea: `skein`,
because it's for strings that are a tangled/knotted mess.  Should probably try
to separate interface and implementation pretty well here so I can potentially
plug and play different implementations in the future.

Found my way to the BI545 classroom.  These MSC/MSRB buildings are laid out like
someone's first Dwarf Fortress build.

First BI545 class.  Mostly reading the syllabus and going through Molecular
Biology 101.  Feels quite basic after HG545 last semester, hopefully things will
pick up as the course gets going.

## 2024-01-15

Tried to modify Pubmed search subscriptions but it looks like logging in via UM
Oauth is broken, sigh.

Finally got around to setting up keyboard shortcuts for a couple of my most
commonly used `pass -c` commands.  I should have done this months ago.


