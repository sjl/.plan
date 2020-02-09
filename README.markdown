[TOC]

# January 2020

## 2020-01-03

Converted `paste.stevelosh.com` to HTTPS.  Forgot it in the previous conversion.

## 2020-01-14

Moved all my repositories from Source Hut to `hg.stevelosh.com`.  Wasn't
expecting to have to shave this yak so soon, but such is life.  On the plus
side: pushing is *so much faster* now.  Rough timing for an empty push was ~5
seconds on Source Hut, down to around a second now.  No more sitting and
staring at the command line waiting to get back to work.

## 2020-01-15

Finished (mostly) reskinning `hg.stevelosh.com`.  Had to shave a couple of yaks
in Mercurial itself (diff headers getting truncated) and the hgweb Markdown
extension.  Ended up just completely forking the extension and tearing out
almost all of its guts.  The result should (hopefully) be easier to maintain as
Mercurial breaks internal shit over time.

Still need to finish the CSS for the rendered Markdown, but that can wait for
now.

## 2020-01-17

Got the RIT VPN set up on my Linux machine so I can connect for class.  I was
worried I'd have to install some horrible Cisco VPN client thing, but it turns
out you can use the `openconnect` client to connect, so `sudo apt install
openconnect` and then `sudo openconnect vpn.rit.edu` just magically works.
Fantastic.

Finished the `hg.stevelosh.com` reskin on my lunch break.  Just had to get the
`README`s looking decent.

Finally figured out a strategy for syncing a small subset of my dotfiles onto
remote servers easily, so I don't have to be completely miserable on them.
Goals:

* Needs to provide a reasonable subset of the stuff I use to get around.
* Needs to handle servers with both bash and fish.
* Needs to be easily syncable with a single command and no extra setup.
* Needs to handle servers that don't have git or Mercurial.

Ended up making a `remote/` folder in my dotfiles.  Almost everything inside it
is a symlink except for a `bootstrap.sh`.  The folder gets `rsync --copy-links`ed
over and then `bootstrap.sh` will symlink all the resulting files into their
places.  Hopefully this should be easier to maintain.  Did a bunch of cleanup on
my bash and fish setups while I was at it.

Still need to figure out how to get a decent Vim setup remotely.  Syncing all my
plugins is probably not ideal, but maybe.  Who knows.

## 2020-01-18

KA biology and coffee.

Cellular respiration:

* Starts with glucose (C₆H₁₂O₆).
* The process is called glycolysis, and starts in the cytosol.
* Glycolysis split the 6-carbon glucose into two 3-carbon molecules (pyruvate).
* In the process we produce 2 (net) ATP's, and reduce 2 NAD⁺ molecules to 2 NADH
  (note the move from a positive charge to negative, i.e. gaining electrons,
  i.e. RIG (reduction is gaining)).
* Some organisms stop here and use the pyruvates for fermentation.
* Otherwise, the carboxyl group is stripped from each pyruvate and released as
  CO₂.
* The rest of the pyruvate (essentially an acetyl group) latches onto "coenzyme
  A" (aka "CoA"), forming acetyl-CoA.
* The enzyme transfers the acetyl group to an oxaloacetic acid, which forms
  citric acid.
* Next step is the "Krebs cycle"/"citric acid cycle", which is… complicated, and
  happens in the matrix of the mitochondria.
* As the citric acid cycle progresses we keep reducing to NADH.
* The ATPs produced in cellular respiration can be used directly.
* The reduced NADHs (and other products like QH₂) are used to create a proton
  gradient in the mitochondria, which is then used to produce more ATP (each
  NADH results in ~2-3 ATPs).  This happens in the crista of the mitochondria.
* Whole result is ~27-38 ATPs (typically 29-30 in most cells).
* Review: the four steps of cellular respiration:
    1. Glycolysis: splits glucose into two pyruvates, produces ATP and reduces NAD⁺ to NADH.  Happens in the cytosol.
    2. Pyruvate Oxidation: each pyruvate is stripped of CO₂, binds to CoA, and generates more NADH.
    3. Citric Acid/Krebs Cycle: each acetyl-CoA goes through a cycle and produces ATP, NADH, and FADH₂.
    4. Oxidative Phosphorylation: the NADH and FADH₂ are used to make a proton gradient, and that is used to make more ATP.

