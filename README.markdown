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
