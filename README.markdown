This is my personal notebook where I dump thoughts and notes for my future self.

**I make no guarantees about the accuracy of anything in here.  Read at your own
risk!**

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

Then <https://localhost:8384> to access the admin.

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

## 2023-08-31

BS521 this morning.  Still pretty straightforward.

Going to create a separate note repo for lab notes, so I can take those
privately.  I'll still put public notes here, but for certain things (e.g. DB
table names, etc) I don't want to have to worry about which are okay to make
public.

Going to port the abortive attempt at a Zettelkasten into here in no particular
order (thank god for `grep`).  Should have done this earlier but it's been
a hectic couple of days. Should I use heading more in this .plan for folding
purposes?  Maybe. I still need to finish going through my fleeting notes that
I've got so far and getting them in here.  I also should have already done this,
but I'll do that this weekend when I have some free time and try not to let it
pile up so much in the future.

### Short-Read Sequencing

Short-read sequencing aims to sequence long stretches of DNA (or RNA) by first
fragmenting them into small pieces, sequencing those pieces separately (usually
in parallel, for speed), then reassembling the fragments into contigs
computationally.

There are several forms of short-read sequencing, but the most popular by far
today is Illumina's sequencing by synthesis approach.

Short-read sequencing is often used for whole-genome sequencing.

The cost of sequencing, especially short-read sequencing, has fallen
*dramatically* in the past 20 years, which has started to enable its use as
a clinical tool.  It was impractical to sequence someone's genome to learn about
their health when it cost $1 billion, but it is much more reasonable to do it
when it costs $1,000.

### Whole-Genome Sequencing

Whole-genome sequencing refers to sequencing an organism's entire genome,
instead of just a limited part of it.

This has the benefit of letting you get data on *all* of the genome at once,
without having to know what you're looking for in advance.  But if you *do* know
what you're interested in, it can be much faster/cheaper to sequence just that
part (or can give you deeper coverage for the same cost).  Like many things in
science and engineering, it's a tradeoff.

### Fragmentation

When sequencing DNA or RNA with short-read sequencing like Illumina, the strands
of nucleic acid need to be fragmented into shorter pieces.  This usually happens
in one of a few ways:

* Mechanical fragmentation by forcing it through a small passage
* Enzymatic fragmentation
* Sonication

### Sequencing Alternatives

Although sequencing costs have fallen dramatically in the past 20 years, they
are not completely free.  There are several alternatives to sequencing that are
still used for a number of reasons:

* They can provide the information more cheaply than sequencing.
* They can provide much deeper coverage than would be practical to get by sequencing.
* They can be done much faster than sequencing, allowing for rapid diagnostic use.

Some examples of alternatives are:

* Microarrays
* Nanostring
* qPCR
* Optical mapping

### Post-Transcriptional Modification

After RNA is transcribed from DNA, but before it goes on to do its actual job
(being translated into protein, or doing something on its own), it is sometimes
modified.  There are a number of modifications that happen, some of the most
common are:

* Splicing out introns.
* Polyadenalation of the 3' tail.
* Adding a 5' cap.

### Post-Translational Modification

After RNA is translated into protein, but before the protein begins to do its
intended work, it is sometimes modified.  Modifications come in many forms and
can affect the terminal ends or one of the amino acid side chains.  One common
modification is phosphorylation.

### Chromatin
 
Chromatin structure varies in the genome.  Chromatin that is uncoiled and
available for work is euchromatin (eu = useful).  Chromatin that is tightly
coiled and not accessible for transcription is called heterochromatin.
Heterochromatin has two sub-types of its own:

* Facultative heterochromatin can temporarily become euchromatic.
* Constitutive heterochromatin is always condensed, and is usually found in
  repetitive sections of the genome.

