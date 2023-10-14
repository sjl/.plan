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
₂
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

## 2023-09-20

HG545 discussion.  Talked a lot about the Y chromosome paper.

## 2023-09-21

BS521.  Went over the binomial distribution.  Seeing this yet another time gave
me an actual intuitive understanding this time, which is nice.

BISTRO seminar.

## 2023-09-22

Retreat.

Lightning talks.

Breakout panel with current grad students.  Lots of stuff, probably not going to
write it all down here.

## 2023-09-23

Finished HW 4 for BS521.

Got some random Latex shit to remember for next time. Aligned equations:

    \begin{eqnarray*}
        foo &=& bar \\
        meow &=& wow \\
    \end{eqnarray*}

References to figures:

    (See figure~\ref{fig:g-a})

    …

    \begin{figure}[H]
        \centering
        \includegraphics[width=0.65\textwidth]{figures/g-a}
        \caption{Graph for exercise 4.1 part a.}
        \label{fig:g-a}
    \end{figure}

Units:

    \usepackage{units}

    Drink 500 \unit{ml} of water at lunch.

And some random R shit to remember for next time:

    dbinom = Binomial PDF
    pbinom = Binomial CDF

Came up with some absolutely cursed code to made shaded normal graphs.
Surprised that's not already a thing.

## 2023-09-25

HG545.  Need to retype all my notes for this module here when I get some time so
I don't lose them.

Today started with a description of RNAseq.  Something vaguely familiar was
a nice change for this class.  Then reviewed STARR-seq which I think I mostly
understand now.

Talked about the similarity between enhancers and promoters.  Polymerase can
sometimes actually sit down at enhancers and produce small RNAs, but
transcription doesn't ever elongate.  But this might be an example of how genes
could evolve.

Then talked about heat shock proteins and heat shock factor as an example of how
rapid transcription can happen.

* HSE: "Heat Shock Element", an enhancer sequence located upstream of a gene,
  e.g. hsp90.
* hsp90: "Heat Shock Protein 90", a protein that's used in cells to help other
  proteins fold in the presence of heat that might otherwise prevent it.  The 90
  is from its weight in kilodaltons (lol).
* HSF1: "Heat Shock Factor 1", a transcription factor that trimerizes, binds to
  HSE, and recruits another thing to activate the transcription of hsp90.

There's a self-regulation loop here where, when things are cold, hsp90 binds to
HSF1 outside the nucleus and prevents it from enhancing transcription of hsp90
(i.e. of itself).  But when heat is applied, other proteins unfold and hsp90
starts chaperoning them more, which leaves HSF1 free to enter the nucleus and
enhance transcription of hsp90.

Remembering how to create a local Postgres DB for testing:

    sudo -u postgres psql

    CREATE DATABASE example;
    CREATE USER testuser WITH PASSWORD 'pass';
    GRANT ALL PRIVILEGES ON DATABASE example TO testuser;

    \c example
    GRANT ALL ON SCHEMA public TO testuser;

    \q

    psql postgresql://testuser:pass@localhost:5432/example

## 2023-09-26

BS521.  Exam is on Thursday.  Today is about sampling distributions and
statistical inference.

BIOINF500.  Fire alarm for the first half of class, nice.  Rest of the class
will be recorded, need to remember to watch it later.

## 2023-09-27

HG545 this morning. Did an initial pass on the homework, then met up with some
other grad students later to chat about it and now I'm even less confident, lol.
Welp.

## 2023-09-28

BS521 exam.  Did okay, though I really should have had a couple of more things
on my note sheet than I did.  Next time I need to go through the slides too, not
just the book — there were things on the test from class only, not in the book.
I think I did alright though.

Finished HG545 homework.  I think I did alright, but my brain is now fried.

## 2023-09-29

HG545 discussion this morning.

Sent a few emails to try to nail down my next three rotations.  I think at this
point I have a pretty good idea of where I want to try, so if I can just get
them all nailed down now it'll be less stuff to deal with later.

Signed up for the 503 discussion sections.  What a painful process to get
registered.  I should have waited til I was home on my large monitor because
trying to flip back and forth between the 90%-whitespace-filled list of sessions
and my calendar/TODO list was extremely tedious.  I think I've got it all mapped
out now though.

# October 2023

## 2023-10-01

Put up a bunch of stuff for sale on the PIBS list.  Need to declutter my
apartment now that I've mostly moved in.

Did a few hours of work on Lab 1 for BS521.  Too much unproductive screwing
around in R trying to figure out how to get decent fonts.  Should be able to
finish it up tomorrow though.  Random notes jotted down from the process follow.

Side-by-side figures in LaTeX:

    \begin{figure}[h]
        \begin{minipage}[t]{0.48\textwidth}
            \includegraphics[width=\linewidth]{figures/bp-histogram}
            \caption{Distribution of blood pressure among participants.}
            \label{fig:bp-histogram}
        \end{minipage}
        \hfill
        \begin{minipage}[t]{0.48\textwidth}
            \includegraphics[width=\linewidth]{figures/bp-nqq}
            \caption{Normal QQ plot of blood pressure values.}
            \label{fig:bp-nqq}
        \end{minipage}
    \end{figure}