Did the `TRIE` problem in Rosalind.  Making an actual trie was easy, but getting
an adjacency list for the flattened/copypasteable output and using `cl-dot` to
graph it nicely was fiddly.  Annoying bits about `cl-dot` to remember for next
time:

* There's no `:shape :square`, it's `:shape :box`.
* `:fillcolor` does nothing without `:style :filled`.
* The solution to "edge labels are too close to the edges" is apparently "add
  spaces to your label string".  Ugh.
* To change the size of a node, use `:height` and `:width`, not `:size`.  They
  will be "helpfully" be ignored if you have a label that's too big to fit.
* `cl-dot` provides implicit labels, so if you want no label you need `:label ""`.

Cleanup up the styling of `hg.stevelosh.com` a bit more.  This time it was the
`<code>` tags inside `<li>`'s that weren't styled.  I styled `<p><code>` before,
because I wanted to *avoid* applying those styles to `<pre><code>` content
(otherwise it'd have double borders all over the place).  But that missed out on
the `<code>` tags that weren't inside paragraphs.  Ended up just styling *all*
`<code>`s and then undoing the borders in `<pre><code>`.  Sigh.

Also realized that the repository descriptions served by hgweb can contain
arbitrary HTML.  Neat.  Used that to clean a few more things up.

Updated all the Bitbucket repository `README`s to point to `hg.stevelosh.com`.
The Great Source Hut Yak Shaving of 2020 is finally complete, thank christ.
Time to move on to doing actual work.

## 2020-01-19

Finally got around to setting up packages for all of my Rosalind problems.  In
all my "coding challenge" repos (Rosalind, Project Euler, Advent of Code, etc)
I originally just shoved everything into one big package.  This was easy to
start with, but as I solved more and more problems I started to hit naming
conflicts more and more often.  Eventually I realized that for my own sanity
I should really give each problem its own package, with all the utilities in
a `utils` package.  I did this for my Advent of Code repo a while back and while
it was a pain in the ass to refactor everything, the result is much nicer.
Today I refactored the Rosalind repo.  The Project Euler repo is a work in
progress, mostly because it's so much bigger than the other two.

Did Rosalind problem `PDST`.  Pretty easy.  Most annoying part was the output,
but I extended my float printer to handle 2D arrays to make it easier to output
what they want in the future.

## 2020-01-20

Wanted to do a Rosalind problem over lunch.  On a whim I decided to use CCL just
to keep myself honest — I usually use SBCL, so using another implementation now
and then helps ensure I'm writing standards-compliant code.  But apparently
a recent Vlime commit broke Vlime in CCL.  So I had to shave *that* yak first.
Sent a PR.

Did Rosalind problem `ASPC`.  The problem itself was trivial.  Made a handy
iterate driver to make it even more trivial.

Running the test suite in CCL gave me exactly what I wanted: examples of where
I was unintentionally relying on SBCL's behavior.  Today there were two:

1. Relying on the traversal order of iterate's `:in-hashtable` (which uses
   `with-hash-table-iterator`) to get the output of `TRIE`.  Made a helper to
   convert the hash tables to sorted alists to fix the output.
2. Relying on the `~,…F` format directive having a half-up rounding strategy.
   Turns out that when format is rounding a float to a given number of decimal
   places, the implementation is allowed to round half however it wants.  SBCL
   seems to round half up (which matches what Rosalind shows in their examples,
   which is why I never noticed) but CCL seems to use banker's rounding.  Had to
   do an ugly hack in `float-string` to make the output consistently match
   Rosalind's style everywhere.

## 2020-01-22

Started doing Rosalind problems in shell/Awk, to join in with a group of folks
at work doing them for the first time.  The first few problems are simple, but
I still managed to learn a few tricks by implementing them with UNIXy tools.

Fixed a few remaining broken links on my site.  It's been a week or two since
I poked around at it, and that was on another machine, but `./deploy.sh` Just
Worked.  It's so nice to have a site generator I designed myself that's not
going to change out from under me when I just want to fix something simple and
move on with my life.

## 2020-01-23

Lesk book exercises, chapter 1:

1. Average density would be `(/ 3r4 3r9) = 1/100000` or 1 gene every ~100kb.
2. Parts:
    * A: Two humans would have roughly 250k differences. 
    * B: A human and a chimpanzee would have roughly 3m differences.
