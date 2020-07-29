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

## 2020-02-10

Started making some actual gnuplot scripts to draw the stuff from yesterday.
Got a couple of scripts working, but went down a horrific rabbit hole.

First: the graphs produced by cummerbund are titled very poorly ("Genes" is not
particularly helpful).  I'm going to need to chat with the professor to try to
decipher what these graphs are trying to show me.

I reproduced the scatter and volcano plots without too much trouble.  Used the
PDF plotter and came up with the simple printable line styles that should be
okay.

Then I tried to reproduce the first graph, the "distribution of expression
levels for each sample", and all hell broke loose.  First of all, what is this
graph even trying to show?  The title is just "Genes", which is useless garbage.
The y-axis is labelled "Density", the x-axis is pabelled `log_10(FPKM)`, and the
function used to create it is `csDensity`, so maybe this is a kernel density
plot of the `log10(FPKM)` values?  Well, I tried that, and I ended up with
fucking spaghetti in gnuplot — there were hundreds of lines all overlaying each
other instead of the expected single line.  I spent like an hour dicking around
online trying to figure out what the hell gnuplot was doing.  Eventually,
*finally*, I realized no one online was going to help me, and decided to break
things down myself.  I extracted the problematic column from the file and
computed the `log10` values myself in Lisp, and found an issue: some of them are
0, which means their `log10` value is undefined.  After removing those and
replotting, I confirmed that those undefined values were what was causing all
the discontinuities in the original gnuplot kernel density plot — instead of
ignoring the values, it would start a new line every time it hit one.  Christ.
So then I cloned down the cummerbund repo to see how they were handling this.
The code is… not particularly easy to read.  I searched around more online, now
that I realized the problem, and eventually found a post where someone notes
that they add `1` to the FPKM values first, before taking the `log`, to avoid
negative and undefined log values.  So the x-axis label that says `log_10(FPKM)`
is fucking lying — what's actually on the graph is `log_10(FPKM+1)`.  Once
I plugged that in, everything works and the graph looks roughly like theirs.  To
hell with all this, I'm done for tonight.

## 2020-02-11

Class today.  Chatted about various stuff.  The XLOC identifiers aren't actual
identifiers, they're just arbitrary IDs generated during the alignment process.
That explains why I was seeing `0`s when trying to plot the `XLOC_012662`, which
was regucalcin in the paper — it's a different gene in my run, so I'd need to
look up the gene in my own results.  Also talked about P and Q values, and
plotting each to find interesting cutoffs.  I really need to refresh my memory
on how to more easily make histograms in gnuplot.

Started reading [A Curious Moon](https://bigmachine.io/products/a-curious-moon/)
and got about 1/3 of the way through.  An interesting approach to teaching SQL,
though the writing voice is a little bit annoying.  Still turning out to be
a good book though.

Finished the gnuplot book.  It's really, really good.

Finished my weekly report and homework for this week.  Good to have a couple
days of buffer.  Figured out how to build the assignment zip file in
a `Makefile` which was overkill, but "fun":

    assignments/sjl7678-alignment.zip: $(ALIGNMENTS)
    	rm -rf assignments/sjl7678-alignment
    	mkdir -p assignments/sjl7678-alignment/
    	cd assignments/sjl7678-alignment && mkdir -p $(KEY_PREFIXES)
    	mcp 'data/02-alignment/*/align_summary.txt' 'assignments/sjl7678-alignment/#1/align_summary.txt'
    	mcp 'data/02-alignment/*/logs/tophat.log'   'assignments/sjl7678-alignment/#1/tophat.log'
    	cd assignments && zip -r sjl7678-alignment.zip sjl7678-alignment

I'm slowly becoming more and more disillusioned of `make`.  Even though I'm only
using it for what it's actually designed for (running commands to turn files
into new files) it's still a tremendous pain in the ass to do anything
nontrivial.  The "scripting" support is completely batshit string-based munging,
and even the basic definition of any dependencies beyond explicit lists of files
is miserable.

## 2020-02-12

Spent some (far too much) time getting the Trapnell data into Postgres, figuring
out how to ergonomically plot it with gnuplot, and figuring out how to do decent
histogram and CDF plots.  I'm not thrilled with what I came up with, but it'll
have to do for now because it's already 11 PM.

## 2020-02-15

Tracked down the root cause of https://github.com/dimitri/pgloader/issues/1005
— need to write it up in a comment.

## 2020-02-16

Finished the `make` book.  I'm becoming less and less enthusiastic about `make`
the more I learn about it and see real-world examples of it.

