This is my personal notebook where I dump thoughts and notes for my future self.

**I make no guarantees about the accuracy of anything in here.  Read at your own
risk!**

[TOC]

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

## 2024-03-20

In the lab most of today except for journal club at 3.

Watched the (very short) BI529 video for tomorrow.

BI603.

## 2024-03-21

BI529, multiple sequence alignment.

Wanted to clean out my downloads folder, but haven't gotten around to getting
a nice graphical file manager on this laptop.  Decided to try out `ranger` and
it was… fine.  `space` to mark files, then `:delete` to remove them.  Previews
are ugly but usable.

## 2024-03-22

BI545, this time about single-nuclei 10x Multiome.  Lab is at
<https://theparkerlab.med.umich.edu/data/porchard/2023-03-02-multiome-lab/multiome-lab.html>,
and there's a  Nextflow workflow at
<https://github.com/porchard/snATACseq-NextFlow/blob/master/main.nf> which might
be worth looking at if I ever decide to use Nextflow again.

Found <https://pair-code.github.io/understanding-umap/> and
<https://distill.pub/2016/misread-tsne/> again which I came across years ago
when working at 10x, read through it because I remember them being useful back
then.

Lunch with some CMB/BI folks.

Finished reading through the 545 lab after meeting.

## 2024-03-24

BI545 and BS522 homework.

## 2024-03-25

Looked for a way to queue up commands to run serially.  Initially found a bunch
of people recommending `at` and `batch` which absolutely do not do that, cool.
Eventually I found `nq` (<https://github.com/leahneukirchen/nq>) which uses
a cute and/or horrifying strategy (the process backgrounds and hangs `flock`ed
on sequential sentinel files, lol), so I'll give that a try.  For example, to
`curl` whatever's on your clipboard, something like this (in bash) can work:

    X=`pbpaste` nq -c bash -c 'curl --remote-name -L "$X"'

The `pbpaste` evals immediately, and the string it produces is used later when
actually running, which is what you want.  Neat.

## 2024-03-26

BS522.

BI529.  Tree search. Implemented DFS and BFS PAIP-style for fun, then also did
them the way they wanted.

BI545, initial presentations.  All but one group came in under time, thankfully,
so it wasn't too painful.

PIBS800.  Part 2 of how to give a talk.

## 2024-03-27

BI603.