3. Parts:
    * A: Average density would be 2 SNPs per 1000 base pairs.
    * B: Is this a trick question?  I think 1.1% of the differences would be in protein-coding regions.
4. Parts:
    * A: I am confused.  The glossary defines a "haplotype" as a group of closely-linked genes that are typically inherited together.  So… 1 haplotype?  But the *text* talks about a haplotype as being a combination of SNPs in a recombination-poor region.  So if "haplotype" means the combination of SNPs, not a set of genes, then I think this would be `4^10 = 1048576`.
    * B: On a diploid chromosome, you'd have two separate sets of SNPs to combine (and order doesn't matter), so I think it's  `4^10 * 4^10 / 2`.
    * C: `(1 SNP / 5 kb) * (100 kb) = 20 SNPs = 2^20 sequences = 1048576 sequences`
5. TODO
6. TODO
7. TODO
8. A much less drastic change, though it could still cause issues if it's at
   a critical point in the RNA molecule (e.g. the anticodon in tRNA).
9. TODO
10. If the gene Kangaroo coat color is not on the X chromosome, you wouldn't be able to get the calico pattern that comes from X chromosome inactivation.
11. Parts:
    * A: No, because if it were a mutation in the gene itself it would act by affecting the structure of the protein, and should have the same effect in adults and children.  But it doesn't, so it's more likely to be a mutation in regulatory region.
    * B: It's not on the Y chromosome?
12. TODO
13. TODO
14. TODO
15. TODO
16. TODO
17. TODO
18. TODO

## 2020-01-24

Solved the `FIB` Rosalind problem in my shell/Awk repo.  Tried doing it in
straight bash, but I couldn't figure out how to get the bash function to use
a global bash array for memoization after like 10 minutes of searching.  Ended
up rewriting it in Awk, which took two minutes, was simple, and runs fast.
Great.

Solved `MMCH` in my Lisp repo.  Much like the previous problem in this line, it
was way easier than they made it seem.  Also fixed the Uniprot cache to use the
filesystem instead of just keeping a hash table, to save a few seconds of my
life every time I `(run-tests)` in a fresh Lisp session.

## 2020-01-25

Rebooted my Mansion repo to try to simplify it enough that I can start
dogfooding it for actual use, then turn it into something publicly-usable.

## 2020-01-27

Trying to decide on data to use for the BIOL-650 project.  A list of
possibilities:

* <https://www.ncbi.nlm.nih.gov/sra/ERX1735780>
* <https://www.cell.com/cell/fulltext/S0092-8674(15)01339-2#back-bib72>
* <https://www.cancer.gov/about-nci/organization/ccg/research/structural-genomics/tcga/studied-cancers>
* <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3673022/>

## 2020-01-29

Figured out how to get the mutt HTMLified email working on my local machine,
like I had done for work.  Had to install NeoMutt from source because the Ubuntu
version is too old to include `group-alternatives`:

* Clone the NeoMutt repo.
* Install Tokyo Cabinet for the header cache with `sudo apt install libtokyocabinet-dev`.
* Configure the NeoMutt build with `./configure --disable-idn --idn2 --disable-doc --prefix=/usr/local --gnutls --with-ui=ncurses --tokyocabinet`.
  * Note the `--disable-idn --idn2` to make it use `libidn2` which is installed, instead of `libidn` which isn't.
  * Is this the correct set of options?  Who knows!?
* Install into `/usr/local` with `sudo make install`.

More searching around for projects for HTSA:

    https://www.sciencedirect.com/science/article/pii/S2352340918302920
    doi 10.1016/j.dib.2018.03.079
    Illumina HiSeq 2500
    https://www.ncbi.nlm.nih.gov/sra/?term=PRJNA432903

    https://www.sciencedirect.com/science/article/pii/S2352340919303750
    doi 10.1016/j.dib.2019.104022
    Ion Proton sequencer
    https://www.ncbi.nlm.nih.gov/sra?linkname=bioproject_sra_all&from_uid=506922

Started going through the gnuplot book at night.  Going to try to do that in
parallel with the class.

## 2020-01-30

Drove to RIT only to discover class was not being held in person, and we're
supposed to work online instead.  **Welp.**