Wrote up the pgloader issue debugging comment.

## 2020-02-18

Class today was a lot of chatting and planning ahead for the group project.
Things to think about:

* Need to get a CSV or something together with the sample names and SRA IDs so
  I can map the FASTQ files back to the actual conditions.  Not sure if there's
  a way to pull this metadata out of the raw data files or whether I have to
  type it out by hand like some uncultured swine.
* Need to figure out what the "transcript integrity number" from the paper
  means.
  * Professor wasn't sure.
  * I think I found the paper that created it, so I just need to read it and hope it doesn't go over my head.
* Need to think more about the filesystem layout for the project.
  * Pipeline directories mostly worked in the individual one.  Try that again?
* Need to figure out how we're going to automate the project.
  * Considered trying `redo` but I want it to run on the server, so that's probably out.
  * Could use `make` again even though I'm more and more disenchanted with it every time I try to use it.
  * Could use bash scripts but that seems miserable in different ways.
* I'd really like to try to reproduce the paper with the exact versions of the
  tools they used, as a baseline.
  * This will likely be fucking miserable because modern software has a half life of a year.
  * If I can manage to do that, then I could update the tools and see what changes.
  * Then try different tools and see what changes.

One more big question: need to figure out what the overrepresented sequences
FastQC is complaining about are.  I figured I'd do BLAST searches for them, so
I wanted to get a list of all the overrepresented sequences.  So I need to pull
them out of the FastQC reports… which are HTML files… all on one line.  Did some
horrific `grep`ing to get what I wanted:

     sjl at ouroboros in /dump/karkinos/fastqs/qc
     ><((°> grep -Po 'id="M9".*<h2' *.html | head | grep -Po '<td>.*?</td>' | grep -v 'No Hit' | grep '<td>[ACTG]' | tr -s '<>' '  ' | cut -d' ' -f3 | sort | uniq -c
           2 CCTCACCCGGCCCGGACACGGACAGGATTGACAGATTGATAGCTCTTTCT
           2 CGGACATCTAAGGGCATCACAGACCTGTTATTGCTCAATCTCGGGTGGCT
           2 CTCACCCGGCCCGGACACGGACAGGATTGACAGATTGATAGCTCTTTCTC
           2 CTGCCAGTAGCATATGCTTGTCTCAAAGATTAAGCCATGCATGTCTAAGT
           2 CTGGAGTCTTGGAAGCTTGACTACCCTACGTTCTCCTACAAATGGACCTT
           2 CTGGAGTGCAGTGGCTATTCACAGGCGCGATCCCACTACTGATCAGCACG

     sjl at ouroboros in /dump/karkinos/fastqs/qc
     ><((°> grep -Po 'id="M9".*<h2' *.html | head | grep -Po '<td>.*?</td>' | grep -v 'No Hit' | grep '<td>[ACTG]' | tr -s '<>' '  ' | cut -d' ' -f3 | sort | uniq | xargs -ISEQ grep --files-with-match SEQ *.html | sort | uniq
     SRR6671104.1_1_fastqc.html
     SRR6671104.1_2_fastqc.html

Interesting — only one of the samples has this issue, and the same sequences
appear in both sides of the pair.  Immediately after doing this horrible `grep`
incantation I remembered the `.zip` produced by FastQC and sure enough, there's
a text file in it with the results in a much less awful format.  But I still
needed a janky awk incantation:

     ><((°> awk 'BEGIN { RS=">>END_MODULE\n"; FS="\n" } $1 ~ /Overrepre/ { for (i=1;i<=NF;i++) print FILENAME, $i }' */fastqc_data.txt
     SRR6671104.1_1_fastqc/fastqc_data.txt >>Overrepresented sequences       warn
     SRR6671104.1_1_fastqc/fastqc_data.txt #Sequence Count   Percentage      Possible Source
     SRR6671104.1_1_fastqc/fastqc_data.txt CCTCACCCGGCCCGGACACGGACAGGATTGACAGATTGATAGCTCTTTCT        58594   0.18785731410785536     No Hit
     SRR6671104.1_1_fastqc/fastqc_data.txt CTCACCCGGCCCGGACACGGACAGGATTGACAGATTGATAGCTCTTTCTC        39157   0.12554065004132323     No Hit
     SRR6671104.1_1_fastqc/fastqc_data.txt CTGGAGTGCAGTGGCTATTCACAGGCGCGATCCCACTACTGATCAGCACG        36886   0.11825963218388151     No Hit
     SRR6671104.1_1_fastqc/fastqc_data.txt CTGGAGTCTTGGAAGCTTGACTACCCTACGTTCTCCTACAAATGGACCTT        34457   0.11047205297836592     No Hit
     SRR6671104.1_1_fastqc/fastqc_data.txt CTGCCAGTAGCATATGCTTGTCTCAAAGATTAAGCCATGCATGTCTAAGT        33273   0.10667604895229328     No Hit
     SRR6671104.1_1_fastqc/fastqc_data.txt CGGACATCTAAGGGCATCACAGACCTGTTATTGCTCAATCTCGGGTGGCT        31923   0.1023478349022949      No Hit
     SRR6671104.1_1_fastqc/fastqc_data.txt
     SRR6671104.1_2_fastqc/fastqc_data.txt >>Overrepresented sequences       warn
     SRR6671104.1_2_fastqc/fastqc_data.txt #Sequence Count   Percentage      Possible Source
     SRR6671104.1_2_fastqc/fastqc_data.txt CCTCACCCGGCCCGGACACGGACAGGATTGACAGATTGATAGCTCTTTCT        58938   0.18896020716948458     No Hit
     SRR6671104.1_2_fastqc/fastqc_data.txt CTCACCCGGCCCGGACACGGACAGGATTGACAGATTGATAGCTCTTTCTC        39362   0.12619789736002668     No Hit
     SRR6671104.1_2_fastqc/fastqc_data.txt CTGGAGTGCAGTGGCTATTCACAGGCGCGATCCCACTACTGATCAGCACG        36752   0.11783001686336315     No Hit
     SRR6671104.1_2_fastqc/fastqc_data.txt CTGGAGTCTTGGAAGCTTGACTACCCTACGTTCTCCTACAAATGGACCTT        34782   0.11151403043484702     No Hit
     SRR6671104.1_2_fastqc/fastqc_data.txt CTGCCAGTAGCATATGCTTGTCTCAAAGATTAAGCCATGCATGTCTAAGT        34471   0.11051693816110664     No Hit
     SRR6671104.1_2_fastqc/fastqc_data.txt CGGACATCTAAGGGCATCACAGACCTGTTATTGCTCAATCTCGGGTGGCT        31900   0.10227409495922085     No Hit
     SRR6671104.1_2_fastqc/fastqc_data.txt
     SRR6671105.1_1_fastqc/fastqc_data.txt >>Overrepresented sequences       pass
     SRR6671105.1_1_fastqc/fastqc_data.txt
     …

Some quick `cut`ing and such and I've got what I need, in a slightly less
horrible way.  I guess.

    ><((°> awk 'BEGIN { RS=">>END_MODULE\n"; FS="\n" } $1 ~ /Overrepre/ { for (i=3;i<NF;i++) printf(">%s/%d %s\n", FILENAME, x++, $i) }' */fastqc_data.txt | cut -f1 | sort -k2 | uniq -f1 | tr ' ' '\n'
    >SRR6671104.1_1_fastqc/fastqc_data.txt/0
    CCTCACCCGGCCCGGACACGGACAGGATTGACAGATTGATAGCTCTTTCT
    >SRR6671104.1_1_fastqc/fastqc_data.txt/5
    CGGACATCTAAGGGCATCACAGACCTGTTATTGCTCAATCTCGGGTGGCT
    >SRR6671104.1_1_fastqc/fastqc_data.txt/1
    CTCACCCGGCCCGGACACGGACAGGATTGACAGATTGATAGCTCTTTCTC
    >SRR6671104.1_1_fastqc/fastqc_data.txt/4
    CTGCCAGTAGCATATGCTTGTCTCAAAGATTAAGCCATGCATGTCTAAGT
    >SRR6671104.1_1_fastqc/fastqc_data.txt/3
    CTGGAGTCTTGGAAGCTTGACTACCCTACGTTCTCCTACAAATGGACCTT
    >SRR6671104.1_1_fastqc/fastqc_data.txt/2
    CTGGAGTGCAGTGGCTATTCACAGGCGCGATCCCACTACTGATCAGCACG

Did a BLAST search for these sequences and they're all 18S Ribosomal RNA.
Professor wasn't sure how that could have gotten into the mix, since the paper
says they only used poly(A) RNA.  Need to ask around at work to see if anyone
has any ideas what the heck happened.

(This weirdness is only on sample C0.  Unfortunately that's not the sample the
paper identified as being low quality (C3) so that isn't the issue.)

Did a bit more on the Enceladus book.  Decided to just read the rest, because
the DB/Makefile crap is getting way too messy.  I really need a `sqlfmt` tool,
but every time I try to use smug to write a parser I get depressed.

Merged a GitHub PR into badwolf and tried to pull it down locally with hg-git,
which fucking broke for the millionth time, with a lying error message blaming
hg-prompt.  Fucking fantastic.  Updated hg-git (apparently there's a new repo on
Heptapod since Atlassian is shitcanning BitBucket's Mercurial support) and now
there are four heads on default.  I have no idea which one I'm supposed to use.
I picked the latest one arbitrarily and it seems to work, at least well enough
to pull down the PR.  Good enough.

## 2020-02-19

Finished the weekly report for class.

Fixed the scroll overflow of the code blocks in this site.

## 2020-02-22

Put together some initial structure for the group project.  Got the files
unzipped and FastQC run, so tomorrow I can dive into new stuff.

Tried to track down a human reference genome for use later.  I *think* I got
what I need, but the sites are… not very user friendly.  Will confirm with the
professor in class.

Started reading one of Tufte's books.  Found a beautiful graph from a 1979 paper
(`10.1126/science.206.4421.987`) with a gorgeous plotter font.  Need to try to
find a similar font to use myself.

## 2020-02-23

Did another graphing exercise from Campbell Biology in gnuplot for fun.

Figured out that `dashtype ''` in my style files was causing the *line* to show
as solid, but the entry in the key was blank!  Turns out `dashtype solid` is
what I actually want.  Also learned that I need to explicitly reset that when
I want a solid line, otherwise the dashtypes I set in previous styles will carry
over.

Refined my color plotting style to use dashed lines instead of lighter colors
for types 6-10.  Seems easier to read that way — the light colors were *really*
light.

Figured out how to do linear regression in gnuplot, and made some helper
functions to make it less annoying:

    # lr  = linear regression (the function to fit)
    # lrt = linear regression title

    baselrt(mm, bb, mprecision, bprecision) = sprintf(\
            sprintf("%%.%dfx + %%.%df", mprecision, bprecision), \
        mm, bb)

    lr(x) = m * x + b
    lrt(mp, bp) = baselrt(m, b, mp, bp)

    lr2(x) = m2 * x + b2
    lrt2(mp, bp) = baselrt(m2, b2, mp, bp)

    fit lr(x)  "plant-co2" using "CO2":"Corn"       via m, b
    fit lr2(x) "plant-co2" using "CO2":"Velvetleaf" via m2, b2

    plot [300:1050] \
        "plant-co2" u "CO2":"Corn"       w lp, \
        "plant-co2" u "CO2":"Velvetleaf" w lp, \
        lr(x)  t lrt(3,0)   lt 6, \
        lr2(x) t lrt2(3, 0) lt 7

Looked into why our first few bases are called at lower quality.  Found
[this](http://seqanswers.com/forums/showthread.php?t=61936) which says that it's
because Illumina uses the first few bases to calibrate their quality score
analyzer, and so they mark them as being less confident to account for the
calibration process.  Signed up for that forum (over bare-ass HTTP, sigh) to get
the damn tech note PDF too.

Dug out the old AxiDraw to play around with
<https://anvaka.github.io/city-roads/?q=rochester%2C%20ny&areaId=3600176069>.
First problem: after installing the new AxiDraw version, connecting to the
AxiDraw in Inkscape failed with `Failed to connect to AxiDraw`.  Sigh.  After
much flailing, it turns out the problem was that something had `pip install`ed
the `serial` module, which is some kind of serialization/deserialization
library, and so `import serial` was importing that instead of pySerial, which is
the serial port communication library that happens to use the module name
`serial` too.  Ugh.  So `pip uninstall serial; pip install pySerial` fixed that.
Then I tried to get the `Render > Hershey Text` thing working again, but it
just… did nothing at all.  Looks like there's a *second* Hershey Text plugin,
this time under the AxiDraw extension menu.  I guess I'm supposed to use that
one now?  Who knows?

Played around with how to make a dot plot in gnuplot while the AxiDraw drew
Rochester.  First I grabbed the read counts for our various FASTQ files, pulled
from the FastQC output files:

    ffind _data.txt \
        | xargs grep 'Total Sequences' \
        | sed -Ee 's|./([^/]+)_fastqc/.*\t|\1 |' \
        | sort --stable -k1,1 -r \
        | sort -k2,2 -n \
        > seqs.txt

    cat seqs.txt | head -n2
    C3_1 21081615
    C3_2 21081615

Then I can plot a dot plot with something like:

    # https://twitter.com/stevelosh/status/1231434196213796864
    set termoption font "Routed Gothic,12"

    # I wonder if there's a way to capitalize stylistically
    set title "READ COUNTS OF INDIVIDUAL FASTQ FILES"
    set xlabel "READS (MILLIONS)"

    # major x tics every 2 million, with 2 minor divisions per major (i.e. minor tics are every 1 million)
    set xtics 2
    set mxtics 2

    set grid y nox

    # left justify
    set ytics left offset -2.2, 0.0

    unset key

    #                                     scale to millions by hand
    #                                                       read FASTQ names from file
    plot [20:35][-1:26] "seqs.txt" using ($2 / 1000000.0):0:ytic(1) lc rgb 'black'

And I get something like:

![plot](https://i.imgur.com/YAPXHaQ.png)

Neat!

Hacked together some Awk to remove overrepresented sequences.  **But** I don't
think a simple `grep -v` approach works, because the two FASTQ files are
expected to have the paired reads at the same positions in the file.  So if we
remove a read from one file but not the other, now all the reads are going to be
offset.  So we need to remove these reads a bit more carefully (really, we need
tools that process the paired-end reads together).  Need to think about this
a little bit more.

## 2020-02-24

Figured out how to mount a directory on my home machine on my laptop with SSHFS,
in advance for tomorrow in case I need it:

    # mount
    mkdir ~/foo
    sshfs -o idmap=user sjl@server:/whatever ~/foo

    # unmount
    fusermount -u ~/foo

Downloaded STAR and got it running.  Read through the manual which, despite the
broken English, was fairly useful.  Tried running it on the gzipped reference
genome but it complains that it requires the genome to be uncompressed.  Tried
to trick it into working by psubbing `zcat` but that didn't work.  Gave up and
decompressed the damn reference.

Once the genome index was built, started aligning the reads.  It failed right
away complaining about a zero-length read.  `zcat | grep`ing showed the read as
being there in both files, *but* I bet this was an issue of the pairs getting
out of sync because we grepped out the overrepresented sequences naively.  Tried
restarting the alignment on the original data and it's still going, so that's
probably it.  Need to figure out how to filter those bad reads properly tomorrow.

## 2020-02-25

Class.  Chatting about QC and such.

Professor says he asked around and people haven't seen the first 5 bases being
lower quality before, but that the explanation from Illumina makes sense, and
that we should *not* trim those bases unless they seem to be causing issues.
Also talked about how to filter out the overrepresented sequences — he thought
fastx had something for this, but I can't seem to find anything in the
documentation.  I may need to write some code.

Professor installed `pigz` on the server, so I can remove my hacky `xargs`
workaround.

Need to find a way to filter bad sequences from BOTH files at once.

Need to align to the NCBI reference GTF instead of the other weird one.

## 2020-02-26

Tried rebuilding the genome index with the other GTF file.  Initially got:

    Feb 26 21:00:45 ..... inserting junctions into the genome indices
    terminate called after throwing an instance of 'std::bad_alloc'
      what():  std::bad_alloc
    ./src/03-index-genome.sh: line 19: 14902 Aborted                 (core dumped) STAR --runThreadN $CORES --runMode genomeGenerate --genomeDir data/03-genome-index …

That seems… bad.  But perhaps this is because I didn't have enough RAM, because
I still had my Lisp process from 2 days ago open consuming ~25 GB of RAM.
I killed that so I've got about 60 GB now.  Let's see if that helps.  Otherwise
it sounds like I may need to look at [this](https://github.com/alexdobin/STAR/issues/103).

Still need to find that other paper my partner found from the same people.

Submitted weekly report.

# March 2020

## 2020-03-16

Installed TrimGalore.  Had to install `cutadapt` first, which is some Python
package.  Luckily it's `apt install`able so I did that, then grabbed TrimGalore
which is blessedly self-contained.

Installed pardre.  The "release" is just a source dump of C++ files with no
`README`, cool.  Had to install `mpi-default-dev` to get `make` to work.  Gross.

Used ParDRe to dedupe a couple of the samples as a test.  It took 927 seconds to
finish the first pair, where I used the `.fastq.gz` files as input and the `-z`
option to enable compression.  I noticed a bunch of the time (the last 700
seconds or so) was spent bottlenecked on a single CPU core while writing the
output.  So then I tried the next sample without compression, and it took 309
seconds.  Welp.

Ran FastQC on the first two sample results.  For the most part FastQC is happy
now, but there *are* still some duplicated sequences left.  I'm guessing this is
because ParDRe is paired-end aware, and will only remove a pair if *the entire
thing* is a duplicate, while FastQC works only on a per-fastq basis.  I don't
know this for sure though.

I did the initial run with 0 mismatches allowed.  We should also try with
N mismatches, though note that this will not work perfectly because ParDRe
clusters reads by their prefix, so reads with `<=N` mismatches in their prefix
(and none in the suffix) will not be caught because they'll never get compared.
Welp.

Cleaned up the scripts to run all the ParDRe runs (0/1/2 mismatches for every
pair) and FastQC them.  Seems to take roughly 5 minutes per pair to do ParDRe.
We have 13 pairs, so it should take around an hour per mismatch setting (i.e.
3 hours) to do them all.

ParDRe finished.  Results look reasonable.  There's not a *ton* of difference
between 0 and 1 mismatch (there is *some* though).  The difference between 1 and
2 is minimal.  Next step is to trim low-quality stuff with trim galore.  Gonna
do that during "class" tomorrow and let it run while I'm at work.

## 2020-03-17

Started sketching out some trimming scripts using Trim Galore.  It has a bunch
of options — I'm not really sure how to go about deciding what the correct
values for each are, other than… try some and see if the resulting FastQC run
seems reasonable?

Attempted to do something foolish: update software.  I wanted to fix the StumpWM
window/frame focus thing, but I figured I would update StumpWM and SBCL and my
dotfiles first.  Clearly, this was a mistake.  I updated all of them, added the
fix, and restarted StumpWM, and everything went to shit.  StumpWM suddenly
started chewing up tons of a CPU core, lagging to hell, and Firefox and Chrome
wouldn't even open.  Tried reverting back to the previous versions but it didn't
work.  Eventually I SSH'ed into the machine and rebooted it, and *then*
everything started working again.  I think.  We'll see.  Going to give up on
updating for today — wasted enough time dicking around with this tonight.
I hate computers.

## 2020-03-18

Debugged a gnuplot issue a bit in IRC with someone.  I think I'm losing my mind.

Submitted weekly report for class.

## 2020-03-19

Met with the professor for office hours to chat about the deduplication/trimming
results.

For deduplication, we first talked about what might cause the actual problem
it's trying to solve.  A cell may have many duplicate copies of a particular
mRNA floating around if the gene is highly expressed — this is exactly what
RNAseq is trying to measure.  However, once those mRNAs are fragmented, it's
extremely unlikely that they would fragment *exactly* in the same place, and so
when you sequence the resulting fragments they should be offset from each other.
If you see exact duplicate reads, it means that the *fragment* was somehow
duplicated, which is probably an artifact of your laboratory process and not
biologically significant.

Next: mismatches.  ParDRe supports removing duplicates with up to N mismatches,
so we talked about why we might want to do this.  If two reads match with `N
> 0` mismatches it indicates one of the following:

* It's the same problem as the exact duplicates, but with an extra error
  accumulated during the process (e.g. a sequencing read error or a PCR
  duplication problem).
* It's from two genes that are very biologically similar, and so is genuine
  useful information.  However, this is still unlikely because the fragments
  would likely be shifted as described above.

At the end he recommended deduplicating with 1 mismatch.

Another complication: ParDRe can operate in paired-end mode, which means that in
some cases FastQC still finds some duplication.  This happens when one side of
the read is an exact duplicate while the other is not.  ParDRe does not remove
this (because of the non-duplicate side) but FastQC only looks at the individual
FASTQs.  He said this is not a problem, and that ParDRe is doing what we want.

Also chatted a bit about trimming.  We mostly talked about the issue mentioned
in the Trim Galore documentation: because it trims *any* matching adapter
sequences, it will *always* trim off a particular base at the end of a read
(because that one base always matches the adapter sequence's last base).  This
is not ideal.  He recommended running Trim Galore and requiring at least adapter
5 bases to match before trimming to deal with that issue.

Plan for today: rerun the trimming with the 5 base requirement and using the
1 mismatch deduplication data as the source, and then kick off an alignment if
I still have time (unlikely).

Neomutt has suddenly started shitting the bed and failing to quite with `Unable
to write` errors.  I *hate* software.  Tried updating to the latest `master` and
rebuilding.  I guess we'll see if it fixes things.

Trimming finished.  It looks like increasing the minimum adapter length to
5 fixed the base imbalance issue.  Good.

Decided to rebuild the STAR index I had made because I can't remember whether
I had already rebuilt it with the different reference file.  Shouldn't take too
long.

Index rebuild finished in ~35 minutes.  Kicked off the 26 alignment runs.  That
should take a lot longer.

Checked in on the STAR progress.  It's actually only taking ~5-10 minutes to run
each alignment.  That's not nearly as bad as I expected.

Initial alignments finished.  Started digging into what I can actually *do* with
the results.  I found the Integrative Genomics Viewer (IGV) that seems
promising.  Downloaded it and loaded the genome into it, then tried to load the
alignments but apparently it wants BAMs, not SAMs, and additionally it wants
indexes of the BAMs.

I looked into how to convert the SAMs to BAMs+indexes.  Went down a bit of an
unnecessary rabbit hole, but it was still productive.  My initial attempt was
using `samtools` to do a bunch of conversion:

    STAR … # produces Aligned.out.sam

    samtools view -S -b Aligned.out.sam > sample.unsorted.bam
    samtools sort sample.unsorted.bam > sample.bam
    samtools index sample.bam

This worked, but took a while and wrote a bunch of intermediate files I don't
really need.  Eventually I realized that STAR can produce sorted BAM files
itself, so all I need to do with `samtools` is the final indexing.  Learned
a bunch about running STAR too.  One nice way to save time across all the
alignments is to have STAR load the genome index into shared memory once at the
beginning and use it for all the alignments, the flush it out at the end:

    function cleanup {
        STAR --genomeDir "${genome}" --genomeLoad Remove
    }

    trap cleanup EXIT

    STAR --genomeDir "${genome}" --genomeLoad LoadAndExit

Then the STAR invocations look like:

        STAR \
            --runMode alignReads                \
            --runThreadN $CORES                 \
            --genomeDir "${genome}"             \
            --genomeLoad LoadAndKeep            \
            --limitBAMsortRAM "${sortram}"      \
            --outSAMtype BAM SortedByCoordinate \
            --outBAMcompression 0               \
            --outBAMsortingThreadN $CORES       \
            --outFileNamePrefix "${outdir}/"    \
            --readFilesIn "${in1}" "${in2}"

I tried putting the temporary directory on `/dev/shm` but it ended up being too
much with the persistent genome index also in RAM.  Unfortunately my order from
Crucial is still backordered.  Oh well, I'll just watch more TNG while I wait
for all the alignments to complete.

## 2020-03-31

Ran the Trapnell plots from the paper on our data.  Results seem at least
plausible on the surface.  Pinged my partner to see if his plots match.

Attempted to install RSeQC to do the TIN score stuff mentioned in the paper.
Ran `pip3 install RSeQC` as described in their docs, but that failed with:

    ValueError: no cython installed, but can not find pysam/libchtslib.c.Make sure that cython is installed when building from the repository

After some searching online I found that this can be fixed by upgrading pip with
`pip3 install --upgrade pip`.  It's… fine, I guess?

Once I got it installed, I tried running `tin.py` to produce the TIN scores.
The script wants the BAM (which I have) and a "BED" file.  BED apparently stands
for Browser Extensible Data and is a TSV file with lines like this:

    chr1	67092175	67109072	XM_011541469.1	0	-	67093004	67103382	0	5	1429,187,70,145,44,	0,3059,4076,11062,16853,
    chr1	67092175	67131183	XM_011541467.1	0	-	67093004	67127240	0	9	1429,187,70,106,68,113,158,92,42,	0,3059,4076,11062,19401,23176,33576,34990,38966,
    chr1	67092175	67131227	XM_017001276.1	0	-	67093004	67127240	0	9	1429,187,70,145,68,113,158,92,86,	0,3059,4076,11062,19401,23176,33576,34990,38966,

The collections of stuff I downloaded from UCSC didn't include one of these, but
the RSeQC site has one available for download.  Actually, it has several BED
files.  I'm not sure which one is correct.  I downloaded `hg38_RefSeq.bed`
because it sounds the most like the GTF I used (`hg38.ncbiRefSeq.gtf`).  Was
that correct?  Who knows?

Now that I have that, I'm doing an initial run with:

    tin.py --input data/05-alignment/clean/C0/C0.bam -r data/00-raw/hg38_RefSeq.bed

It seems like it's going to take a long time.  Guess I'll wait.

The goddamn thing didn't output an ending timestamp.  Come *on*.  It took
somewhere between 2-5 hours, but I have no idea how long because I wasn't
watching it when it finished.  I guess I'll do another run with a `time` prefix.
Sigh.

# April 2020

## 2020-04-04

Spent an hour wrangling gnuplot for class to try to make a multiplot of the TIN
scores.  Mostly it was just a bunch of fiddly stuff to try to make the graph
look exactly like I wanted.  Some of the key points follow.

Basic multiplotting happens with:

    set multiplot \
        title "TIN Score Distributions by Sample" font ",14" \
        layout 3,5

    …

    unset multiplot

Looped through the samples with this:

    do for[c=0:9] {
        set title "C" . c
        bad = (c == 3)
        plot [][0:1] "data/05-alignment/tin/C" . c . ".tin.xls" using 5:(1) smooth cnorm notitle lw 3 \
            lc (bad ? 3 : '#000000') \
            lt (bad ? 6 : 1)
    }

    do for[n=1:3] {
        set title "N" . n
        bad = (n == 2 || n == 3)
        plot [][0:1] "data/05-alignment/tin/N" . n . ".tin.xls" using 5:(1) smooth cnorm notitle lw 3 \
            lc (bad ? 3 : '#000000') \
            lt (bad ? 6 : 1)
    }

Note the `smooth cnorm` requiring the columns to be `using
data-column:literal-value`.  This tripped me up for a while — I was doing `using
0:data-column` and that was fucking things up completely.  I realized the
problem when I noticed there wasn't a peak at zero, and also that sorting
changed the results (which it shouldn't).  `smooth cnormal` needs exactly one
column of the value, plus a weight value for the point.  Remember this!

You can skip around the plot with `set multiplot next` and `set multiplot prev`.
Handy for adjusting the layout.

Instead of trying to draw labels on every graph, I decided to try putting a key
at the bottom right.  This was very fiddly:

    set multiplot next

    $empty << EOF
    EOF

    set termoption fontscale "0.1"
    set title "{/*0.9 Key}"

    set ylabel "{/*0.9 CDF}"
    set xlabel "{/*0.9 TIN Score}"
    set format x "{/*0.9 %g}"
    set format y "{/*0.9 %.2f}"

    set origin 0.75,0.0
    set size 0.25,0.33

    plot [0:100][0:1] $empty using 1:(1) smooth cnorm notitle

Note the `%g` for "humanized" formatting.  I'm going to remember the `g` as
standing for `god dammit, what is the magic character?`.

## 2020-04-11

Merged some PRs for `t` and did some basic test maintenance.  I still love
`cram` for CLI tests — it's such an intuitive, usable way to test things.

# July 2020

## 2020-07-18

More work on Jarl.

Started going through The Data Compression Book, doing the examples in Common
Lisp.  First code was a bit stream wrapper.  I initially did
a `trivial-gray-streams` wrapper but then refactored it into simple structs,
since it's going to be writing a lot of bits and performance probably matters.
Maybe.

## 2020-07-19

Did some server upgrades I've put off too long.  Need to script up some stuff
for automagically doing this in the future.  Might be a good excuse to learn
`expect`?

PR'ed Quicklisp to move my projects from Bitbucket/Github to my self-hosted
setup.  At least now I own my availability and won't have to do this bullshit
again.

Imported a couple of contributed patches to `hg-prompt`.  I'm glad people still
find it useful.  Also took the time to port the documentation to `d` because it
was using some Python wiki bullshit thing before.

Did some more work on The Data Compression Book.  Wrote up a little `main`
skeleton for the binaries.  Might use this as an excuse to try out subtask-style
interfaces in Adopt.  I think it'll work, but I haven't actually tried it yet.

## 2020-07-26

Finally finished reading ULSAH.  Took a few months, but aside from skimming over
20% that wasn't super relevant it was as good as I remember back from 2008.
Lots of things I need to look deeper into and try out on my own:

* `strace` and friends.
* Performance monitoring stuff: `sar`, `vmstat`, `iostat`, etc.
* VMs using KVM and Qemu instead of Virtualbox.
* Learn more about `systemd` (unfortunately).
* Poke at `btrfs` a bit more using my existing setup.
* Look into Ansible as a configuration management system — it seems the simplest
  of the Puppet/Chef/Salt/Ansible crew.
* Building machine images with Packer.
* Look into Terraform for deployment.
* Restructure local wifi into main/guest networks.

## 2020-07-28

Did a bit more work on Jarl.  It's actually coming together.  Still got a bunch
of things on the TODO list but I poked at the GitHub API with it a bit and it
already works surprisingly smoothly.  Neat.
