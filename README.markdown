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
is a symlink except for a `bootstrap.sh`.  The folder gets `rsync
--copy-links`ed over and then `bootstrap.sh` will symlink all the resulting
files into their places.  Hopefully this should be easier to maintain.  Did
a bunch of cleanup on my bash and fish setups while I was at it.

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