Installed FastQC locally and got it running.  Really just downloaded the binary
version and symlinked it into place.

Downloading the actual data is taking a while.  While I wait, thinking about
disk setups: now that I have a NAS and have moved my local backups to it, I can
format my previously-for-backup internal drives and use them for actual data.
I really need to spend the time to grok how Linux formats and mounts drives
— I've been flailing and slapping things together and it has mostly worked until
now, but I really should just learn it.  Ordered a copy of the new edition of
the sysadmin book that I remember being really good from my Dumbwaiter days.
Hopefully that will be a good reference.

Finished the FastQC stuff early, so spent a few minutes going through the
gnuplot book.  Random notes:

* The user config file is `~/.gnuplot` (note the lack of an `rc` suffix).
* To stop gnuplot from stealing my goddamn focus: `set terminal … noraise`.
* To show the current value of a setting: `show …`.

Finally got around to writing a first draft of a `lines` utility.  Discovered
and fixed a stupid bug in Adopt in the process.

## 2020-01-31

Now that I've got a more thorough backup system, went through and did my yearly
pruning of unnecessary crap on my hard drive, and adding restic excludes to
avoid backin up track.  Number of scans was cut drastically:

* Directories: 125k to 30k
* Files: 567k to 285k

Much cleaner now.

# February 2020

## 2020-02-01

Fixed up my `$PATH` in my bash profile, for when I'm forced to use bash.

Also had to fix up the uses of `set_color` in my Fish shell config to only
happen for interactive connections, because Fish shits out some errors when you
call `set_color` on a noninteractive connection (e.g. when using `scp` or
`rsync`).  Sigh.

Now that I've got my backups pushed to my NAS (plus off-site) I can repurpose
those 4 TB drives sitting empty in my tower.  Gonna use them for a data dump
site on the Linux side of things, e.g. for all the FASTQs and resulting data
I'll be dealing with for my class this semester.  Read through the sysadmin book
chapters on the filesystem which were *super* helpful.  Decided to pair the
drives as a `btrfs` raid 0 array.  I'm not super concerned with durability here
— everything should be reproducible from the original raw FASTQs from SRA if I'm
doing my job right, so I may as well just have one giant pool of storage.  Also
I don't need this `/dump` to be encrypted — it'll be handling non-sensitive
data.

To get them ready for `btrfs` I used:

* `fdisk` to create new GPT partition tables on each and blow away the old ones.
* Had to use `sudo cryptsetup luksClose` on the previously-encrypted backup
  drive to remove the lingering `sda_crypt` "partition" I was seeing.
* `wipefs` to finish cleaning them completely.

Even with all that, `mkfs.btrfs` complained about a partition table still
existing on one of the drives.  At that point I gave up and passed `-f` to it,
and everything Just Worked.  In hindsight, I bet I could have just done that to
begin with and let `mkfs.btrfs` handle blowing away everything, but it was still
a fun exercise.

Attempted to figure out how to acquire MS Word for the class.  Apparently
there's a web version of Word now?  If I can use that, at least I won't have to
spin up a full Windows VM to write the papers…

Installed `sra-toolkit` from Ubuntu's repository.  Unfortunately it doesn't seem
to come with `fasterq-dump`, only the older `fastq-dump`, at least according to
`dpkg-query -L sra-toolkit`.  Installed the latest binary from their site
instead.

Poked around at both `fastq-dump` and `fasterq-dump`.  `fasterq-dump` seems more
documented and user friendly, and is definitely faster.  The biggest speedup
came from telling it to use RAM as its temporary filesystem with `-t /dev/shm`,
which cut the time down to 1/3.  Guess all this RAM *is* actually good for
something.

After rebooting later, the boot process was suddenly hanging for over a minute.
Another fucking yak to shave.  Figured out how to disable the goddamn splash
screen (edit `/etc/default/grub` to remove `quiet` and `default` and then
`update-grub2`) so I could get some logs.  Eventually saw some systemd horseshit
about `a job is running for dev-disk-by\x2duuid-…`.  Tried to figure out which
drive had that UUID, but none of them did.  After a bunch of flailing in `fstab`
I realized that it might be the UUID of *the old backup drive I killed*.  Sure
enough, there was still an entry in `/etc/crypttab` for it, and a bunch of
systemd shit in `/run/systemd/generator/` left over that I had to clean out.
After that, everything boots fast(ish) again.  I hate computing.

