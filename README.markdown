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

BS522 lab.

## 2024-02-14

Reading the paper for BI545 on Friday.  They're trying to figure out the cause
of undiagnosed rare muscular diseases using RNA seq to look for alternative
splicing events.  Noticed that figure S6 is confusing because they say in the
paper the median number of potentially pathogenic splice events per sample for
the "all genes" category is 190, but the S6 figure caption says 105, and the
figure itself looks like the median in the box plot is more like 250.  So… which
is it?  Finished the paper up to the methods section, will take a look at that
tomorrow I think.

## 2024-02-15

BI529 in the morning.  Managed to finish it in class at the end with some hints
from Alan.  Wasn't too bad once I understood what they actually wanted.

## 2024-02-16

BI545.  This is the class where we had to read the paper about using RNA seq to
find novel splice isoforms in patients with undiagnosed muscular diseases.  Also
getting some information about the group project.

Figured out how to get R working with Vim.  I should have done this months ago,
now that I've got it set up it's no longer nearly as painful to work in R.  The
trick was realizing that base R running in a terminal, *on its own*, can open up
a plot window itself.  So I don't have to do any horrible workarounds to get
plots visible, they just appear in a window that I can put wherever I want.
Maybe BS522 homework won't feel so painful now.

## 2024-02-17

Did the BS522 homework.  This one wasn't as mind-numbing as the last one,
thankfully.  Only a tiny bit of R involved, but I can already tell I'm loving
the Vim setup with it.  I can edit my code and LaTeX in the same editor, imagine
that.

## 2024-02-18

Read some of the paper(s) for journal club this week.

## 2024-02-19

A bunch of homeworks got rescheduled, and now everything is due on Friday.  Ugh.

Puttered around making a `reductions` function in the evening.  Turned out to be
tricky if you want it to work like CL's actual `reduce`, i.e. supporting
`start`, `end`, `key`, `from-end`, and `initial-value` properly.  I think I've
got something working, though it would also be nice to add a `result-type`
argument so you could ask for a vector directly though.

## 2024-02-20

BS522.  Another day on multiple regression, this time they mentioned continuous
vs continuous but otherwise it still just feels like treading water.  I feel
like we got everything thrown at us in the first week and have been stalled on
the same stuff ever since.

BI529.  This week was much easier, maybe because I slowed down and read the
description more carefully first to try to

* Try to figure out the biology behind what we're actually implementing.  Way
  too easy to treat the problems as a black box, but I'm actually getting to the
  point now where the biological context *helps* me, rather than overwhelming
  me.  Progress?
* Identify which things they're going to handwave over in the implementation
  (e.g. today we just compare *all* genes with *all* SNPs, not the ones near
  them like you'd have to do in reality).

Anyway, reading carefully at the beginning saved me going down a couple of
rabbit holes along the way.  Need to remember to do the same next time.

BI545.  ChIP-seq.

PIBS800, about funding after the PIBS year.  Need to remember to register for
604 as soon as I'm able.

* Figure out who the graduate coordinator is, check in with them once per term
  about funding/appointment changes etc.

Funding mechanisms:

* Fellowship, etc.  Paid through financial aid system.
* Training grants.  Paid through financial aid system.
* Graduate Student Research Assistant (GSRA), paid through HR.
* Graduate Student Instructor (GSI), paid through HR.

EdM stuff:

* Need to be in PhD lab and program as of July 1.
* Make sure rotation 4 is done in EdM (I think we did this long ago).

## 2024-02-21

Found <https://www.ejmastnak.com/tutorials/vim-latex/intro/> and might sharpen
the LaTeX saw a little bit this morning before I dive back into stuff.  I think
I'm pretty invested in LaTeX at this point, and aside from the snippets thing
I use almost everything there already, so it might be a good effort/reward
ratio.

Went through the first part, about snippets.  After some ridiculous yak shaving
(apparently the obvious, reasonable directory name `snippets` is special-cased
to be parsed as some *other* snippet plugin's syntax and so if you dare to name
the directory the obviously correct name it'll fail with a completely
inscrutable error) I got it working.  Going to have a go and see if it's worth
adding snippets back into my life, at least for LaTeX — I haven't really used
them since the Textmate era.

Journal club class.  Paper was about deep learning for EEG data.

## 2024-02-22

BS522 in the morning.

BI529, about Markov chains.  I've done these before so today was pretty basic.
Played around with some Python syntax to see if I could golf things down a bit.

Finished up the BS522 and BI545 homeworks, no idea why it felt like pulling
teeth this time — they (mostly) weren't as bad as the previous ones.

Also finished BI529 code (still need to do the writeup).  Ended up being pretty
easy overall, a lot more straightforward than the previous homework, which was
nice.

Finally got irssi set up on my new laptop.  It's been months, I should have done
this before now.  Oh well, at least it's done.

## 2024-02-23

Cleaned up and submitted BI545.  Going to review later today with folks and
maybe resubmit, but at least there's something up there now in case I forget.

BI545, this time about ATAC-seq.  I feel like it was a good introduction to the
assay, but am cautious about how in-depth the labs/etc will go.

Journal club review.  Last one for me, so I'm done with the reviews for the rest
of the semester, which is nice.

Office hours to try to understand what the 545 homework wanted after submitting.
I still have no idea if I was correct.  Oh well.

Finished BI529 so I don't have to worry about it over the break.
