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

## 2024-03-04

Back in Ann Arbor.  Need to get in touch with the 545 group so we can get the
project started.

Watched the (cringey) videos for 504.

## 2024-03-05

BS522 in the morning.  Need to do the test (tomorrow).

BI529.  Talked about Viterbi.  Need to sit own and work through this on my own
time to make sure I really grok it.

Did Viterbi after lunch.  Was pretty straightforward.

PIBS800.

No BS522 lab today.

## 2024-03-06

Went to watch the videos for BI529 but it looks like there aren't any for
tomorrow, so I guess I'm all set there.  Cool.

Added link title/slug indexing into `mw`.  I think with that added I might be at
the point where I can start dogfooding this thing.  Neat.

## 2024-03-07

BI529.  HMM forward/backward.  Easy to implement, but I'm not 100% sure I grok
where this is going.  I ordered the textbook from the 90s they mentioned for $6
used, so maybe that'll help.

Really need to set up an IRC bouncer so I don't lose chat history.  Looked
around online and found a couple, [pounce][] seems promising, but annoying to
install due to its extreme BSD sporkiness.  Poked around a little bit and
I think I've managed to get it running by:

* `apt install git build-essential openssl libssl-dev pkg-config`
* Download a `libtls` release tarball (*NOT* LibreTLS, which is a different
  thing, jesus).
* `./configure; make all; sudo make install` for `libtls`.
* Run `/sbin/ldconfig` to pick up the new library.
* Clone `pounce` repo.
* `./configure; make all; sudo make install` for `pounce`.

Now I need to figure out how to configure the thing and install TLS certs and
shit for it, but at least it's built.  Need to get this Ansibilized at some
point too.

[pounce]: https://git.causal.agency/pounce/about/

Fuck it, let's just do it.  Ansibilized most of the setup, except for the
installation described above.  I'm also not 100% sure I've done the dehydrated
TLS cert shit which is always miserable.  But it seems to work, for now.

PIBS504 ethics class 1 of 2.

## 2024-03-08

BI545.  Jumped right back into the gene set enrichment with no context, and
I was pretty lost.  I think eventually I managed to orient myself.  Walked
through the labs, lots of going through the motions without grokking what I was
actually doing, but I think I managed to get through it successfully eventually?

Printed papers to read this weekend for my fourth and final rotation.

## 2024-03-10

Finished BI545 homework 4.  Was meh, though not as bad as the previous ones.

Read some papers for rotation tomorrow.  Lots of new stuff to learn again, I'm
looking forward to diving in.

## 2024-03-11

First day of my final rotation.  Looking forward to trying something new
(again).

Filled in some sections for the 545 group project proposal.

## 2024-03-12

BS522.  Model selection.

I really need to get back to the APL videos now that the April author has fixed
the bugs I reported.

BI529.

BI545.

Printed the rest of the journal club papers so I don't have to do it for the
next month.  Read the journal club paper for tomorrow (mostly).

PIBS800.

BS522 lab.  Over really quick today.

## 2024-03-13

Must have left my wireless mouse somewhere, need to try to find that today…

Needed to update R to deal with bioinformatics backwards-incompatibility
garbage, the instructions at <https://cran.r-project.org/bin/linux/debian/> were
helpful.  General process was:

1. Add the GPG key for their Debian repo.
2. Add the repo line to `/etc/apt/sources.list`.
3. Update through `apt`.

That worked okay.  Then I had to update bioconductor to *its* latest version,
`BiocManager::install(version="3.18")`.  Took a long time, but it seems to have
worked.

That, of course, broke my nvim-r setup, because it started complaining about
`nvimcom` not being available for this version of R.  Eventually I was able to
install the `nvimcom` thing from the `nvim-r` repo by running
`install.packages("devtools")` and then inside `nvim-r/R/nvimcom` running
`devtools::install_local()`.  This *seems* to have worked and unfucked
everything, though I have no confidence that I haven't broken other things in
the process.  R packaging does indeed seem to be pretty hellish, as I've heard.

