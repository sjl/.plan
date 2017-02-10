[TOC]

[ELS]: http://www.european-lisp-symposium.org/editions/2017/
[qud-ds]: https://www.twitch.tv/ptychomancer
[cl-ggp]: https://sjl.bitbucket.io/cl-ggp/
[sand]: https://bitbucket.org/sjl/sand/
[scully]: https://bitbucket.org/sjl/scully/
[chancery]: https://bitbucket.org/sjl/chancery/
[temperance]: https://bitbucket.org/sjl/temperance/
[clojure-lanterna]: https://github.com/MultiMUD/clojure-lanterna/
[PCG]: http://www.pcg-random.org/
[bearlibterminal]: https://bitbucket.org/cfyzium/bearlibterminal

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
