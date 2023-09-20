This is my personal notebook where I dump thoughts and notes for my future self.

**I make no guarantees about the accuracy of anything in here.  Read at your own
risk!**

[TOC]

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

## 2023-09-03

Spent most of today getting the reading room in my apartment ready.  Went to
IKEA, looked around a lot and got some ideas, picked up a chair and bookshelf
for my still-boxed unread books.  Not the most productive Sunday, but sitting in
my chair and reading at night felt good.

## 2023-09-04

Continuing the EdX genetics course over breakfast.

## 2023-09-05

BIOSTAT-521 and BIOINF-500 classes this morning.

Going to spend my non-class time looking into Unicycler today (and taking care
of paperwork if anything that needs my attention crops up) and Bandage to
visualize the results.

Grabbed the container from StaPH-B and tried to figure out where the executable
is.  I think it's `/unicycler/unicycler-runner.py`.  Grabbed the sample data
from the Unicycler repo and got something running:

    singularity exec containers/unicycler.sif \
        /unicycler/unicycler-runner.py \
        --short1 sample_data/short_reads_1.fastq.gz \
        --short2 sample_data/short_reads_2.fastq.gz \
        --out assembly/

Pretty straightforward so far.  The result directory contains a log and a bunch
of GFA files.  GFA apparently stands for [Graphical Fragment
Assembly](https://gfa-spec.github.io/GFA-spec/GFA1.html), but I think it's
"graphical" in the "directed/undirected graph" sense and not in the "pixels"
sense.  Text-based format which seems pretty straightforward to parse (maybe
I should have a go at parsing it for fun).

Installed Bandage and viewed the results.  Not sure what exactly I'm looking at,
but it works and looks pretty enough I guess.  [This
example](https://github.com/rrwick/Bandage/wiki/Simple-example) was helpful to
get a sense of what it's trying to show me.

Unicycler has some configuration knobs to tweak:

> Unicycler can be run in three modes: conservative, normal (the default) and
> bold, set with the --mode option. Conservative mode is least likely to produce
> a complete assembly but has a very low risk of misassembly. Bold mode is most
> likely to produce a complete assembly but carries greater risk of misassembly.
> Normal mode is intermediate regarding both completeness and misassembly risk.

Reran with both conservative and bold modes and looked at the difference in the
results for the sample data.  They're not the same, but I can't visually detect
any major obvious differences.  Maybe it's not a big deal on this sample.

Once I got that running in a shell, I got it ported into Snakemake, shaving
a bunch of yaks along the way.

I noticed that Snakemake can take a JSON config file instead of YAML. Fantastic,
switched over to that right away:

    {
        "containers": {
            "fastqc":    "docker://staphb/fastqc:0.12.1",
            "unicycler": "docker://staphb/unicycler:0.5.0"
        },
        "samples": {
            "short_read_example": [
                "sample_data/short_reads_1.fastq.gz",
                "sample_data/short_reads_2.fastq.gz"
            ]
        }
    }

Got the containers downloading via snakemake as well, so it's snakes all the way
down:

    rule containers:
        input:
            expand("containers/{name}.sif", name=config["containers"].keys()),

    rule container:
        output:
            "containers/{name}.sif",
        params:
            source=lambda wc: config["containers"][wc.name],
        shell:
            "singularity pull {output} {params.source}"

Got `snakefmt` working with Neoformat so I can `F6` in Vim to reformat.  Had to
fuck around with the config because it was just emptying out the file — I think
the key was that:

* `snakefmt` edits in-place by default (gross).
* Need to use `replace`: `1` in the Neoformat config to deal with this.

And finally we can assemble:

    def get_input_fastqs(wildcards):
        return config["samples"][wildcards.sample]

    rule unicycler_assemble:
        log:
            "logs/unicycler_assemble/{sample}.log",
        container:
            "containers/unicycler.sif"
        threads: 8
        input:
            "containers/unicycler.sif",
            get_input_fastqs,
        output:
            "assemblies/{sample}/assembly.gfa",
            "assemblies/{sample}/assembly.fasta",
        shell:
            logged(
                "/unicycler/unicycler-runner.py"
                " --threads {threads}"
                " --short1 {input[0]}"
                " --short2 {input[1]}"
                " --out assemblies/{wildcards.sample}/"
            )

Puttered around changing my StumpWM and terminal colors/borders/etc a bit to
make them a little easier on my eyes.  We'll see if it sticks.

## 2023-09-06

HG545 in the morning.  Mostly understood things.

Asked the professor after about a question I had while reading the paper.  One
of the things the paper did to confirm the region of interest was to use a PAC
(P1-derived artificial chromosome) to "rescue" the golden embryos.  The
resulting fish showed mosaic rescue, confirming that the wild-type gene was
likely on that PAC, i.e. in the region of interest.

What I didn't understand is how injecting the plasmid into the embryos resulted
in the expression of the genes farther down the developmental line, e.g. does it
somehow get incorporated into the cells' genomes?  It turns out to be messy.

First: you don't inject "a PAC" into the embryos, you inject "a shitload of
copies of the PAC" into the embryo.  So all of the embryo's cells will have
copies of the PAC floating around inside.  As the cell divides, those will get
diluted in daughter cells over time.  Some of these copies will, by chance, make
it into the nucleus of their cells.  And some of those (rarely) will get
randomly incorporated into the cell's genome, and from then on mitosis takes
over and the gene gets propagated normally.  So the mosaic region from that
point forward will have the gene (and if the region happens to contain some
melanophores, also the rescued wild-type phenotype).

Got my Armis access at some point during class, so it's time to figure out how
to log into the various HPC clusters today.

Doubled checked exam schedule to make sure nothing conflicts.  I think it's
fine.

Changed my school password after the network clusterfuck last week.  Sigh.

Wanted to print something in the lab, realized I never installed any printing
support on this laptop, lol.  `apt install cups` will hopefully Just Work.  CUPS
interface is at `http://localhost:631/`.  It did not Just Work.  Surely 2024
will be The Year of Linux on the Desktop.  Printer wouldn't configure itself,
driver didn't appear in the list when I tried to manually configure it through
CUPS.  `apt install printer-driver-all` got me more drivers but not this one.
Tracked it down on the brother site and downloaded some `.deb` packages but
they're 32-bit instead of 64.  Gave up at this point, what a janky shitshow of
an OS.  If only everything else didn't suck in even worse ways.

Tried getting the VPN running.  Installed with the script into `/opt/cisco`
(good).  Got mysterious errors when trying to connect.  Tried the GUI connection
manager, which runs, but gave a more informative error message I could search
for.  Looks like I need to install `libwebkit2gtk-4.0-37`.  Installed that, now
I get the login screen, but I can't 2FA because I only have Yubikeys set up but
that requires a real browser, not this jank webkitgtk thing, so now I need to
set up *another* 2FA method just for this.  Good god.  Tried to add a new 2FA
device via Duo, but that requires 2FAing *again*, but *this* time it's through
the Duo site which doesn't actually fucking work on Linux, so I can't add it
here, I'll need to use the Windows shitbox at home.  God, I hate two-factor
authentication so much.  It's *always* miserable.

Tried to do the homework for BIOINF-500 (creating a pubmed search alert).  To do
this you need an NCBI account.  Tried to log in via my UM account and managed to
500 the NCBI site.  Incredible.  Poked around and eventually got it working (I
think)?  Created the alert, took a screenshot.  Uploaded the PNG into Canvas for
the assignment.  Canvas shows an error trying to retrieve it.  Uploaded it to
the Canvas "My Files" and used *that* to submit the assignment, instead of
uploading the file directly, and that worked.  *Incredible*.  Why does *nothing*
ever work correctly?

Came home, tried to add the 2FA with the Windows box, but it failed in the same
way (hanging on the popup after successfully touching the yubikey).  But
I finally figured out a workaround (in retrospect, I vaguely recall having to do
this when I added the extra yubikeys originally): log out of everything, then go
to log back into something (e.g. Wolverine Access), but **before** you 2FA in
*that* login process there will be a link to add a new device on the left side
of the screen.  That will then require you to 2FA, but doing it *here* does
actually work.  It seems absolutely wild to me that you need to *not* be logged
in if you want to manage 2FA, but here we are.

Now that I have the Duo app thing on my phone and connected, logging into the
VPN seems to work great.  Yak shaved successfully.

## 2023-09-07

BS521 and its lab this morning.

Got my dotfiles synced to GL.  One tricky thing: my remote `.bash_profile`
sources `/etc/profile` if it exists, but that causes problems on the cluster
because there's some read-only variable set in there that it doesn't like.
Commented out that line and everything looks okay.  `ControlMaster` does work,
so I won't have to auth a billion times a day (thank god).

BS521 lab.  Of course the AC isn't working so it's a billion degrees, lovely.

Installing tidyverse failed with inscrutable errors.  After some googling it
[looks like](https://blog.zenggyu.com/posts/en/2018-01-29-installing-r-r-packages-e-g-tidyverse-and-rstudio-on-ubuntu-linux/index.html)
there's *extra* dependencies you need to install on Linux (C programming is
wonderful):

    sudo apt install libcurl4-openssl-dev libssl-dev libxml2-dev \
        libfontconfig1-dev libharfbuzz-dev libfribidi-dev libfreetype6-dev \
        libpng-dev libtiff5-dev libjpeg-dev

Still fucked, so I manually trawled through the tons of log output, googled
around more, and found that I need to configure an env variable:

    Sys.setenv(PKG_CONFIG_PATH="/usr/lib/x86_64-linux-gnu/pkgconfig")

And finally it works.  Started going through the lab stuff but then time was up
— will come back to it later.

Moving on to rotation lab work.  Working from home today, so I wanted to get my
laptop working with my external monitor and keyboard and such.  Had to swap out
the USB-C cable I was using previously because apparently that one doesn't work
for video ("universal" serial bus my ass) and then adjust my StumpWM `xrandr`
commands, but I did get it working, so now I can use the laptop at my desk,
which is nice.

Note to self: I can probably use the text-mode VPN UI now that I've got the 2FA
sorted out, and maybe remove the webkit crap I installed for it originally.

Finished BS521 lab 0.  Wasn't too bad once I shaved the tidyverse yak.  Getting
it written up with Latex required more Latex derusting, this time for code
listings and images (pulled some of this from the MS thesis).  First, preamble
stuff:

    % Listing package for code listings.
    \RequirePackage{listings}
    \lstdefinestyle{default}{
        basicstyle=\footnotesize\ttfamily,
        showtabs=true,
        frame=lines,
        aboveskip=10pt,
    }
    \lstset{
        language=,
        style=default,
    }

    % Used to embed plots.
    \usepackage{graphicx}

    % No paragraph indentation for homework, just looks awkward.
    \setlength{\parindent}{0pt}

    % Inline code.
    \def\code#1{\small\texttt{#1}}

I really need to split these up into actual files I can include instead of
copypasting them a million times, but maybe I'll wait for one more practice
round first.

Usage:

    % Code listings.
    \begin{lstlisting}
    prop.table(table(DATA$Race))

            Black MexicanAmerican           Other   OtherHispanic           White
        0.22921790      0.23954747      0.04230202      0.03885883      0.45007378
    \end{lstlisting}


    % Graphics.
    \includegraphics[]{figures/bmi-hist}

    \begin{center}
        \includegraphics[width=0.45\textwidth]{figures/hist-age}
        \includegraphics[width=0.45\textwidth]{figures/hist-log-age}
    \end{center}

To actually save PDF plots with R:

    pdf("figures/foo.pdf", height=6, width=6)
    hist(DATA$Foo, main = "Distribution of Foo", xlab="Foo")
    dev.off()

Went to the poster session.  Lots of stuff I don't understand, and a tiny bit
that I do.

## 2023-09-08

HG545 this morning.

Papers never say what *could* have gone wrong with what they did — you have to
just read between the lines and actively think about that (and what it would
have meant, and what you would have done if it did).

Learned about nonsense-mediated decay: a mechanism where mRNA with premature
stop codons is degraded, instead of expressing a (probably truncated) protein.
Without this, if you have a mutation that creates a stop codon in the middle of
the gene, you would see truncated protein expressed.  But because of NMD, the
mRNA is degraded and doesn't express the broken protein (as much).  This is good
not only to reduce wasted translation, but because the truncated proteins can be
actively bad.

One important control that was left out of the study where they wanted to find
where in the organism the target gene is being expressed: inject a probe with
GFP that intentionally shouldn't match *anything*, and expect it to show up
vaguely all over (or not at all).

Another example covered during class: if you suspected a phenotype was caused by
a mutation in a promoter (instead of in an exon), how would you test this?
There were a couple of things folks came up with:

* Could sequence the region in the mutant and wild-type population, compare to
  see if the mutation segregates the two reliably.
* Old school: "reporter genes".  I'm a bit fuzzy on this, but I think you insert
  the promoter into a vector with some easily observable gene (e.g. luciferase,
  a bioluminescent protein).  Then you see if that product is expressed more or
  less with the different variants of the promoter.  This is a bit janky because
  just yanking the promoter completely out of context can be problematic (e.g.
  loses the chromatin structure around it, nearby enhancers/repressors, etc).
* Could use RNAseq to see if the mutants with the variants are producing more of
  the RNA for that gene.
* Could use CHIPseq, if you know the transcription factors that bind to that
  promoter.  Fix, fragment, attach antibodies to the TFs, precipitate them out,
  unfix, extract the DNA (all the remaining is whatever was bound to the
  transcription factors), and then do the sequencing.  You would expect to see
  a larger signal if the mutation in the promoter is causing transcription
  factors to be more likely to bind.


Got back and tried VPN'ing with the command-line client.  It seemed to hang
after entering my password, but then I realized it had just silently tried to
2FA with my phone and I didn't notice.  Trying again and being ready with Duo
let me log in, so I think I can probably ditch the webkit crap I installed for
the graphical thing.

Desktop machine wouldn't take input from my USB hub all of a sudden.  Found some
bullshit in the logs, probably not worth debugging Yet More Linux Jank if I'm
just going to wipe this machine and install Debian on it soon anyway.  Tried to
reboot and systemd hung at the end, so I just powercycled the damn thing.  If
I could just have one single day where no computer broke for me, that would be
so nice.

Flu shots are available, need to get one so PI doesn't get pinged all the time.

Read for BS521 class.  All still pretty basic.  Cleaned up and turned in lab 0.
Finished homework 2 as well, just to get it out of the way.  Or at least
I thought I did, except there are apparently Surprise Questions™ not in the book
to do with R.  I'll do that this weekend.

## 2023-09-09

Actually finished BS521 homework 2.  Realized my Latex `\code` shortcut was
broken:

    % Broken, doesn't scope the \small so later text is changed.
    \def\code#1{\small\texttt{#1}}

    % Fixed     v                 v
    \def\code#1{{\small\texttt{#1}}}

Did a first draft of the HG545 assignment 1.  This one is a lot harder than the
stats homework.  Need to polish it up and submit it tomorrow.

## 2023-09-10

Polished and submitted the HG545 homework.  We'll see how it goes, I guess.

## 2023-09-11

HG545 discussion.  This paper was pretty straightforward.

Met with PIBS peer mentor.

HG545 second paper was posted, need to do an initial read of that tonight.

## 2023-09-12

BS521 again.  Mostly basic linear regression stuff, but got a few interesting
tidbits out of it, mostly about the coefficient of determination, also called
`R²` or `r²`.  This is the square of the correlation coefficient `r`, and it is
said to mean "the fraction of the variability in the data that is explained by
the linear model".  So an `r²` of `0.7` would mean "70% of the variation in the
data is explained by the model".

*Intuitively* what this means would be to look at the total variability in the
data, i.e.:

    (- (reduce #'max y) (reduce #'min y))

Then convert the data to residuals by subtracting out the model:

    (mapcar #'- (mapcar #'model x) y)

and look at home much variability remains:

    (- (reduce #'max residuals) (reduce #'min residuals))

Compare the two to see the fraction that remains after accounting for the model.

Looked into some "R for actual programmers" resources so maybe I can feel like
I'm flailing less:

* <https://arrgh.tim-smith.us/>
* <https://r4ds.hadley.nz/>
* <https://adv-r.hadley.nz/>
* <https://www.burns-stat.com/documents/books/the-r-inferno/>
* <https://www.burns-stat.com/documents/tutorials/impatient-r/>
* <https://www.burns-stat.com/documents/books/tao-te-programming/>

Lunch at a place called Maizie's.  Was actually pretty good!

Doing Yet Another Round of Paperwork for the VA.  So much red tape.  Did what
I could here, but there's a bunch I can't do until I get home after class today.

So far I'm loving the look of the stumpwm config changes I made the other day.
Shouldn't have waited this long to clean things up.  TODO: use
`select-from-menu` to implement a better screen-switching shortcut in stump.

Figured out how to print.  Use <https://mprint.umich.edu/maps?sites> to find
a reasonable printer nearby, then Print Here to use it.  You upload a PDF or
whatever through the web UI.  Good enough, it works.  One color paper cost
$3.22 of my (apparent) $24 print budget.  Welp.

PIBS800.  Getting… another lecture about how to use the library?  Didn't we
already do this in the other class?

Spent a bit more time tracking down my white whale font from that 1979 Science
issue.  Identifont came to the rescue and I think I finally have an answer, or
at least something very close: "Rotation" by Arthur Ritzel from 1971.
Unfortunately a 50-year old font still has ghastly licensing options, so I'll
probably never be able to *use* it, but at least I have peace of mind, I guess.

## 2023-09-13

HG545.  This module is focusing on how to create physical maps of chromosomes,
especially the bizarre human Y chromosome.

There's a difference between a genetic map and a physical map.  A genetic map
can be created with e.g. linkage analysis, and can tell you relative distances
but not necessarily the exact locations of things.  A physical map shows the
actual locations.  Note that physically linked genes might not necessarily be
genetically linked if they're far enough apart that the recombination chance is
50%.

We can't use genetic mapping for the Y chromosome because there's not
recombination with another chromosome.

In the paper they used hierarchical shotgun sequencing to sequence the
Y chromosome, which goes roughly like this:

1. Fragmented the human genome into ~200kb fragments.
2. Cloned those into BACs
3. You want to retrieve *only* the fragments from the Y chromosome, not from the others.
4. Start with a known gene on Y (e.g. a well-known gene like Sry, the
   sex-determining gene) and you PCR that to amplify the fragment(s) that
   contain it.
5. Sequence those fragments (split into 20kb and shotgun sequence).
6. Design more PCR primers that *start* at the ends of *those* fragments, use
   those to amplify things next to it.
7. Repeat to get overlapping tiles.

You end up with overlapping tiles:

    ---------Sry----------                          ----------Zry--------------
                       >>>                          <<<
                       -----------------
                                     >>>
                                     -------------------

Nowadays we can take advantage of long read tech to eliminate a lot of the grunt
work in the process, e.g.:

* Oxford Nanopore: 50-500kb, 90% accuracy.
* PacBio: 20kb, >99% accuracy.

Oxford is still pretty bad accuracy, but is useful to resolve things when PacBio
still runs into trouble with some of the crazy-long repeats.

Also learned about some kind of "bionano" thing that was glossed over very
quickly.  Looks like it's a company?  Need to ask someone about this.

Next talked about content of the human genome:

    Human Genome
        Unique DNA (1/3)
        Repetative DNA (2/3)
            Dispersed Repeats
                Transposable Elements (e.g. LINEs, Alu)
                Retrogenes (e.g. CDY)
                Transposed Genes (e.g. DAZ)
                tDNA
            Local Repeats
                Segmental Duplication (e.g. palindromes)
                Satellite Duplication
                rDNA

Repeats are challenging to assemble, e.g. if you have:

    Unique A | LINE1 | Unique B | LINE 1 | Unique C

You might get reads like:

    A1
    1B1
    1C

It's hard to tell which direction the `1B1` should go, or whether `A` should go
directly to `C`.  `LINE1` specifically can be resolved with PacBio because it's
only ~6.5kb, far less than the 20kb you get from PacBio, but other segments
still cause problems.

Example of problematic things are the large palindromes from the paper:

             1.45mb arm
    <------------------------ Unique -------------------------->
               arms have ~99.97% nucleotide identity

Even if there are a few SNPs on the arms, if the segments right around the
unique part happen to be identical it's hard to tell which arm goes where.

Looked into the PACCAR thing from yesterday, but the application form is
extremely long and I already have enough red tape to deal with through the VA,
so I'm not going to add more paperwork for myself.  Oh well.

Met with John Prensner about possibly rotating in his lab.  Next steps for
rotations are pretty clearly to set up some chats with his students and some
from Boyle/Parker labs to make a choice for the next 1-2 slots.  I'll try to do
that for next week I think.  Also want to talk to Shavit again — I really liked
chatting with him, and I think if I wanted to rotate there I would need him to
join the department as an affiliate of some kind, so I'd need to see if he's
okay with doing that.

## 2023-09-14

I am going to `mark` every time I have to log in and/or 2FA for school for at
least a week, so I can graph it and be sad.  Adjusted my `marks` thing to go to
my Syncthing dir.

Sped up my shell prompt by wrapping the Mercurial prompt in a basic `.hg`
existence check.  Had to relearn how to write a fish function.

BS521. Chatted with the professor at office hours a bit to ask a couple of
things.

Made a TODO list with all the homework/exam/lab stuff for school.  Hopefully
this will make it easier to see what's coming up since Canvas is barely usable.

Started reaching out to set up chats with folks in a few labs I might be
interested in for my next rotation.

## 2023-09-15

HG545 this morning.

## 2023-09-16

BS521 reading.

Z-score means "number of standard deviations above the mean".

Successes-based distributions:

* Geometric: number of trials before observing a success.
* Binomial: number of successes in a fixed number of trials.

The chapters of this book are getting sloppier as they go on — I'm noticing
a lot more typos now than in the first couple of chapters.

Went back to John D Cook's R for Programmers post when the `pnorm` function was
mentioned.  R has several of these functions with veyr confusing names:

    <func><dist>

    <func>: d: PDF ("density")
            p: CDF ("probability")
            q: Quantile, i.e. CDF⁻¹
            r: Random sample

    <dist>: norm: Normal aka gaussian
            unif: Uniform

So `pnorm` is "the CDF of a normal distribution".

Found a way to view which fonts a PDF file embeds and/or references: `pdffonts`.
Nice.

Tired of CACL crashing on my laptop because I don't have CCL, so I'll just
install CCL.

    git clone https://github.com/Clozure/ccl.git ccl
    curl -L -O https://github.com/Clozure/ccl/releases/download/v1.12.2/linuxx86.tar.gz
    cd ccl
    tar xf ../linuxx86.tar.gz
    ./lx86cl64
    (rebuild-ccl :full t)

    sudo ln -s /home/sjl/src/ccl/lx86cl64 /usr/local/bin/ccl64

Finally discovered the reason my bash prompt gets mangled sometimes:
non-printing characters in `PS1` have to be wrapped in `\[…\]`.  So I need to do
something ugly like this:

    export PS1='\n\[${PINK}\]\u \[${D}\]at \[${HOST_COLOR}\]\h \[${D}\]in \[${GREEN}\]\w\[${D}\] $(last_return_value)$ '

But at least it works properly now and won't drive me crazy.

Did a bit more font hunting.  Looking for something to use for figures that
looks plotter-esque, but isn't something with a couple of scattered glyphs and
no weights like the plotter fonts I've found.  Licensing is a minefield, but
Google Fonts has a bunch of stuff that's under the open font license, and
I think I found a couple that might work: Quicksand and Nunito.  Of the two,
Nunito seems a little nicer to me.  Will need to try it in some graphs and see
how it works.

## 2023-09-17

Trying to get ahead of classwork for the next couple of weeks, since I've got so
many other things going on.

Did the reading for BS521 for the next two weeks.

Finished BS521 homework 3.

## 2023-09-18

HG545.  Feeling better about this module than the last, which is surprising
because I enjoyed this paper less.

Chatted with someone about one of the labs I'm thinking about rotating in.

Cleaned up HW2 for HG545 a bit.  Still not done, but at least I'm getting it
into shape.

## 2023-09-19

BS521.

Meeting with two more grad students to chat about their labs.

BI500.

DCMB has full time IT staff: `DCMB-IT-Services@umich.edu`.  Might email them
about Ethernet connection?

Chat widget on <https://michmed.service-now.com/sp> is a decent way to get help.
Also walk-in help in THSL 4020. ARC support: <arc-support@umich.edu>.

Slurm tutorial.  Learned a couple of interesting things:

* `sq` is an alias for `squeue --me`.  Nice.
* `my_job_header` can help debug weird Slurm shit, handy.
* Emails will include core/mem high-water marks.  Need to figure out if I can
  get this programatically, might be more accurate than the Snakemake benchmarks
  (or at least worth comparing).

Chatted about Boyle lab with a current grad student.

PIBS 800.

Finished HG545 homework 2.
