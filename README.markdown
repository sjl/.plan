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

Need to make a last-minute slide for myself for PIBS 800 when I get home.

## 2024-01-16

BS522 early.  Mostly review of stuff from BS521 today.

BI529.  Most of the time spent getting Jupyter working and the data all
downloaded.  Need to find a better workflow here.

BI545:

* Slurm account: `bioinf545w24_class`
* Scratch: `/scratch/bioinf545_w24_class_root/bioinf545w24_class/`
* Turbo: `/nfs/turbo/dcmb-class/bioinf545`
  * `gsi/`: GSI's stuff
  * `sec001`: directories for each student
  * `shared`: read-only, shared data and stuff.

Now basic UNIX/bash scripting stuff.

Slurm `.sbat` script tidbit: use `my_job_header` for debugging info.

Method for raw-dogging batch mode execution instead of writing an sbat: `sbatch
-c4 --mem=32G foo.sh`. Not sure I'll use that much, but good to know it's an
option.

Ate lunch during my short break today.  Tuesdays are going to suck.

Looked around again for how to integrate Jupyter and Neovim and found nothing
good.  Maybe I'll just suffer through using Jupyter for a class and not try to
shave this yak.

BS522 lab.  Pretty simple, but gave lots of advice for the homework which will
come in handy when I get to that.  Sketched out a LaTeX file for it, but
I really really need to get around to modularizing my LaTeX situation at some
point — the copy/paste is getting untenable.

## 2024-01-17

Finished BS529 exercise.  Looked at the solutions to figure out some of the
fiddly bits, like the 1-based indexing from the GFF (I was right) and the GFF
entry type (`CDS`, I was also right).  The problem was I was dumb and forgot to
reverse in the reverse complement.  Welp.

Went through the videos for BI529 tomorrow.

BI602.  Didn't get a chance to ask questions — this is going to be a very
annoying part of the class.

## 2024-01-18

BS522.  Started talking about simple linear regression.  Mostly still review at
this point.

BI529.  Talking about transcription factor binding sites, and fuzzy-matching
motifs using Positional Weight Matrices (PWMs).

Went to a lecture by my grandPI about the human skin microbiome, especially
mapping the distributions of various populations across the topology of the
human skin.

Wrapped up BI529 after getting the clarification email.  Today was more
straightforward than the last class, probably in part by not having to mess
around with Jupyter setup.

Did a first pass at a read of the journal club paper for next week.  It's an
older ML paper whose results are… meh?

## 2024-01-19

BI545. The next few classes will be mostly RNA-seq data, especially focused on
QC.  Need to watch 2 videos in the slides before next time.  Mostly a review for
me at the beginning.  Need to look into:

* Ribodepletion as an RNA selection step.
  * This just means using probes with magnetic beads to select and pull out ribosomal RNA so it doesn't get sequenced.
* Strand-specific library prep for RNA seq.

## 2024-01-22

Tried to watch the BI529 videos but they kept cutting out.  Will retry later.

Started the Biostat 522 homework.  So far it's… meh.  Still trying to find
a Latex font setup I like.  Going to try XCharter this time, it seems… slightly
better than Stix?  Really with I could use Rotation, but foundries gonna founder
I guess.

BI529 videos are still cutting out.  Ugh.

Watched the BI545 videos.  Those were on Youtube, so that worked reliably.

## 2024-01-23

The roads and sidewalks are one giant sheet of ice today.  This sucks.

BS522.  More linear regression stuff.  He really rushed through the last few
topics far too fast in the last couple of minutes of class — I think I need to
review those slides myself to make sure I got what he was trying to cover.

BI529.  Gibbs sampling.  Thursday will also be this topic, so if we finish today
we can skip that day if we want.

BI545.  QC and such for RNAseq.  Lots of various things to consider, but felt
like a bit of a grab bag of topics.

Read through the journal club paper again for tomorrow.  Some ideas on
questions:

* How does the performance of their tool compare to a human doctor?
* How robust is their data?  E.g. what if someone has a heart attack outside of
  the hospital, could that be counted as a control?

PIBS800.

BS522 lab.

## 2024-01-24

Finally learned about `View > Panes > Console on Right` in R.  Should have found
this months ago.

Reread the paper for BI602.  Being forced to ask synthetic questions sucks
a lot, but oh well.

BI602.

## 2024-01-25

BS522.  Many slides with walls of text and notation.

BI529.  Mostly done already, so just relaxing for a change.

Started reading the paper for BI602 review session tomorrow.

Poked around a little at implementing some of the 521 stuff in Common Lisp.  It
was trivial to port the first class, but I've now hit two stumbling blocks.

Naive parsing of bioinformatics files like FASTAs is slow when you have a stream
sandwich of a flexi stream wrapping a gzip stream wrapping a Lisp stream.  Can
likely live with this for now, and writing a real parser for some of the common
formats (which would probably work directly with the binary and avoid the slow
flexi stream layer) has been on my list for a while, so this isn't an
insurmountable obstacle.

The other snag I hit is the lack of Numpy.  There are a bunch of linear algebra
libraries in CL and they're all lacking.  Oddly enough the one that seems to
have the most promise for me is April, even though it would have the steepest
learning curve at the beginning.  I've poked around with it a bit before but
maybe this is a good time to actually give it a real try.  Need to go through
some/all of:

* <https://xpqz.github.io/learnapl/intro.html>
* <http://archive.vector.org.uk/art10011550>
* <https://microapl.com/APL/tutorial_contents.html>

At least I shaved the input yak the last time I looked at it, so I can dive
right in (as if I don't have enough other shit to do, but at least this is
computery so it's actually fun to learn).

## 2024-01-26

BI545.  More RNA seq lectures, talking mostly about how to normalize and account
for non-biological variability when doing differential gene expression.

BI602 review session.  Was pretty fun and chill and cool.  By far the best part
of the class so far.

Continued one of the APL tutorials.  Pretty basic stuff, pretty much just
getting my fingers used to the keyboard shortcuts to type basic stuff.

## 2024-01-27

Found a series of videos about using APL to build neural networks, which might
be a fun thing to go through:
<https://www.youtube.com/playlist?list=PLgTqamKi1MS3p-O0QAgjv5vt4NY5OgpiM>

Watched the BS521 videos for Tuesday.  Starting assembly with De Bruijn graphs
which is going to be fun.  Need to find those papers I read a while back that
had a good summary of the process.

## 2024-01-28

BI545 homework.  Long.  The first two sections (biology/computer stuff) were
easy, the last (experimental design) was rough.

Started the BS522 homework.  Going to finish it tomorrow I think.

Went through some more of those APL videos.  I'm actually liking it (and April)
quite a lot.  I feel like I might be actually motivated to learn this time
because I can see things I would use it for now, as opposed to years ago when it
was just a fun novelty.

## 2024-01-29

Finished BS522 homework.  That was *tedious*.  The inconsistent notation in this
class is… not fun.

## 2024-01-30

BS522.  Started multiple linear regression, mostly review for now.

