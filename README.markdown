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

Trying out syncthing as a Dropbox replacement.  Installing:

    sudo apt install syncthing
    systemctl --user enable syncthing.service
    systemctl --user start syncthing.service

Then <http://localhost:8384> to access the admin.

Got my budget scripts working and synced via syncthing (also shaved a couple of
yaks by making scripts to archive/create new hosts while I was at it).  Seems to
work okay at the moment.  Will gradually transition other stuff over time.

Going to spend some time learning about Nextflow while I wait to hear from
rotation folks.  Nextflow is basically a DAG, where:

* Edges are FIFO queues (Nextflow calls them "channels")
* Vertices are things that consume input from their channels and produce output (Nextflow calls them "processes").

There are two types of channels.  First: queue channels: asynchronous FIFO queues.  Examples:

    # emits sequence of given values
    ch = Channel.of(1, 1, 2, 3, 5, 8)

    # emits a single file path (queue of size 1)
    ch = Channel.fromPath('data/one-single-file.txt')

    # emits multiple file paths
    ch = Channel.fromPath('data/*.txt')

Value channels: like queue channels, but just emit the same value over and over.
Basically `(constantly val)`.

Processes: basically stages of a pipeline.  Take input and output definitions,
plus something to run (e.g. `shell`).  Example after a bit of poking around:


    // allows you to define processes to be used for modular libraries
    nextflow.enable.dsl = 2

    workflow {
        ids = Channel.fromPath('data/ids.txt') // single-item channel
        chunksize = Channel.value(1000)        // (constantly 1000) but will only ever be used once here

        // The process below produces a list of outputs.  It will only ever be
        // run once, but nextflow doesn't know that -- you could potentially
        // have a process run multiple times that each produces a list.  So by
        // default it groups all the outputs into a single emitted value.  But
        // here we want to flatted [[aa ab ac ad ae]] into [aa ab ac ad ae].
        batched_ids = split_ids(ids, chunksize) | flatten
        batched_ids.view()   // .view() doesn't consume, good for debugging

        result = reverse(batched_ids)
        result.view()
    }

    process split_ids {
        input:
        path(ids)
        val(chunksize)

        output:
        file('batch-*')

        shell:
        """
        split -l !{chunksize} !{ids} batch-
        """
    }

    process reverse {
        input:
        path(batch_file)

        output:
        file('result')

        shell:
        """
        tac !{batch_file} > result
        """
    }

Nextflow seems to have the concept of a "run name", i.e. an identifier for
a particular run.  It creates a `work/` directory with the output files, but
*also* seems to splat out a bunch of hidden `.nextflow/` and `.nextflow.log.*`
files in the current directory.  `nextflow clean` removes `work` but not the
hidden files.

Can run with some basic reporting with some extra flags:

    nextflow run example.nf -with-report report.html -with-dag graph.svg

Of course there appears to be some backwards-incompatible jank in the language
already.  Reading through <https://www.nextflow.io/blog/2020/dsl2-is-here.html>
shows minor syntax changes I guess I'll need to be aware of when looking at
things a few years old.

Putting some things on the TODO list for learning mroe about nextflow:

* <https://github.com/seqeralabs/nextflow-tutorial> (uses old DSL)
* <https://carpentries-incubator.github.io/workflows-nextflow/index.html>

I also need to get some basic scratch VM infrastructure set up with qemu/vagrant
and Ansible so I can test out Nextflow/pipeline stuff without polluting my own
machines and/or any servers I eventually get access to with random testing
garbage.  Maybe I'll put that on tomorrow's list too.

## 2023-08-29

First BIOSTAT-521 class.  This one seems like it's going to be quite easy, but
given I have a crazily-hard class and lab rotation work to do, I think that's
fine with me.  It *does* use R, which will be a good excuse to poke around at
that since it's used so heavily in the industry.

First lab meeting as well.  It was good to meet everyone in person.  Talked
about scheduling stuff and overall gist of my project, though we can't move
forward directly right now while the university network is still hosed.  But
I did get some more information about things I'll want to look into:

* Snakemake (not Nextflow, oh well).
* Singularity containers (should probably read the UNIX book section on
  containerization first).
* I still want to get Vagrant/libvirt/qemu/Ansible working to make scratch envs.

Going to meet again on Thursday to see if the network is available.  If so I'll
dive in more then — until then I'll just poke around learning that stuff because
I know I'll need it eventually.

Don't have a lot of time before next class, but I went ahead and installed
Snakemake highlighting/etc for Vim.

## 2023-08-30

HG545 this morning.  Class was mostly about how to succeed in the class.