Found the mouse in BI545 class, thankfully.  Now that I think about it, it's
probably worth buying a second copy of my Gamer Mouse™ at home to leave at the
lab.  Attempted to do so and found that it's been recently discontinued, so
I have to pay a premium but thank god I can still find one.  The hamster wheel
of backwards incompatibility turns ever on, even in the real world, I guess.

Journal club class.  Another machine learning tool for scRNA-seq.

Watched 529 video for tomorrow.  Guess we're starting on Profile HMMs.

## 2024-03-14

BS522, over Zoom today.

BI529, profile HMMs.

Final PIBS504 session.

## 2024-03-15

Had to use the core-imaged machine they gave us today (haven't used it since
the awful word doc writing for HG545).  Took minutes to boot, then complained at
me to update teams (I've never used Teams on that machine).  Then complained at
me to reboot, and when I said "Okay, reboot" it threw an "Error: can't reboot",
so I clicked start → reboot and it rebooted.  Jesus.  I guess I'll remember this
the next time Linux does something dumb.

BI545.  Lecture was on single cell data and ways to "integrate" it (I think this
just means ways to take multiple data sets and compare/contrast them, but it
wasn't super well defined).  I mostly followed the general ideas, but there were
a lot of biology terms thrown in that weren't defined (although hey, I actually
did know what an astrocyte already is thanks to my rotation) and a lot of math
notation that was passed over too fast to really grok.

## 2024-03-17

BI545 homework today, mostly implementing Baum-Welch.  Looked around for some
resources on this, found <https://www.youtube.com/watch?v=JRsdt05pMoI> which
really helped clarify the meaning of the forward/backward/forward-backward
values in my mind:

* Forward (called α in the video): given the sequence we've seen so far, what's
  the probability we're in this state?  In their robot example, if I see blue
  carpet I know I'm probably in my bedroom or den.
* Backward (called β in the video): given the sequence we're *going to see*,
  what's the probability we're in this state?  Continuing the example, if the
  next state is a red rug I know I'm in the living room or the bedroom.
* Forward-Backward (called γ in the video): combine both forward and backward (α
  and β) to find the most likely state.  In the example, α says bedroom or den
  and β lets me rule out the den.

## 2024-03-18

Going to see if I can get Mutt set up on this machine again.  Installed mbsync
(the package is named `isync`, sigh) and neomutt via apt.  Started syncing my
mail down with `mbsync --all --pull`.  Need to grab the config files from my
other laptop when I get home (or set them up to sync).

Fixed an old blog entry of mine when someone pinged me in IRC.  I'm *so* glad
I rewrote my blog to generate it myself with Common Lisp.  I haven't touched it
in forever, but everything Just Worked on the new laptop immediately with no
fucking around on the HWoBI.  So nice.

Watched BI529 videos.  Going to be moving to pairwise alignment.  I swear I've
done Smith-Waterman in the past, but looking around all I can find is an
implementation of Needleman-Wunsch in my sandbox repo.  Maybe that's what I'm
thinking of.  Oh well, at least I've done something like this before.

## 2024-03-19

BS522.

BI529.  Smith-Waterman.  Finished relatively quickly, but the most confusing
part was which sequence was "seq1" vs "seq2" and matching that to row/col.

BI545.  Mostly about spatial today.  Already seen a lot of this from working on
Xenium at 10x.

Since my second `G A M E R M O U S E` arrived yesterday I decided to some up
with some key mappings for non-gaming use, so I don't have to swap back and
forth as often during daily driving.  In the process I got tired of my StumpWM
config being one giant file, so I decided to shave that yak first and split it
up a bit.  I started by just splitting into files, but after reflection
I decided to make it a full ASDF system called `stumpconfig` to make it play
more nicely with the rest of Quicklisp.  Hopefully it'll also help the loading
times, since it won't have to recompile everything every time I change (though
`:serial t` might be preventing some of the optimization here).

Hopefully I haven't completely fucked my Stump setup with this — need to try
restarting X to make sure it still cold boots… yep, seems okay.

PIBS800.

Did some more StumpWM yak shaving between classes, fixing up broken mode
line/sensor support, etc.