## 2020-02-02

Spent some time cleaning up the `Makefile` for my individual class project.
Learned some stuff about `make` in the process:

* When you have a pattern rule `foo/bar/%.baz`, whatever matches the `%` is
  called the "stem", and you can use `$*` to get the stem inside the rule.
* There are a bunch of ways to allow users to override variables, but the one
  I settled on is to use `VAR := val` in the `Makefile`.  Users can override
  these with `make VAR=newval …`.  This doesn't allow overriding with
  environment variables, but that seems fraught with danger anyway, so let's
  consider it a feature, not a bug.
* I was dicking around a lot with `addprefix` and `addsuffix` unnecessarily
  before.  Much simpler is to use `$(FOO:%=prefix%suffix)`, e.g. `FASTQ_FILES
  := $(KEYS:%=data/00-input/%.fq.gz)`.  This works with multiple-word variables
  too (god help me if filenames ever contain spaces).
* Prefixing a command with `@` prevents `make` from echoing the command before
  executing it (but not when doing a dry run).  Handy for the `echo …` commands
  in `make debug`.
* Management of directory creation is… annoying.  Ended up going with
  placeholder `.ph` files.  Simple but inelegant.  Oh well.

Finished writing up my class project pick paper.

Did more in the gnuplot book.

Updated my `lines` tool to add a `--limit` option and handle broken pipes.
I could have sworn I handled broken pipes in some other Lisp script at some
point, but can't seem to find it now.  I used `sb-int:broken-pipe` but I'm not
sure if that's something I should be relying on.  Need to ask in `#sbcl`.

## 2020-02-04

Class today.  Did a bunch of various things after the lecture (I hope I can
remember it all).

Got the group permissions sorted out on the server in two steps:

* Had the admin [add a `setgid` bit to the team directory][dir-setgid], so new
  stuff in there will get created with the team group as the owner by default.
* Then we all added `umask 002` to our `rc` files to change our default `umask`,
  so when we create files they'll be `664` by default instead of `644`.  This
  isn't a problem for non-team files because they get created with your personal
  group as the group.

[dir-setgid]: https://www.gnu.org/software/coreutils/manual/html_node/Directory-Setuid-and-Setgid.html

Once that was sorted out, started diving into aligning the Trapnell data with
tophat and bowtie.  This is… not pleasant.

First I need to install both tools.  There's an Ubuntu package for `tophat`, but
it wanted to install NodeJS as a prerequisite.  Why on earth does tophat want
NodeJS?  `SIGINT`ed that immediately and downloaded the binary version instead.

The wrapper script `tophat2` tries to set up `$PATH` magically so everything
just works:

    #!/usr/bin/env bash
    pbin=""
    fl=$(readlink $0)
    if [[ -z "$fl" ]]; then
       pbin=$(dirname $0)
     else
       pbin=$(dirname $fl)
    fi
    export PATH=$pbin:$PATH
    $pbin/tophat "$@"

Unfortunately it doesn't try hard enough.  The `readlink` is *attempting* to
deal with symbolic links there, but only works with absolute links — relative
symlinks (e.g. `ln -s ./tophat-…/tophat2 tophat2`) just return the relative
path, which then gets passed to `dirname` and treated as relative from whatever
directory you happen to be in.  And let's ignore all those unquoted variable
expansions I guess.  Sigh.  Better version:

    #!/usr/bin/env bash
    pbin=""
    fl=$(readlink -f "$0")
    if [[ -z "$fl" ]]; then
        pbin=$(dirname -- "$0")
     else
        pbin=$(dirname -- "$fl")
    fi
    export PATH="$pbin:$PATH"
    "$pbin"/tophat "$@"

Once it's installed, I can finally run it.  This is where things get even more
confusing.  After a whole bunch of flailing I think I managed to narrow down
what the hell all these magic parameters are, and how things have changed since
the paper was written.  Notes:

* Bowtie is an aligner — it aligns reads to a reference genome.
* Tophat uses bowtie to align reads, but adds splice-awareness on top.
* To use Bowtie to align, you need to preprocess your reference genome and
  create an index of the genome.