[ATAC-Seq](https://en.wikipedia.org/wiki/ATAC-seq): "Assay for
Transposase-Accessible Chromatin using sequencing" is used to determine which
parts of the genome's chromatin are accessible (and, implicitly, which are not).
It uses a mutant, hyperactive transposase to insert sequencing adapters
*everywhere* it can inside the genome.  Those tagged fragments are then
extracted and sequenced.

[ChIP-seq](https://en.wikipedia.org/wiki/ChIP_sequencing):
"Chromatin-immunoprecipitation sequencing" is used to determine which parts of
genome particular proteins are interacting with, e.g. where a particular
transcription factor is binding to in the genome.  The steps are roughly:

1. Crosslink the DNA and proteins to lock them together, so the protein can't
   unbind from the DNA (usually using formaldehyde).
2. [Fragment](n/fragmentation.md) the DNA into small (~500bp) fragments.
3. Use immunoprecipitation to extract only the proteins you are interested in
   (antibodies that bind to your protein of interest).
4. Unlink the DNA and proteins, extract the DNA, and sequence it (e.g. with
   Illumina).

The resulting reads will be regions where the protein of interest was originally
bound to the DNA, allowing you to see (roughly) where a particular protein
interacts with the genome.

### Homopolymer

"Homopolymer" when used in the context of sequencing means a sequence of the
same base repeated, e.g. `AAAAA` or `CCC`.

Many sequencing technologies have trouble with these kinds of sequences.  For
example, Oxford Nanopore sequencing uses the properties of the bases currently
inside the pore to determine the bases that enter/leave. But for homopolymers
it's hard to tell when one enters and another leaves if they're completely
uniform along the entire pore.

### Long-read sequencing

Long-read sequencing is a relatively new branch of technology that allows for
sequencing much longer reads than e.g. Illumina.  This is useful because many
parts of many genomes have regions that are difficult for short-read sequencing
to deal with, e.g. repetitive elements and high-level structural variation.
Long-read sequencing can help assemble those sequences which would be difficult
to piece together from short reads.

### Oxford Nanopore Technologies

A long-read sequencing technology that can be used to directly read a strand of
DNA using a molecular pore that produces current as DNA passes through it.  The
variations in current can be recorded and processed to determine the DNA
sequence being passed through.

          ---,
              \
               \
                ===============  DNA helix
               /
              /  ssDNA (unwound)
             /
           ( | )
           ( | ) motor protein
           ( | )
          [  |  ]
          [  |  ] pore for sensing DNA
          [  |  ]
          [  |  ]
          [  |  ]
    ______[  |  ]__________________________
             |
             |
           vvvvv  DNA is fed through the pore by the motor protein and current (picoamps) measured

ONT units are available as small devices that connect to a USB port on a laptop,
which makes them much more portable than other sequencers (though the library
prep equipment is not as portable, yet).

### 10X Genomics Linked Reads

A form of synthetic long-read sequencing from 10X. Long DNA fragments were
loaded into gel beads with barcodes.  They were then fragmented and barcoded,
then sequenced on a normal sequencer.  The barcodes allowed you to know which
short reads came from the same longer fragment (i.e. were "linked"), which helps
reconstruct the longer fragments from the short ones.

We discontinued this product while I was working at 10X.  RIP.

### Non-uniform genotypes

An organism is a **mosaic** if it has cells with different genomes that stem from
a somatic mutation in one of the ancestral cells, which then divided and
resulted in a chunk of the organism having the mutation while the rest does not.

An organism is a **chimera** when it has cells with different genomes that are
caused by multiple zygotes combining early in development.  The resulting
organism will have cells with completely different genomes depending on which
zygote they trace their ancestry back to.

### Kaelin 2017

Read this paper from intro materials.  Main thrust was about broad vs narrow
claims in papers.

Scientific papers make and justify claims using evidence.  Papers vary on how
many claims they make, and how well-supported each of those claims is with
evidence in the paper.

Because scientists have limited time and papers must be a finite size, there is
almost always a tradeoff between making a broad set or a narrow set of claims:
more claims will generally mean less evidence to support each claim.

The author claims that in biomedical research there is a growing trend toward
requiring papers with broader and more sweeping claims if you want to get
published. Reviewers want more and more claims, more "translatability" to the
real world. It is no longer enough to notice and document something is
happening, now you must also propose *why* it happens and experiment to
demonstrate this mechanism.

Requiring authors of scientific papers to make broader and broader claims in
order to get published has several (likely unintended) effects.

First, by adding more and more claims to a paper, each claim will likely have
less individual support behind it.  Instead of a few claims supported by many
pieces of evidence:

    ------- -----
     |||||   |||

papers will end up with a collection of claims, each balancing precariously on
narrow support:

    ---------  -----  ---  --- -----  ----
     |     |     |     |    |    |     ||

This harms reproducibility because claims that are not supported by a robust set
of evidence are less likely to reproduce successfully.

Broad claims are also often harder for peer reviewers to deal will -- they often
need to be an expert in multiple fields just to be able to evaluate the paper.

### Recombination

Recombination is a step that happens during meiosis where homologous chromosomes
cross over pieces of themselves, effectively swapping random chunks of their
sequences.  This provides much more genetic variation than random segregation of
chromosomes alone, allowing sexual reproduction to explore more of the genetic
space more quickly.

The number of recombination events (crossovers) per chromosome is random, but is
usually relatively low (3-5 per chromosome).

# September 2023

## 2023-09-01

HG545.  Looked over the slides last night and was a little worried, but felt
okay after the lecture for the most part.  Still a few things I need to look up
and I do still need to get my fleeting notes into this, but I feel okay.

Continuing the Snakemake tutorial.

Threads can be specified for a given job with `threads: 8`, and you need to
propagate that to the command yourself with `{threads}`.  Will be scaled down if
run with fewer cores than threads, otherwise will wait until that many are
available.

Snakemake has some support for noticing log files, but it seems like you have to
manually create them yourself?  This seems… tedious?

    rule bwa_map:
        input:
            "data/genome.fa",
            lambda wc: SAMPLES[wc.sample]
        output:
            "mapped_reads/{sample}.bam"
        threads: 8
        params:
            rg=r"@RG\tID:{sample}\tSM:{sample}"
        log: "logs/bwa_map/{sample}.log"
        shell:
            "("
            "bwa mem -R '{params.rg}' -t {threads} {input}"
            " | samtools view -Sb - > {output}"
            ") >{log} 2>&1"

Do I really have to wrap everything in `(…) >{log} 2>&1` by hand myself?

You can get a summary of file provenance with `snakemake --summary`.  The output
is a TSV, so I went down a rathole of pretty-printing TSVs and eventually found
that `| column -s $'\t' -t` works (mnemonic: `s$tt`).  I love how every UNIX
program gets to invent its own bespoke command line interface for specifying
special characters. Really great.

Can mark outputs as `temp()` and `protected()`, which is nice.

Need to install singularity *inside* my VM:

    # Ensure repositories are up-to-date
    sudo apt-get update

    # Install debian packages for dependencies
    sudo apt-get install -y \
        wget \
        build-essential \
        libseccomp-dev \
        libglib2.0-dev \
        pkg-config \
        squashfs-tools \
        cryptsetup \
        runc

    # Install Golang
    export VERSION=1.21.0 OS=linux ARCH=amd64 && \
        wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz && \
        sudo tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz && \
        rm go$VERSION.$OS-$ARCH.tar.gz

    echo 'export PATH=/usr/local/go/bin:$PATH' >> ~/.bashrc && \
        source ~/.bashrc

    # Install Singularity
    export VERSION=3.11.4 && \
        wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-ce-${VERSION}.tar.gz && \
        tar -xzf singularity-ce-${VERSION}.tar.gz && \
        cd singularity-ce-${VERSION}

    ./mconfig && \
        make -C builddir && \
        sudo make -C builddir install

## 2023-09-02

It is time to shave the LaTeX yak again. Installed it with `texlive-latex-base`
to start, we'll see if I need to add some more crud in later. Going to go
through some guides for now.

Going to note some things to remember.  Skeleton of document:

    \documentclass{article}
    \begin{document}

    Basic text.

    \end{document}

Math:

    Inline math $y = 3 \sin x$ example.

    Block equation:
    \[
            y = 3 \sin x
    \]

    With reference:
    \begin{equation}\label{equa}
        y' = 3 \cos x
    \end{equation}
    refer to it by label, e.g. equation (\ref{equa}).

    More complicated: $x^2$ and $x^{2+\alpha}$ and $y_{n+1}$.

Verbatim:

    Verbatim text: \verb"$x^{2+\alpha}$".  Delimiter can be anything ala sed,
    \verb_%%&_ or \verb+$$+.

    Must escape special characters \&, \$, \%, \_, \{, \}, and \#.

    \begin{verbatim}
    A whole verbatim region.

    (defun square (x)
    (* x x))
    \end{verbatim}

Comments:

    Comments exist.  % This is a comment.

Type styles:

    Shapes:
    \textup{Upright}
    \textit{Italic}
    \textsl{Slanted}
    \textsc{Small}

    Series (weight):
    \textmd{Medium}
    \textbf{Boldface}

    Families:
    \textrm{Roman}
    \textsf{Sans}
    \texttt{Typewriter}

Emphasis:

    \emph{Never} do Foo!

"Environments" are sections that are treated differently, made with `\begin{…}`
and `\end{…}`.

Lists:

    Unordered list:
    \begin{itemize}
        \item Foo
        \item Bar
        \item Baz
    \end{itemize}

    Ordered list:
    \begin{enumerate}
        \item One
        \item Two
        \item Three
    \end{enumerate}

    Customizable labels:
    \begin{description}
        \item[Rule 1.] Foo
        \item[Rule 2.] Bar
        \item[Rule 3.] Baz
    \end{description}

Sizes (note the brace comes BEFORE the command!):

    {\Huge Huge}
    {\huge huge}
    {\LARGE LARGE}
    {\Large Large}
    {\large large}
    {\normalsize normalsize}
    {\small small}
    {\footnotesize footnotesize}
    {\scriptsize scriptsize}
    {\tiny tiny}

Centering:

    \begin{center}
        {\large\textbf{Assignment 1}}\\% The \\ linebreaks.
        Steve Losh\\
        BS521
    \end{center}

Example table.

    \begin{tabular}{l|rc} % lrc = cols should be left, right, centered, pipe for vertical line
        Name & Mark & Grade \\
        \hline\hline
        Foo & 99 & A+ \\
        Bar & 51 & C  \\
        Baz &  5 & F
    \end{tabular}

Colspan with multicolumn command.

    \begin{tabular}{|l||r|r|}
        \hline
            & \multicolumn{2}{c|}{Grades} \\
                \cline{2-3}
        Name & Class 1 & Class 2 \\
        \hline\hline
        Foo & 99 & 88 \\
        Bar & 51 & 65  \\
        Baz &  5 & 58 \\
        \hline
    \end{tabular}

Full example, with referencing and caption, e.g. `Table~\ref{tab:a} on page~\pageref{tab:a}`.

    % b = try to put at Bottom.  Also t top, h here, p separate page.
    % Can do multiple in order of preference.
    % [!t] ! = try harder
    \begin{table}[b]
        \begin{center}
            \caption{An Example Table}
            \label{tab:a}

            \begin{tabular}{lr}
                Name & Value \\
                \hline
                Foo &  1.0 \\
                Bar & 15.9 \\
                Baz &  6.2
            \end{tabular}
            % \caption{Caption at the end works too.}
        \end{center}
    \end{table}

Sections:

    \section{Some section} % includes numbering
    \subsection{Some subsection}

    \section*{Some section} % no numbering
    \subsection*{Some subsection}

Quotation marks (hilarious):

    `Single quoted'
    ``Double quoted''

Change overall text size (simple):

    \documentclass[11pt]{article} % only valid sizes are 10/11/12.

Palatino instead of Computer Modern:

    \usepackage{mathpazo}
    \linespread{1.05}         % needs more leading (space between lines)
    \usepackage[T1]{fontenc}

Vimtex stuff:

* Close thing with `]]` in insert mode.

Got about that far, which was enough to start my BIOSTAT-521 homework.  Will dig
in again later, but it's nice to be able to use it for something real to
practice.

Puttered around a bit looking at other fonts, but didn't find anything new or
interesting.