Reasonable quantile plot in R:

    qplot <- function(filename, data, label, main, ...) {
        n = length(data)
        plot(((1:n - 1)/(n - 1)), sort(data),
             type = "l",
             main = main,
             xlab = "Quantile",
             ylab = label,
             ...)
    }

QQ plot with the damn line in R:

    nqqplot <- function(data, ...) {
        qqnorm(data, ...)
        qqline(data)
    }

Reading in a CSV with specific column types:

    data <- read_csv("EPID_521_lab_data.csv", col_types="iddfiffdffdd")

Note that this seems to give you a "tibble", whatever the hell that is.  Some
kind of tidyverse thing?  It's very confusing that everywhere you look there's
a hairball of a mess of base R, tidyverse, and ggplot2 and everyone just assumes
you understand which is part of what.

Reordering levels:

    data <- mutate(data, diet=factor(data$diet, levels=c("Poor", "Fair", "Good", "VeryGood", "Excellent")))


Removing rows with `NA`s for e.g. the `cot` column:

    data <- data[complete.cases(data$cot),]

Histograms with specific bin widths, rather than a number of bins:

    hist(data$age, breaks=seq(from=15, to=90, by=1), main="", xlab="Age")

Multiple box plots in one image:

    boxplot(bmi~sex, data=data)

Marking and/or filtering on a boolean condition:

    data$locot <- data$cot <= 0.011
    locot <- subset(data, cot <= 0.011)
    hicot <- subset(data, cot > 0.011)

## 2023-10-02

HG545 review this morning.  Need to go back and review the first module again
tomorrow since it's been a while.

Finish BS521 lab 1, finally.  That was a lot more work than I expected.

Met with a professor about possible rotation.  Need to chat with my advisor to
see if there's special paperwork I'll need.

## 2023-10-03

BS521.  Confidence intervals.

BI500.  Research writing.

Finally got around to splitting my Vimrc into minimal and extra files, so I can
sync the minimal one to servers and not hate myself when trying to edit. There's
some jank involved around the colorschemes and `set termguicolors` but I think
have have something that should work.

PIBS800.  Mentor/mentee relationships.

## 2023-10-04

Advising meeting.  Need to do a couple of things in EdM and register for 602,
but I'm currently blocked on both by other folks so I'm good for now.

HG545 exam.

## 2023-10-05

Finished the HG545 exam last night.  That was… deeply unpleasant.

BS521.  Hypothesis testing.

BS521 reading.

Read the paper for HG545.  I get the general idea, and it seems like a pretty
clear experiment.  I wonder how much we'll stick to the paper vs going off topic
this time.

