This is my personal notebook where I dump thoughts and notes for my future self.

**I make no guarantees about the accuracy of anything in here.  Read at your own
risk!**

[TOC]

## 2024-02-01

Tried to commit my dotfiles this morning and had to commit to a subrepo
I modified yesterday.  Wanted to push that to the git mirror but the hg-git
mapping was fucked again, so I needed to run that janky `remap-hggit-mapfile`
thing I wrote ages ago.  But I needed to port *that* to Python 3 to get it to
run on this laptop.  Did that and finally unwound the stack of yaks.  Ugh.
Final process to run the remapping is something like:

    cd src/foo
    cd .hg
    git clone https://github.com/sjl/foo gitrepo
    cd ..
    remap-hggit-mapfile . .hg/gitrepo
    remap-hggit-mapfile . .hg/gitrepo > .hg/git-mapfile

BS522.

BI529.  Going to release the first homework assignment today.  The assignment
was tricky today — I think there's a bug in the doctest and/or their
implementation of the Eulerian walk.

Continued watching a couple of APL videos.

## 2024-02-02

Started reading the journal club paper for next week, about prediction of CRISPR
off-target effects.  It's not very well-written, unfortunately — I'm not even
a page in and there are multiple typos.

BI545.  Lecture plus interactive lab on Great Lakes.  The lab was okay, but
quite rushed because the lecture took a long time.  I'm pretty decent at CLI
stuff so it went smoothly for me, but I still didn't have enough time to finish
in class.

## 2024-02-03

Watched some BI529 videos for next week.  Still need to finish up the homework.
Next week is BWT, which always breaks my brain, so I think I should probably
have a poke around tomorrow just to get my head around it again.  I wonder how
it would be to implement in APL.

## 2024-02-04

Finished the BS529 homework.  Wrote a bunch of stuff about the confusing parts
in the summary document only to realize there's a one page limit.  Oh well, it
was cathartic for me at least.

Started the BS522 homework, but I just don't have the willpower to deal with the
tedium of this today.  I'll get it done tomorrow.

Looked at some BWT transform videos.  I think I understand it a little better
now, though not sure if I'll retain it.  I need to write it down at some point
if I really want to remember it (is it worth it?).

## 2024-02-05

Read part of the chapter on BWT in the Bioinformatics Algorithms textbook.
It's… really not great.  They have a really weird way of presenting algorithms
that's long and rambly and does a lot of unnecessary work to actually explain
things.  Sometimes they go on for a page about something trivial, and other time
gloss over major points.

I think I need to find a better source to review for tomorrow.  Found
<https://james.fabpedigree.com/bwt.htm> which is actually pretty nice because it
shows how to *efficiently* do this, albeit with godawful terse C code.  After
going through it and deciphering the stupid C programmer shortcuts… I think
I finally get it.  At least the efficient compression and decompression side of
things.  Took me a long time, but it feels good.

BWT fried my brain, so I'm procrastinating the tedious BS522 homework til
tomorrow.  Sorry, future self.

## 2024-02-06

Slept late, missed BS522.  Need to watch the VOD tomorrow.

BI529 about BWT.  Easy given that I figured it out yesterday, though there were
some new data structures that we'll need for string matching (which I still
haven't figured out — only the decompression).

Had a stroke of luck with respect to the BS522 homework — they pushed the due
date back to Sunday (four more days) so I've got a few more days to deal with
it.  That's a relief.

BI545, about novel transcript identifications.

## 2024-02-07

Spent a ton of time trying to decipher what the BI529 homework was trying to ask
for.  Not fun.

BI602.  Paper was about using machine learning to predict CRISPR off target
scores for various sgRNA configurations.

## 2024-02-08

BS522.  Feels like we're moving incredibly slowly now, but the homeworks are
still painful.  Very strange.

BI529, BWT matching.  Going to try to make sure I understand what's actually
happening here.

BI545, hodgepodge of various topics (RNASeq contamination, GEO databases?).
Trying to install the R packages they told us to install at the beginning of
class using the cluster was an absolute mess, because 50 people all hitting the
login nodes and doing a ton of file IO slows everything to a crawl.  I ended up
doing things locally, which was much faster.

Started reading the paper for journal club next week, about prediction
transcriptional response to genetic perturbation.

## 2024-02-10

Watched BI529 videos.

Finally did the absolutely mind-numbing homework 3 for BS522.  Truly, truly
miserable.  Result was eleven pages, much of which was manual plug n' chug
algebra to verify that R can, in fact, do math correctly.  Very unpleasant.

## 2024-02-11

Did a chunk of the BI545 homework.  Otherwise not super productive today,
unfortunately.

## 2024-02-12

Finished BI545 homework.

## 2024-02-13

BS522.  This class is too early.  Spent all class talking about the special case
of binary interaction variables, which felt like it didn't need a whole entire
class just for that.

Forgot to charge my laptop last night, so I'm at 50% in BI529.  Welp.  Managed
to finish all but the last function, though the documentation was not
particularly clear and I think they didn't expect us to handle certain edge
cases they gave us.  Finished that last bit of 529 right before 545 started.

BI545.  Another grab bag of stuff, none gone into a lot of depth, lots of magic
incantations for how to perform analyses in R without explaining what everything
is.  Oh well.  Checked my work with some folks after class and feel a bit better
now.

PIBS800, training grant fair.
