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

## 2024-03-28

BS522.

BI529.  Finished the in-class stuff pretty early (basic distance computation
stuff) so I started poking around at making a little DB migration library in CL,
so I can use it for little things in the future.

Went to the tools & tech seminar to learn about HMMSTR.

## 2024-03-29

BI545.  Mostly about GWAS.

## 2024-03-31

Met with folks about the BI545 project.  Need to get my side of things done
relatively quickly because it's blocking the rest of the DAG.

BS522 homework part one.  Looks like this one is going to be another miserable
slog, ugh.

Got a skeleton of the BI545 project repo sketched out.  Threw together some
scripts to download the data, leaving it running overnight because in spite of
its name `fasterq-dump` is not particularly fast.

## 2024-04-01

The BI545 downloading finished this morning as I was drinking coffee.
Unfortunately some of the sample are single-end, which means there's one
a single FASTQ, so the downloading script (which assumed 2 FASTQs broke for
those after downloading).  But that's not too bad, because I can throw together
a one-liner to `gzip` the rest easily enough, and at least it downloaded them
all, which is the slowest part.

Started `gzip`ing the remaining data on the login node, but it's taking too long
for my linking.  `salloc`ed an interactive instance with more threads to make
this a bit faster.

Continued the BS522 slog.

## 2024-04-02

Added STAR rule to our BI545 project.  It was surprisingly difficult to find
a Singularity/Docker container for it. Eventually finished getting most of the
pipeline up and running, at least to the point of producing the `.htseq` files
so the other folks are unblocked.

## 2024-04-04

BS522.

BI529.  Clustering.

Postgres on a VM notes because I have to look this up every single time:

    sudo apt install postgresql postgresql-contrib
    sudo -u postgres psql

    CREATE USER testuser;
    CREATE DATABASE testdb;
    ALTER USER testuser WITH ENCRYPTED PASSWORD 'pass';
    GRANT ALL PRIVILEGES ON DATABASE testdb TO testuser;
    \c testdb
    GRANT ALL ON SCHEMA public TO testuser;

    psql postgresql://testuser@localhost:5432/testdb

## 2024-04-05

