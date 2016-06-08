.plan
=====

I'm going to try keeping a `.plan`.  Let's see how this goes.

[Bones]: http://bitbucket.org/sjl/bones
[AMOP]: http://www.amazon.com/dp/0262610744/?tag=stelos-20
[Masters of Doom]: http://www.amazon.com/dp/0812972155/?tag=stelos-20
[Mazes book]: http://www.amazon.com/dp/1680500554/?tag=stelos-20
[Mazes]: http://bitbucket.org/sjl/mazes
[ELS 2016]: http://www.european-lisp-symposium.org/
[LOL]: http://www.amazon.com/dp/1435712757/?tag=stelos-20
[WAM book]: http://wambook.sourceforge.net/
[cl-nrepl]: https://bitbucket.org/sjl/cl-nrepl

## 2016-06-01

* Created this thing.
* Added a fish alias to make it easier to edit.
* Also added a Vim mapping...

## 2016-06-02

* Added Prolog list support to [Bones][].  Need to think about the UI more, but
  it speeds things up considerably (I don't *fully* understand *why* yet...).
* Started playing guitar again after a month of so of not at all.  Truss rod is
  all out of whack thanks to the changing weather.
* Read some more [AMOP][].  My brain hurts.
* Read more [Masters of Doom][].
* Noticed the `dynamic-extent` declaration of a `flet`ed function in
  Alexandria's `extremum`... should look into this for the bigass `labels` in
  [Bones][].
* Did a bit more from the [Mazes book][].

## 2016-06-03

## 2016-06-04

* Went to a talk by Tony Hoare at my school.  It was interesting, but the more
  I dive into purely theoretical things the more I realize I really love
  *actually making the computer do things*.
* Started watching the [ELS 2016][] videos.  I wish I could have made it this
  year, but unfortunately my school schedule conflicted.  Next year!
* Asked for help/advice/feedback on the UI for [Bones][]:
  <https://gist.github.com/sjl/1f4bb73967663af0f9276b491af84140>
* Implemented `cut` for [Bones][].  I simplified the book's fuckery quite a bit
  and it turned out to work pretty well, after chasing down a couple of other
  pre-existing bugs.

## 2016-06-05

* Discovered a bug in the [Bones][] compiler, and I think the best way to fix it
  is to rewrite the bulk of the compiler.  This sounds bad, but "rewrite the
  compiler" has been on my list of things to do for a while now, so it's as good
  a time as any.
* The compiler is pretty crufty because it started out with me trying to wrap my
  head around the awful [WAM book][] and grew organically.  Now that I've got
  a fairly solid understanding of how this shit works, my second attempt should
  be nicer.
* Watched more [ELS 2016][] videos.
* Finished reading the main part of [AMOP][].  Gonna put it down and move on to
  [LOL][] instead of trying to power through reading the entire MOP spec.
* Started rewriting the [Bones][] compiler.  Made good progress, will probably
  take another day or so to get working and then another day to clean up.
* I really should go through and type hint all the stuff in that compiler.  The
  type hints have proven useful in the rest of the project.
* Started thinking about what an inspector plugin for [cl-nrepl][] would
  look like.  The "dump the object" code I wrote for the new compiler is ugly
  and painful to write -- if I just had a nice inspector I wouldn't need to fuck
  around with writing it.

## 2016-06-06

* Read more [LOL][].
* Logistic travel stuff.

## 2016-06-07

* [Finished
  rewriting](https://bitbucket.org/sjl/bones/commits/72bbdd5157258b77c85a6c0172240a26bb7ad4a4) the [Bones][] compiler.

## 2016-06-08

* Implemented Aldous-Broder and a bunch of code cleanup for [Mazes][].