Still trying to decide on how I want to take notes while I'm here.  I read the
Zettelkasten book and was considering trying that.  But after poking around at
it I'm not sure I like the overhead of having to link everything up all the
time.  I tried creating some notes while studying and it was a pain to have to
try to link everything to something else.  Sometimes I want to just jot down
something without worrying about its place in the graph. I think I might end up
going with this current format (stream-of-consciousness .plan file style notes)
for everything, but taking a few things from Zettelkasten than might help:

* Take fleeting notes as I read.
* Turn fleeting notes into permanent ones, but as text in my .plan instead of
  linked entries in some other system.

That seems like something I might actually *do*, and hopefully with grep it'll
be good enough for what I need.

Installing JabRef to try as a reference manager.  Zotero looks nicer (no stupid
flat UI) but syncing the DB requires sending it to their web thing.  JabRef
seems to use a plain text file so I can probably just sync it with syncthing and
deal with conflicts manually.  Spent some time adding a couple of papers to it.
Not sure it's great (it got the info wrong for 2/3 papers) but I guess that's
just typical open source jankery.

Apparently you can just `C-v` a DOI into JabRef and it'll import it.  Hard to
discover, but seems to work okay.  JabRef is complaining about capital letters
in the titles but I'll figure out that jankery later.  At least I've got
something for now.

Had some wonkiness with my Syncthing budget stuff, but I think I just forgot to
reeval the location on my desktop.  Will poke around more if anything else seems
to break.

Watched some snakemake videos and read through their paper.  This smells a lot
more academic than Nextflow did, which is a little worrying.  I'm sure it'll be
fine in the end though.

Send off the rest of my VA paperwork so things can get moving on that side.

Read the ULSAH section on containers to get a high-level overview.  Started
looking into Singularity and it's already looking spicy.  Apparently the project
forked a couple of years ago and there are now two competing versions?  Great.
Also you have to install it from source, which requires installing Golang.
I thought I was free of Rob Pike's Googly Tendrils but I guess I never will be.
Installed Go, built Singularity.  At least it installs to a prefix
(`/opt/singularity`), so I can remove it easily if I want.

Poked around a little to make sure it's working, e.g.:

    singularity pull docker://debian:bookwork-slim
    singularity shell debian_bookworm-slim.sif

Seems to be working as far as I can tell.

Also installing snakemake.  Using pip with a venv for now even though the
documentation tries to convince you not to.  If anything breaks I can revisit
it, but for now it's probably fine to go through some tutorials without pulling
in some giant slab of junk.

Started going through the Snakemake tutorial.

> Since the rule has multiple input files, Snakemake will concatenate them,
> separated by a whitespace [sic]

Oh boy.

Realized I'd need to install a pile of stuff to get through the tutorial,
decided to pause and shave the qemu yak first so I can do this without dumping
a ton of stuff on my laptop.  So many yaks.

Shaved the qemu yak, now I've got a reliable VM setup.  Committed the
instructions and a tiny script to a `vms` repo so I don't have to relearn this
again.

With that out of the way, installed Snakemake and all the prereqs from their
tutorial on the VM with wild abandon.  Now I can *actually* do the tutorial.
The simple tutorial was straightforward for the most part, but for this:

    rule bcftools_call:
        input:
            fa="data/genome.fa",
            bam=expand("sorted_reads/{sample}.bam", sample=SAMPLES),
            bai=expand("sorted_reads/{sample}.bam.bai", sample=SAMPLES)
        output:
            "calls/all.vcf"
        shell:
            "bcftools mpileup -f {input.fa} {input.bam}"
            " | bcftools call -mv - > {output}"

It's not clear how the expanded input lists are ordered.  Are they guaranteed to
always produce the same order given the same input list?

Finally realized I could put my pubkeys online so I can just `curl
https://stevelosh.com/pubkeys >> ~/.ssh/authorized_keys`.  No idea why I never
though of this before now.  Also updated my site now that I've moved.  Of course
everything just worked even though I haven't touched the site in months, because
it's written in Common Lisp which never changes.  It's so nice to not have to
work with constantly-breaking shit.

Installed R and RStudio for tomorrow's class.  Base R is `r-base` in Debian.
Unfortunately Debian 12 has only been out for a few months and the RStudio
Debian package only supports 11, but apparently the `deb` one for Ubuntu 22
works so I guess I'll just yolo it with that one for now.

Reading for tomorrow's BS521 class: chapter 1 of OpenIntro Statistics (probably
also want to real Holm's stats book again as a refresher).  All pretty basic so
far.