* Additionally/separately, you also need to create a *transcriptome* reference
  genome for the splice awareness.  You do this with tophat, which invokes
  bowtie under the hood.  This means you end up with *two* bowtie indexes:
  a genome index and a transcriptome index.
* To create the genome index: `bowtie2-build --threads 15 foo.fa some/prefix/foo`
  * This creates a bunch of files in `some/prefix` named `foo.…`.
  * Why does this take a basename and not just a directory name?
  * Do the name of the FASTA and the name of the index files have to match?
* To create the transcriptome index: `tophat2 -p 15 --GTF foo.gff --transcriptome-index=another/prefix/bar some/prefix/foo`
  * There are three separate things specified here, each in a different way:
    * The gene annotation file is provided with the `--GTF` option, as a path.  (Even if it's a GFF file, not a GTF file.  There's no `--GFF` option.  Of course.)
    * The genome index is provided with a positional parameter, as a basename.
    * The destination for the transcriptome index is a basename, and it'll splat out a bunch of files with various suffixes there.
* Note that the chromosome names in the `.gtf`/`.gff` file and the sequence
  headers in the `.fa` file must match.
  * This caused me much pain when I was trying to use the `.gtf` file (foolishly assuming `--GTF` required a `.gtf`), the inclusion of which seems to be a trap in the input data laid for the unwary student.  I will not be fooled again.
  * Tophat gave me a completely useless error (`"Couldn't build bowtie index with err = 1"`) when I tried this, rather than tell me anything useful that might have pointed me in the right direction.  Extremely Good Software.
* Some/all of the prefixes/basenames may or may not have to match.  By the time
  I flailed enough to get everything working I had renamed everything to
  a single prefix, but I'm not sure if it was strictly necessary.  I'll
  investigate tomorrow or Thursday, when I'm less annoyed.
* Once you've got the two indexes created, you can run the alignment:
  `tophat2 -p 15 --transcriptome=another/prefix/bar --output-dir baz/ some/prefix/foo *.fq`

That's as far as I got today.  Next step is to clean up this mess and get it
into the `Makefile`.

## 2020-02-06

Refactored the `Makefile` and added in all the alignment stuff.  Wrote up the
weekly report far too late.

## 2020-02-08

Decided to try using gnuplot to do the graphing exercises in the Campbell
Biology textbook, to combine the things I've been reading lately.

The first exercise I did was from chapter 9.  Data:

    Low        4.3
    Normal     4.8
    Elevated   8.7

Gnuplot file:

    set title "{/:Bold*1.5 Thyroid Hormome Levels and Oxygen Consumption}"
    set xlabel "Thyroid Hormone Level"
    set ylabel "Oxygen Consumption Rate [nmol O_2 / (min * mg cells)]"

    unset key
    set boxwidth 0.8

    plot [][0:10] "bio/thyroid" u 0:2:xtic(1) w boxes fillstyle solid fc rgb "black"

That was pretty simple.  Then I went back to a previous chapter.  Data:

    # Time (min)  Concentration of inorganic Phosphate (μmol/mL)
    0               0
    5              10
    10             90
    15            180
    20            270
    25            330
    30            355
    35            355
    40            355

Gnuplot file:

    set title "{/:Bold*1.3 Glucose-6-Phosphate Activity in Isolated Liver Cells}"
    set xlabel "Time (minutes)"
    set ylabel "Concentration of ℗_i (μmol/mL)"

    set xtics format "%h min"

    unset key

    set grid xtics ytics

    set lmargin 12
    set rmargin  6

    plot [0:45][0:400] "liver-glucose" w lines linewidth 2

This one was a little trickier.  I was trying to play around in the gnuplot
REPL, but pasting the Unicode characters was producing garbage at the gnuplot
command line.  Pasting into a normal terminal/fish shell worked fine.  After
much flailing I tracked down the problem to gnuplot itself:

* Gnuplot uses one of several different libraries to handle readline-like
  editing: `libeditline`, GNU `readline`, and some others (I think).
* The library it uses is specified as an argument to `./configure` and linked in
  at compile time.
* `libeditline` does not handle UTF-8 input correctly in this, the year of our
  Lord, 2020.
* GNU `readline` *does* handle UTF-8 input correctly.
* Unfortunately, `readline` is GPL-licensed, which is incompatible with
  gnuplot's license.
