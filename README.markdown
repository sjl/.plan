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
[Dash]: https://kapeli.com/dash
[Roswell]: https://github.com/roswell/roswell
[ANSI Common Lisp]: http://www.amazon.com/dp/0133708756/?tag=stelos-20
[Successful Lisp]: http://www.amazon.com/dp/3937526005/?tag=stelos-20
[CLtL2]: http://www.amazon.com/dp/1555580416/?tag=stelos-20
[OpenGL SuperBible]: http://www.amazon.com/dp/0672337479/?tag=stelos-20
[CEPL]: https://github.com/cbaggers/cepl
[On Writing]: http://www.amazon.com/dp/1439156816/?tag=stelos-20
[Salem's Lot]: http://www.amazon.com/dp/0307743675/?tag=stelos-20
[Reddit GDC]: https://www.reddit.com/r/gamedev/comments/4oodum/what_are_some_of_the_best_gdc_talks/

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

## 2016-06-09

* Downloading/updating everything to prepare for my long-ass flight back to the
  states tomorrow.
* Grabbing doc trees with `wget`, but also might try out [Dash][] to see if it
  can reduce this pain a bit.
* Roswell broke when I updated it through Homebrew and I had to manually remove
  all its cached files in `~/.roswell` for it to work again.  Computers are
  garbage.

## 2016-06-10

* Flew back to the states for a short visit.
* Fixed a pair of really nasty bugs in [Bones][] on the plane.

## 2016-06-11 - 2016-06-23

* Traveling in the US.  I miss American food.
* I had left a cache of paper books at a friend's place in the US, so I read
  through a few while I was there.
* Read through [ANSI Common Lisp][].  Pretty basic, nothing too advanced in it.
  It reminded me how much I hate Paul Graham's function/variable naming style.
  Aim for brevity of *ideas*, not characters.
* Read/skimmed [Successful Lisp][].  Also pretty basic, but kind of weird at the
  same time.  It seemed to just skim a lot of topics and not really go in-depth
  enough on any of them.  Except for the chapter about the bit-twiddling
  operations, which I haven't seen in any other Lisp book (except maybe
  [CLtL2][]).  I don't think I'd recommend it.
* Read through most of the [OpenGL SuperBible][].  Graphics programming is some
  really neat and powerful stuff wrapped in a hilarious nest of disgusting
  syntax and boilerplate.
* I really want to play around with shaders and such, but the C++ development
  environment seems like an enourmous pain in the ass.  There's also [CEPL][]
  but I'm worried that I should really know some OpenGL before diving into that.
  I might poke at WebGL a bit as a middle ground.
* Read through [On Writing][] by Stephen King.  Some good advice in there,
  especially about just reading and writing a *lot*.  I haven't been reading
  enough lately -- so from now on the Kindle is gonna replace my phone while on
  the bus.

## 2016-06-24

* Still jet lagged.  Catching up on things back in Iceland.
* Halfway through [Salem's Lot][].  I forgot how much I loved reading fiction.
* Grabbed a bunch of GDC talks from [this thread][Reddit GDC] to watch later.
* Read more [LOL][].  This dude is a wonderful nutbag.  The chapter on
  efficiency is crazy, but interesting.  I might use some of its ideas in
  [Bones][] once I've got that to a stable place.
* Watched the Juice it or Lose It talk from that Reddit thread.  Really nice.
  Simple stuff like tweening makes a big difference.

## 2016-06-25

* Watched the "Ellie: Buddy AI in The Last of Us" GDC talk over breakfast.  It
  was really interesting.  The idea that making Ellie stick close to the player
  means that any mistakes become the player's fault (so they won't blame her)
  seems obvious now, but wasn't before I watched it.
* Finally finished up a blog post that's been halfway done for months.  Might
  post it on Monday.
* Finished [LOL][] (though I had to tap out halfway through the final Forth
  chapter).  My dude certainly has a lot of fresh, hot, steaming takes.  I'd
  recommend the book, but only with a rabbit-sized grain of salt.
* Watched the [ELS 2016][] talk "Type Checking on Heterogeneous Sequences in
  Common Lisp".  Seems a lot like the Clojure spec stuff that was released
  shortly after.