Needed to convert some PDF graphs to PNG to put in a presentation, but `convert`
was whining about some security crap:

    ><((°> convert n50.pdf n50.png
    convert-im6.q16: attempt to perform an operation not allowed by the security policy `PDF' @ error/constitute.c/IsCoderAuthorized/421.

Turns out there was a bug in ghostscript, which was fixed, but convert still
doesn't trust it so won't convert stuff.  Great.  Have to edit
`/etc/ImageMagick-6/policy.xml` and comment out these lines to make it behave:

    <!-- disable ghostscript format types -->
    <policy domain="coder" rights="none" pattern="PS" />
    <policy domain="coder" rights="none" pattern="PS2" />
    <policy domain="coder" rights="none" pattern="PS3" />
    <policy domain="coder" rights="none" pattern="EPS" />
    <policy domain="coder" rights="none" pattern="PDF" />
    <policy domain="coder" rights="none" pattern="XPS" />

Skimmed through the slides for HG545 tomorrow.  It's nice to be able to get
a preview of things again.

## 2023-10-06

HG545, class was about splicing.  I feel much better about this module thanks to
being able to prepare a bit with the preview last night.

## 2023-10-07

Installed <https://github.com/numcommand/num> — might come in handy here and
there.

## 2023-10-08

Reread the paper for HG545.  It's… a little clearer now?  Though honestly it
wasn't too bad before compared to the other papers.  Just a lot of acronyms.
Got a list of things to ask.

## 2023-10-09

HG545 this morning, about co/post-transcriptional modification.  The downside of
having slides is that people put a ton of things on them and you can't take
notes fast enough.  Need to go back over the slides and write down things once
I get home so I don't forget them.

## 2023-10-10

BS521, hypothesis testing, p values, t distribution.

BI500, code quality tips.  Checked with Prof. Sartor and submitting a LaTeX PDF
for the references homework is fine.

Pinged a few students in a lab I'm interested in to see if they're willing to
chat about their experience.  Just need to nail down my third rotation and then
I'll be all set.

Ordered a used copy of the Grammar of Graphics book.  I've read enough in the
ebook copy from the library that I know I want the entire thing, even though
it's quite expensive.

Read chapter 4 of the book while the straggler genomes finish in the last batch,
about variables and basic transformations on them.  The book uses the ridiculous
terms "homoscedasticity" and "heteroscedasticity" to mean "homogeneous variance"
and "heterogeneous variance", which I *think* is the same idea as Cleveland's
"monotone spread" (or possibly a more general version of it).

I really wish the book wouldn't omit the axis-drawing code from the diagrams
— it makes it unclear where each piece of the output is coming from.  I think
I *mostly* understand it, but would prefer if it were all explicit (even if it
would make things a bit longer).

Read chapter 5 too, on algebras.  This was much, much more confusing and would
have been much clearer with more explicit examples.  Need to read this at least
one more time to get it, I'm sure.

Going back to take some notes for HG545 while they're still (vaguely) fresh in
my mind.  First: notes from the class on splicing.

The "R-loop" terminology is confusing.  It's inspired by the name "D-loop",
which notes how DNA will unzip to show a loop when it's being duplicated (and
there's a complementary strand bound to one side).  "R-loop" *also* refers to
the loop *in the DNA* when it's bound *to RNA* (e.g. when it's being
transcribed).  Again: the actual loop in an "R-loop" is a loop of DNA.

An RNA molecule has 3 relevant sites when considering splicing:

```
 5' exon |                  intron                            | 3' exon
 ======AG|GUAAGU============================YNYURAY====Y₁₁NCAG|G==============
                                                 ↑
      5' Splice Site                    Branch Site      3' Splice Site
```

Note that in this case the branch site is specifically an adenine.  That's
important (reason comes later).

One important aspect of RNA that allows it to be spliced (contrasted with DNA)
is the hydroxyl group on the 2' carbon in RNA, which is not present in DNA
(that's why it's *deoxy*ribose).  That hydroxyl group is what attacks the
phosphate bond at the 5' splice site and cleaves it apart (after being brought
close to it by the spliceosome).  That leaves a hydroxyl group exposed hanging
off of the 5' exon, and in the next step *that* group is brought close to the 3'
splice site and attacks it.  Once that bond is broken the intron (as
a lariat-shaped thing) floats away, and the exons are spliced together.

The chemistry of the breaks is called "transesterification": two
phosphodi*ester* bonds are broken (at intron/exon and exon/intron boundaries),
and two more are created (one in the lariat, and the splice between exons).

(Of course like everything in biology, in reality it's all a giant mess and there
are multiple kinds of splicing, including self-splicing.)

The spliceosome is a giant thing made of a bunch of different proteins and also
5 RNAs that mediates splicing.  The RNAs are important because those are what
recognize the splice and branch sites through complementary pairing, e.g. at the
5' splice site we have:

       ____________
      /     U1     \  U1 component of spliceosome
      \            /
       \__CAUUCA__/
          ┆┆┆┆┆┆
        ==GUAAGU==    RNA

In a similar way, the U2 component binds to the branch site, but the binding
sequence specifically skips the adenine at the site, which "extrudes" it from
the RNA a little bit:

              extruded adenine
                   ↓
                   A
    ======U A C U A C=======    RNA
          ┆ ┆ ┆ ┆ ┆ ┆
       .——C A U U C A——.
      /                 \
     /        U2         \      U2 component of spliceosome
     \___________________/

Alternate splicing is also a big deal, because it allows the creation of many
different mRNAs from the same gene by bringing together different exon/intron
boundaries to be spliced instead of always splicing the closest one.

Of course there's other complications too, like splicing enhancers and silencers
that can recruit/block the splicing machinery.

Skimmed over tomorrow's HG545 slides so I don't have to go in blind again. Seems
pretty reasonable, though the end seems pretty rushed and I *think* it's
relevant to one of the questions in the homework.  Need to pay attention at the
end.

PIBS800, how to read a research paper.  I feel like I've had three versions of
this presentation by different people at different times at this point.

Started BS521 homework 5.  A bit more confusing than the previous homeworks, and
it's been a week or so since I touched LaTeX so I once again have to fight it
every step of the way.

## 2023-10-11

HG545 this morning, about translation.

VA onboarding after that.  Took a couple of hours, but I now finally have
a badge.

Been reading the GoG book during some spare free minutes here and there.
Skimming over a lot of the formalism, I still feel like this could be much
improved by showing some full examples with everything laid out.

Sketched out some answers to HG545 questions.

Finished BS521 homework 5, turned it in.

Cleaned up HG545 answers.  Need to do one final pass tomorrow.

## 2023-10-12

BS521, started talking about two-distribution t tests.

Finally got around to swapping my search engine on my phone to Kagi.  The
degoogling continues.

I really need to figure out a decent way to do proper pivot tables in Postgres.
From reading the docs it looks *surprisingly* janky for what I'd expect from
Postgres.

Read up on index operator classes, which was preventing Postgres from using an
index when searching for a prefix of a string, e.g. `SELECT name FROM foo WHERE
name LIKE 'pref%';`.  Fixed by telling Postgres this index will be used with
text patterns by e.g. `CREATE INDEX i__foo__name ON foo(name
text_pattern_ops);`.

## 2023-10-13

HG545 discussion.

## 2023-10-14

Fall break.
