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
[The Implementation of Prolog]: http://press.princeton.edu/titles/5264.html
[Coding Math]: http://bitbucket.org/sjl/coding-math/
[Learning WebGL]: http://learningwebgl.com/
[iterate]: https://common-lisp.net/project/iterate/
[parenscript]: https://common-lisp.net/project/parenscript/
[Wisp]: http://bitbucket.org/Gozala/wisp
[CCL]: http://ccl.clozure.com/
[SBCL]: http://sbcl.org/
[The Road]:

## June 2016

### 2016-06-01

* Created this thing.
* Added a fish alias to make it easier to edit.
* Also added a Vim mapping...

### 2016-06-02

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

### 2016-06-03

### 2016-06-04

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

### 2016-06-05

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

### 2016-06-06

* Read more [LOL][].
* Logistic travel stuff.

### 2016-06-07

* [Finished
  rewriting](https://bitbucket.org/sjl/bones/commits/72bbdd5157258b77c85a6c0172240a26bb7ad4a4) the [Bones][] compiler.

### 2016-06-08

* Implemented Aldous-Broder and a bunch of code cleanup for [Mazes][].

### 2016-06-09

* Downloading/updating everything to prepare for my long-ass flight back to the
  states tomorrow.
* Grabbing doc trees with `wget`, but also might try out [Dash][] to see if it
  can reduce this pain a bit.
* Roswell broke when I updated it through Homebrew and I had to manually remove
  all its cached files in `~/.roswell` for it to work again.  Computers are
  garbage.

### 2016-06-10

* Flew back to the states for a short visit.
* Fixed a pair of really nasty bugs in [Bones][] on the plane.

### 2016-06-11 - 2016-06-23

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

### 2016-06-24

* Still jet lagged.  Catching up on things back in Iceland.
* Halfway through [Salem's Lot][].  I forgot how much I loved reading fiction.
* Grabbed a bunch of GDC talks from [this thread][Reddit GDC] to watch later.
* Read more [LOL][].  This dude is a wonderful nutbag.  The chapter on
  efficiency is crazy, but interesting.  I might use some of its ideas in
  [Bones][] once I've got that to a stable place.
* Watched the Juice it or Lose It talk from that Reddit thread.  Really nice.
  Simple stuff like tweening makes a big difference.

### 2016-06-25

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
* Started a blog post about Lisp and symbols which turned into a 5k word
  monster.  Gonna edit it down over the next few days and post it some time next
  week.

### 2016-06-26

* Watched the "Antichamber: An Overnight Success, Seven Years in the Making" GDC
  video.  Pretty inspiring, though I think he still probably underestimates how
  much luck matters.
* Started reading [The Implementation of Prolog][].  Some good ideas and
  explanations in here, though the coding style is maddening.  I might even try
  a clean rewrite of [Bones][] a year or two down the line, using some of the
  concepts I'm seeing here.
* Started doing the [Coding Math][] series again.  Finished episode 28.
* Started back into the [Mazes book][] again.  Implemented Wilson's Algorithm in
  my little [demo][Mazes].

### 2016-06-27

* Printed off and read the manuals for two Lisp things I've been meaning to look
  into: [iterate][] and [parenscript][].
* [parenscript][] seems like an ugly, practical compile-to-JS Lisp.  It's not
  pretty, but it has macros so I make it pretty if desired.  And at least it's
  not abandoned like [Wisp][].
* [iterate][] is neat.  I can definitely see how it's cleaner than `loop`.
  There are some parts that seem tricky, but I have the feeling that they're
  edge cases that I only say because I read the manual cover-to-cover -- I doubt
  they'd appear much in real life.  I really should just bite the bullet and
  start using it -- there's no other way to learn -- but `loop` is like
  a comfortable rut I've found myself stuck in...
* Did the first few lessons of [Learning WebGL][].  So far I understand
  everything (reading the [SuperBible][OpenGL SuperBible] helped a ton).  I'm
  beginning to think graphics programming *seems* really tough because it's
  usually done in weak languages that can't abstract for shit like C and JS.
  Most of the boilerplate in these tutorials could be abstracted away with some
  careful inline functions or macros.  But maybe I'll change my mind once I dive
  in more.

### 2016-06-28

* Finished [Salem's Lot][].  I really want to visit Maine again.
* Did more [Learning WebGL][].  Still pretty smooth sailing.
* More [Coding Math][].

### 2016-06-29

* Watched "Designing Monument Valley" over breakfast.  This style of game isn't
  my particular cup of tea, but the talk was interesting.  He mentioned a few
  times that mechanics get in the way of the storytelling/experience and while
  that can be true, maybe even *most* of the time, I kept thinking about Dwarf
  Fortress as a counterexample.  If you read the DF subreddit or forums you see
  countless stories and characters unfold, each one unique, and all of them
  created by the interaction of the player's imagination and the game's
  procedural mechanics.  I'd love to make a game like that.
* Posted a [blog post](http://stevelosh.com/blog/2016/06/symbolic-computation/)
  about symbolic computation.
* [Added support for dynamic calling](https://bitbucket.org/sjl/bones/commits/de6e248866f44f1b997669339a7cce227305419c)
  (Prolog's `call/1`) in [Bones][].  This lets you write `not/1` trivially,
  which we need for some GDL games.
* Fixed a [nasty unrelated bug](https://bitbucket.org/sjl/bones/commits/05ce726f28744cb1c412e0f450fac3b978a6001d)
  in the `bind!` function of [Bones][]' VM.

### 2016-06-30

* Watched the "Obsessive Compulsive Development" GDC talk over breakfast.  It
  was refreshing to see a talk about a game that didn't turn out to be a huge
  success.  Lots of good advice in it which seems obvious in retrospect, but
  I can see how in the heat of the moment it would be easy to lose sight of the
  bigger picture.
* Did another episode of [Coding Math][].  This one is about writing a tweening
  library.  I ended up writing a ridiculous pair of [tweening
  macros](https://bitbucket.org/sjl/coding-math/src/783609c42ef0955634097267531ee06541275574/src/tween.lisp)
  that will tween arbitrary places with a nice simple UI.  It's much more
  general than the Javascript version, which is limited to tweening (unnested)
  properties of objects.  Want to tween the car of a slot of an entry in a hash
  table?  No problem!  `(tween-place! (car (slot-value (gethash 'foo table)
  'myslot)) 500 2.0 #'tween-linear)`  I shudder to think how you'd do this in
  a language without macros...
* Added support for running [Bones][]' test suite on [CCL][].  Up til now I've
  just been using [SBCL][] for development, but I accidentally opened the wrong
  REPL today and didn't notice until I got a traceback for something stupid
  I typed, so apparently it Just Works™ on CCL too.  SBCL is currently much
  faster, but I'm pretty pleased that it runs correctly on another
  implementation with zero extra effort.  It's *so* nice to be working in
  a language with an *actual standard*.  I put the CCL testing into the
  precommit hook to help keep me honest going forward.
* Ported two GDL games (`hanoi7_bugfix` and `aipsrovers01`) into Bones'
  `examples/` directory.  Now that I can write `not/1` it was trivial, and
  should be trivial for all GDL games.  It is *really* tedious to do by hand
  though, so I really want to write a GDL to Bones translator.  But to do that
  I think I need to sort out the `assert`/`retract` situation.
* More [Learning WebGL][].
* Added the Hunt and Kill algorithm to [Mazes][], and also started diving into
  [iterate][] by switching over a few of the `loop`s.  I'm never gonna learn if
  I don't just force myself to jump in the deep end.

#### Assertion and Retraction in [Bones][]

I've been thinking about the best way to implement the rule assertion/retraction
UI in Bones and I have a few ideas.  The current stopgap UI of "all the parts of
a predicate need to be defined in a single `(rules ...)` call" is *really* awful
to work with.

There are a few ways I could solidify this.  One way would be to delay
compilation of all the predicates until you call a top-level `(compile)`, at
which point all the predicates would be compiled and fixed forever.  This
would let you split apart the rules, but not assert/retract things at runtime
without rebuilding the entire WAM, which is kind of shitty.

On the other end, I could implement full dynamic assertion/retraction.  This
would be the most flexible, but has drawbacks.  There would probably be a lot of
wasted compilation: if you do `(fact (foo 1)) (fact (bar 2)) (fact (baz 3))` it
would compile `foo` three times, throwing the first two away.  I'd also need to
implement a garbage collection algorithm for the code store, which seems like
a lot of work and a large cost at runtime.

An idea I've been rolling around in my head is to try to trade off some
flexibility for speed by using a kind of "stack-based" assertion/retraction
scheme.  You would add rules one at a time and it would delay compiling them
until you call `(allocate-logic-stack-frame)`, at which point it would compile
everything and record the current top of the code store (and which predicates
have been defined).  Then you could define more predicates, as long as they
weren't already used in a previous "frame", and freeze the frame again to use
them.  When you want to retract, you would only be able to pop an entire frame
of predicates in one go.

This gives you less control -- you can only retract entire frames, and if you
want to retract something you defined way back at the start you're also forced
to retract everything that came later.  But the benefit is that you don't have
to suffer useless recompilation, and you don't need to wait for garbage
collection.

This is probably my GGP mindset showing, because this would be perfect for using
with GDL.  When you receive the rules of the game you compile them all, and
freeze the stack.  Then for each state you can just compile and push the `next`
and `does` predicates into the new top frame, and pop it when you're finished
examining the state.


## July 2016

### 2016-07-01

* More [Learning WebGL][].
* Another episode of [Coding Math][].  Penner's easing functions are beautiful
  little functions clouded by a haze of godawful programming style.  I tried to
  write my versions to be a bit more readable, at the expense of some speed.
* Finished [The Road][].  Meh.

### 2016-07-02

* Watched the "Programming Context-Aware Dialog in The Last of Us" GDC talk by
  Jason Gregory.  Really neat stuff.  This is the kind of AAA game I'd love to
  work on.  Vanilla FPS, sports, etc games bore the shit out of me, but The Last
  of Us has a lot more depth to it.

  I admit I did twitch a bit when I saw the infix `(('speaker 'health) > 0.5)`
  notation in their Scheme-like dialog scripting language -- I guess even
  Naughty Dog isn't perfect, hah.
* Shaved a yak related to packages in [cl-nrepl][] that I've been meaning to get
  to for a long time.  Really I need to rewrite that whole project now that
  I'm not a complete noob in Common Lisp.
* Did episode 32 in [Coding Math][].  I decided to use Common Lisp's multiple
  return values for everything this time instead of taking/returning vectors
  everywhere, just to see how it felt.

  Implementing the core functions felt really nice with multiple values, but
  when it came to the drawing code things got a bit more awkward.  Needing to
  use `multiple-value-(call/bind)` to get things done is kind of a pain in CL
  because of how verbose things can get.  I could make some read macros to ease
  the pain, but it's probably not worth it.

  I'm trying to come up with a good rule of thumb for when to use multiple
  values and when not to.  Multiple value return obviously only gives you one
  level of "hierarchy" to work with, so e.g. instead of `(values x1 y2 x2 y2)`
  it's probably better to do `(values point1 point2)`.  Also if the items are
  the same "importance" it's probably also better to just return a structure of
  some kind -- the fact that CL treats the value first differently makes it seem
  like it's special when really `point1` isn't any more important than `point2`.

  I think the general rule I'll follow (for now) is to use multiple value
  returns very sparingly, and only when one of the values is different than the
  rest and is obviously the "most important" one.
* Worked on [Mazes][] some more.  I did a tiny bit more of the [book][Mazes
  book] but mostly it was me playing around with [iterate][].

  Iterate is turning out to be cool.  I made some custom drivers for my maze
  grids and a couple of custom clauses that are really neat.  `(averaging
  (...some expr...) :into some-var)` will keep track of the average of the
  expression over the life of the loop, and `(timing run-time :since-start-into
  v1 :per-iteration-into v2)` sets vars to store timing info.  And they even
  work together -- in `run-stats` I average the per-iteration times together.
* More [Learning WebGL][].

### 2016-07-03

* Watched the "Network Programming for Physics Programmers" GDC talk over
  breakfast.  Impressive results, but I wonder how specific they are to his
  particular data set (or at least the physics engine).
* Did a few more episodes of [Coding Math][].  Ran into a weird issue with
  Sketch's `polygon` function... I'll have to ask vydd about that in IRC the
  next time I have an internet connection.
* Switched [Bones][] over to use `?question-style` for logic variables instead
  of the previous `:keyword-style`.  Aside from updating the tests it was about
  three lines worth of change, which is good.

##### Variable UI in Bones

I'm still not happy with the `?question-style` though.  First, the check becomes
less elegant and efficient:

    (declaim (optimize (speed 3) (safety 0) (debug 0)))

    (defun* variablep (term)
      (:returns boolean)
      (declare (inline keywordp))
      (keywordp term))

    ; disassembly for VARIABLEP
    ; Size: 64 bytes. Origin: #x1006B80692
    ; 92:       4881F917001020   CMP RCX, 537919511               ; no-arg-parsing entry point
    ; 99:       741B             JEQ L2
    ; 9B:       8D41F1           LEA EAX, [RCX-15]
    ; 9E:       A80F             TEST AL, 15
    ; A0:       7506             JNE L0
    ; A2:       8079F145         CMP BYTE PTR [RCX-15], 69
    ; A6:       740E             JEQ L2
    ; A8: L0:   B917001020       MOV ECX, 537919511
    ; AD: L1:   488BD1           MOV RDX, RCX
    ; B0:       488BE5           MOV RSP, RBP
    ; B3:       F8               CLC
    ; B4:       5D               POP RBP
    ; B5:       C3               RET
    ; B6: L2:   488B4119         MOV RAX, [RCX+25]
    ; BA:       483B057FFFFFFF   CMP RAX, [RIP-129]               ; #<PACKAGE "KEYWORD">
    ; C1:       B917001020       MOV ECX, 537919511
    ; C6:       41BB4F001020     MOV R11D, 537919567              ; T
    ; CC:       490F44CB         CMOVEQ RCX, R11
    ; D0:       EBDB             JMP L1

    (defun* variablep (term)
      (:returns boolean)
      (and (symbolp term)
        (char= (char (symbol-name term) 0) #\?)))

    ; disassembly for VARIABLEP
    ; Size: 99 bytes. Origin: #x1006B1C2AF
    ; 2AF:       4881FA17001020   CMP RDX, 537919511              ; no-arg-parsing entry point
    ; 2B6:       7418             JEQ L2
    ; 2B8:       8D42F1           LEA EAX, [RDX-15]
    ; 2BB:       A80F             TEST AL, 15
    ; 2BD:       7506             JNE L0
    ; 2BF:       807AF145         CMP BYTE PTR [RDX-15], 69
    ; 2C3:       740B             JEQ L2
    ; 2C5: L0:   BA17001020       MOV EDX, 537919511
    ; 2CA: L1:   488BE5           MOV RSP, RBP
    ; 2CD:       F8               CLC
    ; 2CE:       5D               POP RBP
    ; 2CF:       C3               RET
    ; 2D0: L2:   488B4A11         MOV RCX, [RDX+17]
    ; 2D4:       8D41F1           LEA EAX, [RCX-15]
    ; 2D7:       A80F             TEST AL, 15
    ; 2D9:       7506             JNE L3
    ; 2DB:       8079F1E5         CMP BYTE PTR [RCX-15], -27
    ; 2DF:       742C             JEQ L6
    ; 2E1: L3:   8D41F1           LEA EAX, [RCX-15]
    ; 2E4:       A80F             TEST AL, 15
    ; 2E6:       751F             JNE L5
    ; 2E8:       8079F1E1         CMP BYTE PTR [RCX-15], -31
    ; 2EC:       7519             JNE L5
    ; 2EE:       0FB64101         MOVZX EAX, BYTE PTR [RCX+1]
    ; 2F2: L4:   4883F83F         CMP RAX, 63
    ; 2F6:       BA17001020       MOV EDX, 537919511
    ; 2FB:       41BB4F001020     MOV R11D, 537919567             ; T
    ; 301:       490F44D3         CMOVEQ RDX, R11
    ; 305:       EBC3             JMP L1
    ; 307: L5:   0F0B0A           BREAK 10                        ; error trap
    ; 30A:       02               BYTE #X02
    ; 30B:       0F               BYTE #X0F                       ; NIL-ARRAY-ACCESSED-ERROR
    ; 30C:       9B               BYTE #X9B                       ; RCX
    ; 30D: L6:   8B4101           MOV EAX, [RCX+1]
    ; 310:       EBE0             JMP L4

In practice this probably won't be too bad (though this is something Bones
checks a *lot* during the initial parsing pass).

On the plus side, it matches what most other logic libraries use, so it's
familiar.  It also matches GDL, so I won't have to transform things when parsing
a GDL game, which is nice.  It'll also let me write a macro to bind results to
variables, which is a nicer UI than having to pull them out of a data structure.

### 2016-07-04

* Watched the "Julia: To Lisp or Not To Lisp?" talk from [ELS 2016][].  I wish
  he had gone further in depth on how Julia does macros.  He showed a simple
  `timeit` macro but I would have liked to know how to introspect the
  expressions a macro gets and work with them.

  One of the things that makes Lisp macros so nice is that the expressions
  macros get (and the tools you use to work on them) are the same kinds of
  things you use everywhere *else* in the language (lists, symbols, etc).  This
  makes it really frictionless to switch back and forth.  If your macros are
  getting some special `AST_Node` type that you need to learn to work with it
  feels a lot more like work.
* Poked around in `#lisp` and `#sbcl` to clear up some performance-related
  questions I had about Lisp arrays.  I have exciting new ideas for [Bones][].
* Added anonymous variables and the `*_void` instructions to [Bones][].  This
  was more difficult than I anticipated, but part of it was a bunch of
  refactoring that had to happen along the way.

### 2016-07-04

* Did the "Intro to Fractals" episode of [Coding Math][].  Fun stuff.  Need to
  play around with animating them like he did at the very end.
* More [Learning WebGL][].
