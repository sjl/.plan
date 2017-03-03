[TOC]

[bearlibterminal]: https://bitbucket.org/cfyzium/bearlibterminal
[chancery]: https://bitbucket.org/sjl/chancery/
[cl-blt]: https://sjl.bitbucket.io/cl-blt/
[cl-ggp]: https://sjl.bitbucket.io/cl-ggp/
[cl-losh]: https://bitbucket.org/sjl/cl-losh/
[cl-pcg]: https://sjl.bitbucket.io/cl-pcg/
[clojure-lanterna]: https://github.com/MultiMUD/clojure-lanterna/
[dieharder]: https://www.phy.duke.edu/~rgb/General/dieharder.php
[ELS]: http://www.european-lisp-symposium.org/editions/2017/
[euler]: https://projecteuler.net/
[local-time]: https://common-lisp.net/project/local-time/
[PCG]: http://www.pcg-random.org/
[qud-ds]: https://www.twitch.tv/ptychomancer
[sand]: https://bitbucket.org/sjl/sand/
[scully]: https://bitbucket.org/sjl/scully/
[surreal numbers]: http://www.amazon.com/dp/0201038129/?tag=stelos-20
[temperance]: https://bitbucket.org/sjl/temperance/

# January 2017

## 2017-01-26

* Rebooting this `.plan` after a long absence.  It's a new year!
* Wrote a first draft of my proposal for a talk at [ELS][] 2017.
* Made a little prototype [name generator](https://github.com/sjl/sand/blob/master/src/names.lisp)
  based on some ideas from last week's [Caves of Qud dev stream][qud-ds].

## 2017-01-27

* Polished up my ELS paper.

## 2017-01-28

## 2017-01-29

* Finished and submitted the ELS paper.
* Worked a bit more on a platformer game assignment for a class.  I hate
  graphics/shader programming so much.
* Added a few docs to [cl-ggp][].  Still got a bit more to write.

## 2017-01-30

* Handed off maintainership of [clojure-lanterna][].
* More platformer work.  Finally got the fucking sprite pack working.  I hate
  things with no documentation.

## 2017-01-31

* Got nerd-sniped and ended up implementing [PCG][] in Common Lisp.

# February 2017

## 2017-02-01

* Started working on a constrained game with my team for AGDD.

## 2017-02-02

* Added a bit of juice to the constrained game.
* Finally sorted out the AI/animation bullshit for my minimal game.  Assets
  without docs are the worst.

## 2017-02-05

* More juice to the constrained game.  Been doing non-computer stuff lately.

## 2017-02-06

* Implemented a little easing API in my [sandbox][sand] repo.
* Made the pluralization rules in [Chancery][] slightly less awful.  I should
  just sit down and fix it right some day.

## 2017-02-07

* Chatted with my advisor a bit and solidified my plans for the home stretch of
  [Scully][].
* Made a little Lisp wrapper for [bearlibterminal][].  Learned more about SBCL's
  floating-point traps than I wanted to.

## 2017-02-08

* Worked more on our constrained game with my team.  Got something almost
  game-like now!

## 2017-02-09

* More constrained game work.  It's an actual game now.  Fun.
* Changed all the `#:foo` uninterned symbols in [Temperance][] to regular `:foo`
  keywords.  Memory is cheap.

## 2017-02-10

* Finished the docs and pushed the 1.0.0 release of [cl-ggp][].  I still need to
  submit it to Quicklisp, but I need to submit [Temperance][] first.
* Dusted off my old [Project Euler][euler] repo and did another problem.
* Dumped initial commits of [cl-pcg][] and [cl-blt][] to the internet in case my
  laptop catches fire.  Still lots of work left to do on those.

## 2017-02-11

* Added basic level generation and scrolling to my AGDD minimal game.  Also
  sound.
* Fleshed out [cl-blt][] a tiny bit more.  Ported a little terrain gen demo over
  to it.  It seems promising.
* Wrote a little harness for [cl-pcg][] to test it with [dieharder][].

## 2017-02-12

* Did another [Project Euler][euler] problem over breakfast, and a couple more
  after that.  The early ones are simple to just brute-force.
* More work on the constrained game.

## 2017-02-13

* More [Project Euler][euler].  Math is fun.
* Fixed up the universe-based matching in Scully.  I'll need it soon for the
  percept matching.

## 2017-02-16

* More [Project Euler][euler], this time I had an excuse to poke at
  [local-time][].

## 2017-02-17

* More tiny [Project Euler][euler] problems.
* Finally got the percept filtering in [Scully][] all figured out.
* Cleaned up [Temperance][] and start writing docstrings.  One more "Finishing
  Friday" and it should be ready for an initial release.  Not perfect, but good
  enough for now.

## 2017-02-20

* More [Project Euler][euler].
* Poked a bit more at my minimal game.  It's gonna be *very* minimal.

## 2017-02-21

* Finished the damn minimal game.
* Another [Project Euler][euler] problem.

## 2017-02-24

* Chatted with my advisor and did more work on [Scully][].  The home stretch is
  in sight!
* Tipsy [Project Euler][euler].

## 2017-02-25

* More [Project Euler][euler].
* Watched the first part of the Merry Fragmas 3.0 Unity session.  Multiplayer
  FPS in Unity looks to be not too bad.
* Cleaned up the internal API in [Scully][] a bit.

## 2017-02-26

* More [Project Euler][euler].
* Watched the second part of the Merry Fragmas 3.0 Unity session.

## 2017-02-28

* More [Project Euler][euler].  Problem 51 was painfully underspecified, but
  I finally got the stupid thing.
* Watched the last part of the Merry Fragmas 3.0 Unity session.

# March 2017

## 2017-03-01

* Started poking at a prototype game my teammate made.
* Added a janky priority queue to [cl-losh][].

## 2017-03-02

* Finished the stupid [Project Euler][] poker problem.  This isn't math.

## 2017-03-03

* More [Project Euler][euler].
* Started documenting [Chancery][].
* Started working through [Surreal Numbers][].  I'm going to try to code each
  chapter up after I read it, to make sure I understand everything.  So far I'm
  done with chapter 2.