* Debian (and Ubuntu) therefore link gnuplot with the broken `libeditline`,
  rather than linking it to `libreadline` and violating the GPL.
* As far as I can tell, there's no way to simply disable all line editing in
  gnuplot so it can be wrapped with `rlwrap` or something.

At this point I just gave up on using Unicode at the REPL and created `.gp`
files that I then `load`.  The GPL strikes again.

## 2020-02-09

Installed R Studio from the `.deb`.  Needed to `apt install r-base` first to get
the dependencies.  It installed… a lot of stuff.  Let's hope it hasn't wreaked
too much havoc.

Moved on to differential gene expression with `cuffdiff`.  Finally starting to
understand what the actual data files are.  The input FASTQs are:

    GSM794483_C1_R1_1.fq.gz
    GSM794483_C1_R1_2.fq.gz
    GSM794484_C1_R2_1.fq.gz
    GSM794484_C1_R2_2.fq.gz
    GSM794485_C1_R3_1.fq.gz
    GSM794485_C1_R3_2.fq.gz
    GSM794486_C2_R1_1.fq.gz
    GSM794486_C2_R1_2.fq.gz
    GSM794487_C2_R2_1.fq.gz
    GSM794487_C2_R2_2.fq.gz
    GSM794488_C2_R3_1.fq.gz
    GSM794488_C2_R3_2.fq.gz

The `C` here apparently stands for "condition".  I still have no idea what
`R[123]` is trying to tell me.  The `_[12]` is the paired-end read pairs.  Would
it kill people to name things more descriptively and/or include a `README` that
explains what all their one-letter abbreviations mean?

Thinking about restructuring the filesystem layout to make the relationships
between the FASTQ files more explicit:

    C1/
        R1/
            GSM794483_C1_R1_1.fq.gz
            GSM794483_C1_R1_2.fq.gz
        R3/
            GSM794484_C1_R2_1.fq.gz
            GSM794484_C1_R2_2.fq.gz
        R3/
            GSM794485_C1_R3_1.fq.gz
            GSM794485_C1_R3_2.fq.gz
    C2/
        R1/
            GSM794486_C2_R1_1.fq.gz
            GSM794486_C2_R1_2.fq.gz
        R2/
            GSM794487_C2_R2_1.fq.gz
            GSM794487_C2_R2_2.fq.gz
        R3/
            GSM794488_C2_R3_1.fq.gz
            GSM794488_C2_R3_2.fq.gz

But I might be too lazy at this point to do it.

The more I work with `make` the more I realize how limited it is.  The general
idea behind it (computing a dependency graph and using it to rebuild things) is
sound, but the implementation is a clusterfuck of string processing and horrific
syntax.  It really gives me the urge to create Yet Another Build System.  Sigh.

Eventually `cuffdiff` finished.  Time to move on.  Tried to install cummerbund
in R, but ran into a bunch of errors.  Had to install numerous third-party
dependencies outside of R:

* `libcurl4-openssl-dev`
* `libxml2-dev`
* `libmariadbclient-dev`

Why on earth does installing cummerbund require a goddamn **MySQL** client?!
This is completely nuts.

Ran into a giant pile of inscrutable errors even after installing all these
bananas dependencies.  Eventually tracked it down to the R version shipped in
the Ubuntu package repository being too out of date to work with some of the
required packages.  I hate volatile software.  Installed a newer version of
R with [this guide](https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-18-04).

Finally managed to get cummerbund working and started graphing stuff.  It mostly
works, but my graphs don't really look quite like theirs.  Need to ask the
professor about this. 

In the mean time, played around with using gnuplot to plot the data instead of
R.  Turned out to be not too bad, since cuffdiff already dumps its output in
a textual format.  Example of the plot comparing the expression levels of the
various genes:

    set logscale
    unset key
    plot "gene_exp.diff" using \
        "value_1":"value_2" lt 3 pt 1 lw 1, \
        x+(0.5*x) lt -1 lw 1 dt 2, \
        x-(0.5*x) lt -1 lw 1 dt 2

I also played around with adding some nicer default `linetype`s to my
`~/.gnuplot` using colors from ColorBrewer.  Fairly happy with the result so
far, but I'll need to play around with them more over time to see if they hold
up.