Realized I can bind a key to toggle fullscreen windows on StumpWM.  Amazing.
I should have done this ages ago.  `H-0` on the keyboard (mnemonic: "zero other
things on the screen") and `s-12` on the Gamer Mouse™.

BI545, eQTL and allelic bias analysis.

## 2024-04-07

Finished BI529 homework.

## 2024-04-09

BS522.

Finished and submitted BI529 homework, the last one I *technically* need to do,
since the other two classes are drop-lowest and I'm happy with all my current
scores.  We'll see how ambitious I feel.

Really need to update my `st` installation at some point.  I hear there have
been performance improvements since I last updated… looks like four years ago?
But updating `st` is such a miserable fucking slog because of the absolutely
unhinged approach they take to configuration of "edit the C code and recompile,
lol", so you need to maintain patch stacks and constantly remerge them to stay
up to date.  Absolutely batshit behavior.  I need to write my own goddamn
terminal some day.

I tried just pulling and merging but of course that doesn't fucking work because
there are a million conflicts from the various patches.  So I need to figure out
what I need to recreate on the new `st` version:

* My config changes.
* Scrollback patch.
* "Fix keyboard input" patch.
* Externalpipe patch.
* Boxdraw patch.

BI529, gene set enrichment analysis.  I think I kind of understand the GSEA
plots now, in a handwavey way.

Added a couple of simple tests to DBvolve so I can at least sanity check things
when I make changes.  Just uses an in-memory SQLite DB for the tests for now.

Started reading the paper for journal club class tomorrow.  I think this is the
final one.

PIBS800.

## 2024-04-10

Final journal club of the semester today.

## 2024-04-11

BS522.

BI529, mass spec stuff and discrete Fourier transform.

## 2024-04-12

BI545 flex time appointment thing today.

Worked on getting QoRTs running again:

* Previous runs exploded with a mostly-useless error about a GTF line having
  too few columns.
* Tried rerunning with an Ensemble GTF instead of one from NCBI and it seems to
  work.
* Had to explicitly tell QoRTs to use more than 1GB of memory (lol), by passing
  the typical Java `-Xmx` option as an option to the shell script, which does
  some magic garbage to extract it out and pass it separately to Java.
* There are options for number of threads for QoRTs but they're marked as
  deprecated because Threading is Hard, so I guess it'll just be single-threaded
  all the way.

## 2024-04-15

Started writing out a methods section for BI545.  I'm quite ready to be done
with this class.

Met with 545 folks.

## 2024-04-18

Emailed some folks about BIDS-TP.

## 2024-04-19

Finally turned in the 545 project.  One less thing to worry about.

## 2024-04-22

Added a `--slurp` kludge to CACL so I can use it for easy math.  For some reason
when I use `/dev/tty` as the input I end up having to `c-d` twice to exit the
REPL, but I can't be bothered to dig that rabbit hole apart today, so whatever,
it's fine for now I guess.  The joys of personal software.

Starting all the paperwork to join the lab for the rest of my PhD.  Exciting!

## 2024-04-23

Practiced the 545 presentation a couple more times and got it down to under
2 minutes.  I wish I could update the presenter notes, but sadly that's not an
option.  Oh well.  Presentation went fine.

Did the BS522 final.  3/25 questions were just… wrong on the test.  Got an email
hours later acknowledging that but yeah, that fits overall with this course.  At
least I'm done with it now, thankfully.

## 2024-04-24

Did the second (easier) half of the 529 homework.  I'm realizing now that we
were probably supposed to pass a locals dict in the lab instead of creating
local variables and rawdogging the rules with `eval` to mutate the state,
whoops.

## 2024-04-25

Realized UM students can get a free Yubikey from the university tech shop, so
I picked one up today.  Nice.

Almost had a heart attack when the GSI for 529 emailed about the homework being
due in 1 hour.  The assignment page had "Available until (later date)" as the
first words under the assignment and my brain parsed that as the due date, when
the due date was listed later, so I almost completely skipped it.

## 2024-04-29

Helped someone debug how to upload stuff to an external service via Great Lakes
which was an interesting rabbit hole to go down.  Gonna port the notes here for
my future self because I'm sure I'm going to have to do something like this at
some point.

The first layer of problem is that the Great Lakes slurm nodes can't access the
internet by default. <https://arc.umich.edu/document/internet-from-nodes/> has
some notes on why this is the case.  So we need to use one of the workarounds on
that page, but which one you need starts bumping up against the next layer of
problems.

The recommended upload method for what they were looking at was `ncftpput`,
which is using FTP, which is notorious for being a weird pain in the ass of
a protocol because it uses multiple TCP connections on different ports to
transfer shit instead of just using a single connection like… everything else.
So using FTP here would be even more painful because we'd need to deal with
wrangling multiple ports/connections on the slurm nodes, which is not great.

Luckily SFTP is also an option in this particular case.  SFTP is probably going
to be easier here because it only uses a single connection/port.

Side note: there's `/etc/profile.d/http_proxy.sh` on the cluster, but that just
sets some environment variables for HTTP-based proxies.  `ncftpput` explicitly
says it cannot use these in its `firewall` file, so that doesn't help.

So step one is to use the final workaround in that ARC document to set up
a tunnel to the server on the slurm node, then point SFTP at that.  According to
that document you can do that with something like this:

    ssh -o HostKeyAlgorithms=ssh-ed25519 \
        -NAL 9922:sftp-private.ncbi.nlm.nih.gov:22 \
        greatlakes-xfer.arc-ts.umich.edu \
        &

But if you actually *try* that you immediately hit a problem that they just
kinda… ignore? in the document.  SSH prompts you to check the host key
fingerprint the first time you log in, which is done interactively and can't
happen when it's backgrounded with `&` like that.  So we need to run `ssh -o
HostKeyAlgorithms=ssh-ed25519 -NAL 9922:sftp-private.ncbi.nlm.nih.gov:22
greatlakes-xfer.arc-ts.umich.edu` once interactively and accept the host key by
hand which will store it in `~/.ssh/known_hosts`, then just `^C` it.  Then (as
long as they don't change the keys) we never need to do that again.

As for the `HostKeyAlgorithms` crap, that's yet another snag.  ARC also keeps
a list of known host fingerprints for the Great Lakes hosts in something like
`/etc/ssh/ssh_known_hosts` (which is good).  SSH will check that these
fingerprints are valid when you connect (also good).  But SSH supports multiple
key formats, and they've configured the ssh server on the `greatlakes-xfer` host
to prefer to send one format, but they've listed a different one in their
`ssh_known_hosts` (I have no idea why they would do this, it's probably an
oversight?).  So `-o HostKeyAlgorithms=ssh-ed25519` will tell SSH to prefer that
format of key, which matches what's in `/etc/ssh/ssh_known_hosts`.

Okay, so at this point we need something like this:

    #!/bin/bash

    #SBATCH lines here…

    set -euo pipefail

    # https://arc.umich.edu/document/internet-from-nodes/

    ssh -o HostKeyAlgorithms=ssh-ed25519 \
        -NAL 9922:sftp-private.ncbi.nlm.nih.gov:22 \
        greatlakes-xfer.arc-ts.umich.edu \
        &

    sleep 5

    # Actually upload the files here

    kill %1

And now we can finally get to the internet from the slurm node.

We want to use `sftp` to upload by logging in with `sftp` and running something
like:

    cd uploads/somedir
    mkdir new_thing
    cd new_thing
    put /path/to/data

First snag: we want to upload an entire directory, so we probably need `put -r`
to recursively do that.  It's probably also worth adding `-a` to make it
resumeable:

    cd uploads/somedir
    mkdir new_thing
    cd new_thing
    put -ar /path/to/data

But we don't want to have to interactively type the commands here since it's in
a script.  `sftp` has a `-b batchfile` option where you can put those commands
into a file and read it in, e.g.:

    sftp -b commands.txt user@host

We could do it that way, or use bash process substitution to fake a file without
actually creating one:

    sftp -b <(echo "
    cd uploads/somedir
    mkdir new_thing
    cd new_thing
    put -ar /path/to/data
    ") user@host

Since we're using a tunnel instead of connecting directly to the server, we tell
`sftp` to connect to that:

    sftp -P 9922 \
         -b <(echo "
    cd uploads/somedir
    mkdir new_thing
    cd new_thing
    put -ar /path/to/data
         ") \
          someuser@localhost

But there's one more snag: entering the password to the SFTP server.  For that
there's a handy utility called `sshpass` that's already installed on the
cluster:

    SSHPASS="mypassword" sshpass -e \
        sftp -P 9922 \
             -b <(echo "
    cd uploads/somedir
    mkdir new_thing
    cd new_thing
    put -ar /path/to/data
             ") \
              someuser@localhost

Could also stick the password into a text file (probably with `600` permissions
for safety) and use `sshpass -fpassword.txt` instead of an environment variable
to avoid including it in the script.

I think that's all the layers of the onion, so the final script would look
something like this:

    #!/bin/bash

    #SBATCH …

    set -euo pipefail

    # https://arc.umich.edu/document/internet-from-nodes/

    ssh -o HostKeyAlgorithms=ssh-ed25519 \
        -NAL 9922:sftp-private.ncbi.nlm.nih.gov:22 \
        greatlakes-xfer.arc-ts.umich.edu \
        &

    sleep 5

    # Might be safer to use the file-based mode for sshpass with sshpass -fsomefile
    SSHPASS="mypassword" sshpass -e \
        sftp -P 9922 \
             -b <(echo "
    cd uploads/somedir
    mkdir new_thing
    cd new_thing
    put -ar /path/to/data
             ") \
              someuser@localhost

    kill %1

Whew.

## 2024-05-01

Final day of rotations.  It's been wonderful — I would have *loved* to have
something like this on the industry side (on both sides of the hiring process).

## 2024-05-06

First day at my permanent lab.  Time to get back into the swing of things.  Lots
of paperwork and notes rereading today, I think tomorrow will probably be more
actually-productive.

Did a little more Lisp web stuff after work.  Tried cl-who for a template
library in this one because I don't really like Djula and it has zero
dependencies, but… I still don't like it.  The syntax for flipping back and
forth between Lisp and HTML is annoying, the macro-based-everything makes it
a pain in the ass to extract helper functions, and it'd be utterly inscrutable
to any non-Lisper.

## 2024-05-07

Did a bit more Lisp web stuff after work.  Tried out
<https://github.com/mmontone/ten> and while I don't *love* it I think it's what
I'll go with for now.  It has more dependencies than cl-who (including cl-who
itself, lol) but not *that* many, so I think I can live with that.  The tags are
pretty much vanilla lisp which is a lot less janky than Djula's tags, and the
templates are at least closer to something a non-lisper might be able to read.
The non-automatic compilation step is annoying, but I can probably hack a Vim
shortcut to get something usable there.

## 2024-05-08

Wrote a little wrapper script to ensure my paper database from JabRef is backed
up, because at this point it would be catastrophic to lose it, and while
Syncthing has been… okay so far, I don't fully trust it yet.

Fixed a [Vlime/Paredit bug](https://github.com/vlime/vlime/issues/54) that's
annoyed me for *checks github issue timestamp* four years.  I should have done
this ages ago, I don't know why I never bothered to look into it.

## 2024-05-09

Started trying to figure out how I want to organize all my PhD-related files for
the next five years.  I've tried [Johnny Decimal](https://johnnydecimal.com/) in
the past and used it for a while, but never really felt like I really got into
it.  Maybe I should resurrect that and try to focus it more on just my PhD,
instead of trying to track my entire life through it.

## 2024-05-13

Got some Sundew cuttings from a labmate today, going to try propagating them at
home.

## 2024-05-14

Wanted to deal with error handling and trailing slash redirection in Hunchentoot
today, but unfortunately it looks like there's no easy way to do either (at
least not one that's documented).  Hunchentoot allows you to specify some kind
of error directory, but that only allows static templates, not e.g. rendering
a template.  Though maybe that's good enough for what I need…

## 2024-05-15

A little more web stuff, pretty happy with my choice of templating library
(TEN).  Now that I grok that it's mostly just the lisp with a tiny syntax
wrapper, it's trivial to just do e.g.:

    {% multiple-value-bind (foo bar) (get-stuff arg) %}
        …
    {% end %}

I'm still not happy with the routing library situation.  Looked at a bunch of
different options and none of them seem decent.  The one I'm currently using
(easy-routes with Hunchentoot) doesn't really give me a nice way to deal with
rendering error pages, or a way to add middleware to e.g. handle trailing slash
crap site-wide.  Need to think more about how I want to deal with this.

## 2024-05-30

Updated my Mercurial hosting site to enable archive downloads.  Notes for my
future self:

* Use `man 5 hgrc` and search for archive for the settings.
* The `hgweb.conf` you need to edit is inside the `hg.stevelosh.com` deployment repo.
* The deployment repo and the public repo are not the same.
