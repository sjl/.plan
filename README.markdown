.plan
=====

I'm going to try keeping a `.plan`.  Let's see how this goes.

[TOC]

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
[sandbox]: http://bitbucket.org/sjl/sand/
[hype]: http://bitbucket.org/sjl/hype/
[The Road]: http://www.amazon.com/dp/0307387895/?tag=stelos-20
[ancg]: http://www.amazon.com/dp/0470018127/?tag=stelos-20
[heisler]: http://www.amazon.com/dp/0823085651/?tag=stelos-20
[WebGL Fundamentals]: http://webglfundamentals.org/
[Neovim]: https://neovim.io/
[miniyank]: https://github.com/bfredl/nvim-miniyank
[YankRing]: http://www.vim.org/scripts/script.php?script_id=1234
[Paredit]: https://github.com/vim-scripts/paredit.vim
[PAIP]: http://www.amazon.com/dp/1558601910/?tag=stelos-20
[policy-cond]: https://bitbucket.org/tarballs_are_good/policy-cond
[cl-charms]: https://github.com/HiTECNOLOGYs/cl-charms
[Silt]: http://stevelosh.com/blog/2015/12/ludum-dare-34/
[99 Prolog Problems]: http://www.ic.unicamp.br/~meidanis/courses/mc336/2009s2/prolog/problemas/
[cl-ggp]: http://sjl.bitbucket.org/cl-ggp/
[taop]: http://www.amazon.com/dp/0262192500/?tag=stelos-20
[ggp-book]: http://www.amazon.com/dp/1627052550/?tag=stelos-20
[ooze]: https://bitbucket.org/sjl/dotfiles/src/default/vim/bundle/ooze/
[Lisp Hackers]: https://leanpub.com/lisphackers/read
[Hillbilly Elegy]: http://www.amazon.com/dp/0062300547/?tag=stelos-20
[Hillbilly Elegy Interview]: http://www.theamericanconservative.com/dreher/trump-us-politics-poor-whites/
[Engines of Logic]: http://www.amazon.com/dp/0393322297/?tag=stelos-20
[diagonalization]: https://en.wikipedia.org/wiki/Cantor's_diagonal_argument
[lispjamaugust16]: https://itch.io/jam/august-2016-lisp-game-jam
[Silt2]: http://bitbucket.org/sjl/silt2
[cl-ecs]: https://github.com/lispgames/cl-ecs
[cl-losh]: http://bitbucket.org/sjl/cl-losh
[DCSS]: https://crawl.develz.org/
[beast]: http://bitbucket.org/sjl/beast
[IRDC talks]: https://www.reddit.com/r/roguelikes/comments/4wwlx2/are_any_of_the_talks_from_the_recent_irdc_getting/
[New England Lisp Games Conference talks]: http://xelf.me/nelgc-videos.html

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

* [Finished rewriting](https://bitbucket.org/sjl/bones/commits/72bbdd5157258b77c85a6c0172240a26bb7ad4a4) the [Bones][] compiler.

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

### 2016-07-05

* Did the "Intro to Fractals" episode of [Coding Math][].  Fun stuff.  Need to
  play around with animating them like he did at the very end.

* More [Learning WebGL][].

* Spent most of the day implementing the "logic stack" assertion/retraction
  I [rambled about](https://gist.github.com/sjl/1f4bb73967663af0f9276b491af84140)
  a while back.

    It works, and it looks pretty good in action!  It also cut the time in my
  little benchmark almost in half (because we only need to compile the state
  code once instead of like 3+ times at each node), and it's MUCH nicer to read
  rule definitions now.

    I'm thinking that programatically parsing/running GDL games is actually
  feasible now, so I think that'll be my next step.  Once I can run arbitrary
  GDL games without having to translate the logic by hand I'll have a LOT more
  nice test cases.

### 2016-07-06

* Cleaned up the UI of [Bones][] a bit.  The new function/macro pairs are a lot
  cleaner to read and work with.

* Got a couple of books out of the RU library before it closes for a few weeks
  in the summer.  Started going through [Algorithms and Networking for Computer
  Games][ancg] and made a little [sandbox][] repo to play around in.

* Hacked together a quick [proof of concept][hype] GDL player that can read and
  search arbitrary GDL games.  It's so nice to see things finally starting to
  come together!

### 2016-07-07

* Chatted with my advisor about [Bones][] and GGP stuff.  Lots of new ideas!

### 2016-07-08

* More [Coding Math][].

* After rereading the section of the [WAM book][] on anonymous variables
  I realized I could clean things up a lot in [Bones][].  I *knew* it had to be
  easier than I was making it.

* More [Mazes][].

### 2016-07-09

* Watched the "Designing Downwell Around One Key Mechanic" GDC talk over
  breakfast.  No revolutionary ideas in it, but I love "case studies" of
  really well-done things like this.  It's the same reason I love books like
  Gregory Heisler's [50 Portraits][heisler] -- you can learn a lot from
  listening to someone experienced talk about what goes through their mind as
  they create something.

* Finished the [Learning WebGL][] series.  I'd definitely recommend it.  It's
  a really good introduction to OpenGL if you just want to learn how the damn
  graphics card works without fucking around with the nightmarish C/C++
  build/ecosystem.  Just open a browser and start hitting OpenGL.

* Started the [WebGL Fundamentals][] series.  I want to get a second look at
  this stuff before I dive in and try to poke at it with Lisp.

* Started screwing around with [parenscript][] in my little [sandbox][].

* Poked a bit more at the [ANCG book][ancg].  Gonna try to take this one in
  bite-sized pieces.

* More [Coding Math][].

* Poked around at some basic GGP games, which revealed some bugs and memory
  problems in [Bones][], so I fixed them.

### 2016-07-10

* Watched the "Learning Through Failure - Portico" GDC talk.  Short but good.
  I think the best idea in is was "players only learn through failure when they
  *understand* what went wrong".

* Brain dumped some stuff about [Bones][] below.

* Removed the stupid garbage `set-*` opcodes from Bones and consolidated them
  into the `unify-*` opcodes like God intended.  Proceeded to rename those
  stupid `unify-*` opcodes to `subterm-*` so mortals can understand what the
  fuck is going on.

* Poked a bit and pushing the constant optimization down into the compilation
  phase, but ran into a bit of a wall so I threw away the diff.  Might take
  another stab at it later once I let it roll around in my head a bit.

* Mostly refactored the Bones code store to be a `simple-array`, after profiling
  indicates that most of the runtime is spent in data vector refs.

#### Splitting the Bones Store

Up until now I've been writing [Bones][] as mostly a transliteration of what's
in the [WAM book][].  This means, for example, that the heap/stack are just
arrays of bytes in memory.  This made it easy to follow along with the book, but
I'm at the point now where I feel like I've wrapped my head around it and am
ready to move on.  My idea for the next big step in Bones is to split the store
into two separate arrays.

The WAM store consists of "cells", each of which has a type and a value.  For
example, reference cells have a type of `REF` and their value is an
index/pointer to whatever they're bound to.  Because I wanted to pack everything
into a single Lisp array, I've implemented this by storing a cell as an
`(unsigned-byte 16)` with a few of the low-order bits used for a type tag.  So
to check the type of a cell, you mask off everything but the low-order bits.  To
get the value, you shift it right.

This works, and is pretty memory-efficient, but has a couple of problems.
First: you need to do masks and shifts all the time which are extra
instructions.  But that's probably not a really huge problem in practice -- CPUs
are fast.  The bigger issue is that because the value of a cell has to be packed
into part of an `unsigned-byte`, you can basically only store integers as cell
values.  For `REF` (and `STR`) cells this is fine (they're just indexes into the
store array), but for functor cells it's not ideal.  Bones currently keeps what
is essentially a symbol table to map functor/arity pairs to integers, which is
really ugly.

This is an annoying layer of indirection, but it also limits us further.  I'd
*really* like to let Bones work with arbitrary Lisp objects.  For example, you
could say something like `(fact (username sally "sal"))` and the string there
would Just Work.  You'd also get support for numerics basically for free (though
I might still special-case those a bit).

So the solution I've been rolling around in my head for a while is to split the
store into two separate arrays: an array of types and an array of values.  The
types array would just store small unique integer tags, so it could be packed
pretty tightly (maybe four-bit bytes for each tag).  The values array would just
be a normal Lisp `(vector t)`.  This means each cell would be 64 bits, and you
could store pointers to normal Lisp objects.

This would let us ditch the symbol table entirely.  Now a functor cell would
just have a tag of `FUN` and the value would be a pointer directly to the Lisp
symbol.  We'd still need to handle the arity, but we can just follow every `FUN`
cell with a second cell containing the Lisp fixnum for the arity.

Crucially, SBCL (and CCL, possibly others) will still store fixnums immediately
in the array, so for `REF` and `STR` cells we don't need to suffer an extra
memory deref -- we've still got the index right there in the array's contiguous
hunk of memory.  And we actually don't need to deref even for functors in this
new scheme; the functor values are pointers, but since we just need to compare
them with `eq` and it just compares the pointers themselves.

This also has another possible benefit: we don't need the WAM at (query) compile
time.  Currently when you compile a query you need to have the WAM object
present, so Bones can shove any functors in the query inside its symbol table.
But now we just store the functor symbols directly, so there's no need to have
the WAM available at compile time.

This means that for queries which are completely known at compile time, we can
do the expensive compilation of query-to-WAM-bytecode at compile time instead of
runtime with a compiler macro.  For example: if we have something like `(defun
legal-moves () (query-all (legal ?role ?move)))` we can, at Lisp compile-time,
process that `(legal ?role ?move)` query into a hunk of WAM bytecode and turn it
into: `(defun legal-moves () (query-all #<array of WAM bytecode>))`.  Then at
runtime we just load that into the query area of the code store and go -- no
expensive bytecode compilation needed.

For dynamic queries where we need to build the query at runtime (e.g. ``(defun
legal-moves-for (role) (invoke-query-all `(legal ,role ?move)))``) we can't do
this, unfortunately.

So there are a bunch of benefits to splitting up the store, but of course there
are also drawbacks.  Obviously it will use more memory, but I don't care much
about that.  Popping things off the stack/heap will also become more expensive
because now we need to null out references to Lisp objects when we pop them, so
they can be GC'ed properly.

It also makes another idea I've had slightly more complicated.

#### Prolog on the GPU

A few months back when I was thinking about topics for my upcoming master's
thesis one of the things on my list was seeing if I could get my WAM queries
running on the GPU using OpenGL.  This could potentially speed things up when
you want to know *all* the results of a query and not just the first.

The basic idea would be something like this.

Ahead of time:

* Write an implementation of the WAM bytecode interpreter (not the compiler,
  just the VM part) in GLSL as a vertex (or possible compute?) shader.
* For each predicate, note how many different choices it has (essentially the
  number of `try/retry/trust` instructions).

The idea would be to divide up the and/or tree of Prolog choices into `N`
subtrees, where `N` is the number of GPU cores you've got.  Then each core
searches a portion of the subtree and you merge the results at the end.

At query time:

* Push the WAM code store to the graphics card as a texture.
* Walk the and/or tree of predicates breadth-first to generate `M <= N`
  "traces", each of which is a list of which choice you picked at a given node.
* Push all those different traces to the vertex shader as vertices.
* Each time the vertex shader runs, it gets one trace which essentially tells it
  which direction to take at each choice point it encounters, so it can skip the
  backtracking and just dive head-first down this one path.
* Once it reaches the end of the trace, it just continues normally and starts
  backtracking when necessary.
* Results can get written to a texture framebuffer or something and pulled out
  at the end.
* Merge the results from all the vertices.

This parallel mode would be heavily restricted.  Things like `cut` would cut off
(no pun intended) the trace at that point, forcing full processing by the shader
from that point on.  And of course anything with side effects would just error
out.  But when you're just grinding through unification of basic Prolog terms it
might potentially speed things up (though the latency to/from the graphics card
memory could be a problem).

All this is just an idea I've had for the far future, but I've been thinking
about it because if I split up the WAM store and start treating functors as Lisp
object pointers, that complicates things.  We can easily push integers up to the
graphics card, but if functors are pointers (which can potentially get moved
around by GC) what can we do?

For a while I thought it was unsolvable, but now I think there might be a way.
If we just keep a global "object index" that maps Lisp objects to integers, we
can use those integers as stand-ins for the actual objects when we're on the
GPU.  Of course that would interfere with GC, but there's a solution.  Most
modern implementations support hash tables with weak values, so if we use that
for the index I think it would fix the problem.  We'd be able to map objects to
fixnums without interfering with GC and leaking memory.

### 2016-07-11

* Finished up the [Bones][] code store refactor and a couple of other minor
  things.

* Switched over the Bones main store to be a `simple-array` too.  Another
  performance increase.  I've switched to a new game for benchmarking because
  the previous one was starting to finish too fast for me to be confident in
  getting sane results.  I think that's a good sign.

* Puttered around with a bunch of other little optimizations.  Not *super*
  productive, but I did learn a lot along the way, so I think it was worth it.

* Today's commits took the runtime for the `aipsrovers01` game from about 47
  seconds down to 19 seconds.  Not too bad!

### 2016-07-12

* Watched the "Interpreting Feedback & Maintaining Your Vision" GDC talk.
  I like the idea of not backing down and changing to try to give users exactly
  what they want all the time.

    The last slide in the talk is the best -- a game is a conduit to get some
  idea/experience from your head into the players' heads.  Players give you
  feedback based on what happens in their heads, but they don't know what's
  going on in yours, so you need to interpret their feedback keeping that in
  mind.

* More [Coding Math][].

* Implemented last call optimization in [Bones][].  Not much of a speed
  improvement for the particular GGP games I've been testing with, but it had to
  happen at some point, so we can write actual Prolog without blowing the stack.

* Got a good start on splitting apart the Bones store like I wrote about above.
  It'll probably take another day or two two finish up.

### 2016-07-13

* Spent an hour or so cleaning up my `.vimrc` and plugins, and moving fully to
  [neovim][].

    The catalyst was discovering [miniyank][].  I've been using [YankRing][] for
  years, but it has always been *super* janky.  The way the original YankRing
  works is to rebind all the keys that could possibly result in yanking text,
  like `d`, `c`, `x`, and `y` to a function that handles them.  As you might
  imagine, this can cause problems -- especially with plugins like [Paredit][]
  that need to manage those keys too.  Miniyank hooks into a new neovim event,
  which lets it do what it needs to do without all the hacky workarounds.

* Finished splitting apart the [Bones][] main WAM store into separate type/value
  arrays.

### 2016-07-14

* Watched the "Distributed High Performance Computing in Common Lisp" talk from
  [ELS 2016][] over breakfast.  It would be really fun to try to get a GGP
  player running on an 11k-core supercomputer...

* Got [Bones][] to run on ECL.  I needed to hack [policy-cond][] to do it, but
  I talked to the ECL maintainer in IRC and hopefully I should be able to remove
  the hack in the future.  Performance is pretty bad, but at least it runs!

* Tried out the [PAIP][] tries for [Hype][]'s transposition tables, but they
  don't seem to be much better than a vanilla CL hash table, at least in SBCL.
  Oh well.

* Wrote a real nasty macro to improve the performance of Bones' hot loop.

* Remapped a couple of more keys on my keyboard and I feel like I'm going
  insane, but I think it'll be worth it in the long run.

### 2016-07-15

* [Got nerd sniped](https://www.reddit.com/r/lisp/comments/4si6qm/go_forth/d5d827u?context=1) by /r/lisp.

* Tried to work on more [Coding Math][] but *something* I did yesterday with
  Roswell completely fucked my CCL/Sketch situation.  First SDL2 wouldn't build
  at all.  Then it built, but the key input, title bar, and cmd-tabbing are all
  broken when running from the command line.  ClozureCL.app works, until I do
  something that throws an exception, then it just hangs forever and can't be
  cmd-tabbed back to.

    I don't know why I keep trying to ever update anything on my computer.
  Everything always breaks all the time because programming, especially
  graphics/GUI programming, is a dumpster fire.  I should just never update
  anything ever.  A fucking lab mouse would have learned by now.

* Added support for arbitrary Lisp objects in the [Bones][] heap, and hooked it
  up for numbers for now.  This is the first real Lisp/Prolog interop I've got,
  which is pretty cool.  It also means I can excise the stupid number-munging
  code from [Hype][].

* Refactored the Bones compiler to use structs in a few places instead of CLOS
  classes to reduce consing a bit.  Also fixed a couple of other hot points and
  split apart the horrifically large `compiler.lisp` file.

* Removed the functor table from the WAM.  This is the first step toward making
  Bones GC-friendly.

* Finished the Bones store split by splitting apart functor cells into functor
  and arity cell pairs.  Now that I know this is going to work I'm excited for
  what I can do with Prolog/Lisp interop in the future.

### 2016-07-16

* Started wrapping my head around the WAM's clause indexing.  I think I mostly
  understand the idea -- I'll need to let it roll around a bit before I try to
  implement it though.

* Went through and removed `defstar` from [Bones][] entirely because apparently
  the fucking thing is GPL'ed.  This is why we can't have nice things.

* Made a tiny little ncurses demo with [cl-charms][] in my [sandbox][].  I'm
  thinking about porting [Silt][] to Common Lisp for the [August 2016 Lisp Game
  Jam](https://itch.io/jam/august-2016-lisp-game-jam), so I figured I should
  make sure things actually work before the jam starts.

    I was pleasantly surprised to see that cl-charms just worked right out of the
  box, even inside neovim's terminal emulator.

* Ported a few of my solutions to [99 Prolog Problems][] from Prolog over to
  Bones as unit tests.  I found one bug in Bones itself from them, and I expect
  they'll be good to have as test cases in the future.

* Fought with Roswell a bit to get it to rebuild my lispindent script.  The
  problem was that I has installed ECL under Roswell to test Bones with, and
  this had switched the default Lisp implementation for Roswell to ECL, which
  made it shit the bed when trying to `ros build`.  The solution was to `ros
  use` SBCL again.

### 2016-07-17

* Wrote a compiler macro in Bones to precompile static queries to WAM bytecode
  at compile time, allowing us to run them by simply loading the code store with
  the contents of the precompiled array and firing off the main loop.  This is
  a lot faster, and ends up saving a lot of consing too.

* Did a bit more in the [ANCG][] book.  Tried to use gnuplot to plot the
  data for a spectral RNG test and it was behaving poorly.

    The plot would open up under iTerm2, not have a Mac title bar or entry in
  the command-tab switcher, etc.  For my future self who's run into this shit
  again: the problem is that you're launching it from a tmux process that's been
  detached through a logout.  You need to kill the entire tmux process (not just
  the session, **all** the sessions) and restart it.  This is also what was
  fucking up sketch for me the other day.  Computers are garbage.

* Another episode of [Coding Math][].

### 2016-07-18 - 2016-07-21

* Planning and traveling in the Westfjords.

### 2016-07-22

* Started plugging [Hype][] into [cl-ggp][] to see if I can make this whole
  circus run.  It kind of does.  I worked out a couple bugs in cl-ggp, and one
  of the games uncovered a bug in [Bones][] that I should fix.
* Fixed the bug in Bones.
* Now that I've fixed the bug in Bones my little stupid Common Lisp random-move
  player can play games (and lose) against the Clojure player using GGP-Base
  that my partner and I made last semester.  The yak has been shaved!
* My copy of [The Art of Prolog][taop] finally made it through the mail system,
  so I started reading that.
* I also borrowed the copy of [General Game Playing][ggp-book] that was sitting
  around in the CADIA lab and started skimming over that.  Most of it is the
  stuff we covered in class, I just want to fill in any gaps in my knowledge.

### 2016-07-23

* Another episode of [Coding Math][].  I'm nearing the end!
* Read more of the [GGP Book][ggp-book].  I should implement some of these
  simple players (again) in [Hype][] as an exercise.
* Started adding examples/exercises from [The Art of Prolog][taop] to [Bones][]
  as unit tests.  I get more practice and Bones gets more test coverage.  We're
  [getting two birds stoned at
  once](https://www.youtube.com/watch?v=pXEm08dsQOc).
* More [WebGL Fundamentals][].
* Another section of [ANCG][].  It's slow going, but mostly because I'm trying
  to do other things along the way.  For example, I wrote a `frequencies`
  function that does the same as Clojure's `frequencies` so I could test my
  results, and to do that I wrote a little [iterate][] driver too.  Lots of
  naked yaks.
* Fixed a bunch of shit in [Ooze][] that has been bugging me for a while.  Also
  started to thing about its successor.

### 2016-07-24

* More [Coding Math][].
* More [Bones][] tests from [TAOP][].
* Started cleaning up my vector math stuff from Coding Math.  Might make it into
  its own little library so I can use it in other things.

### 2016-07-25 - 2016-07-31

* Traveling around Iceland with a friend who was visiting.
* Read [Hillbilly Elegy][] after reading [this interview][Hillbilly Elegy
  Interview].  It was a really interesting book.  You should read it if you want
  to understand how what's happening in the US could possibly be happening.
  Luckily the book doesn't strike **too** close to home for me, but growing up
  in rural Pennsylvania I definitely saw bits and pieces of what he describes.
* Read the [Lisp Hackers][] book.
* Finished reading [Engines of Logic][].  It was interesting, but kind of
  a weird mix.  I expected a basic pop science book about the history of logic
  and computing, and for the most part that's what it was, but it was written by
  a mathematician and has some really strangely-explained examples of particular
  mathematical concepts that were really hard to follow.  For example: I already
  understood Cantor's [diagonalization][] argument before reading the book, but
  I still found it hard to follow the author's explanation of it.  The author
  seems to be trying to "dumb down" the explanations but does it in a way that
  makes it harder to grasp overall.

## August 2016

### 2016-08-01

* Did an initial skeleton commit for the [August 2016 Lisp Game
  Jam][lispjamaugust16].  Going to really dive in tomorrow though.

### 2016-08-02

* Started sketching out some basic structure on [Silt2][] for the
  [jam][lispjamaugust16].  I think I'm going to try using a state machine as the
  main game loop and see how it goes.

### 2016-08-03

### 2016-08-04

* Started working on [Silt2][] for real.  Spent some time figuring out how to
  make Diamond-Square terrain tile/wrap properly.  It's not as simple as people
  make it out to be, but I think I've got it working nicely now.  Gonna have to
  remember to write a little blog post about that.
* Set up my build process so I can deploy Silt2 as I work on it.  You can
  `telnet silt.stevelosh.com` to play what I've got so far.  It's not much
  though -- really just the basic terrain/height generation for now.  But it's
  a start.
* Played around a bit with [cl-ecs][] but quickly ran into a use case it doesn't
  really cover.  In true Lisp fashion I decided to roll my own entity/component
  system and got something hacked together enough to work for now.

### 2016-08-05

* More work on [Silt2][].  Revamped the entity component system a bit to make it
  a lot more performant.  Happy with the progress so far.
* Finally got around to consolidating all my `utils.lisp` files in various
  projects into [my own personal utility library][cl-losh], because the world
  definitely needs another one of those.

### 2016-08-06

* Played a bunch more [DCSS][].  I'm addicted.  This does not bode well for my
  productivity.
* Worked on [Silt2][] more.  Added rotting fruit, creatures, eating, inspection,
  random names, and a bunch more.  It's starting to come together.  Four more
  days left for the jam.
* Fixed the UTF-8 issues with the Silt telnet server.  I just had to force
  `export LANG=en_US.UTF-8` before running the Lisp binary in the telnet script.
* Fixed another funny bug on the Silt server.  Building the Silt binary with
  [Roswell][] means that when it runs `save-lisp-and-die` it saves
  *everything*, including the initial seed for the random number generator.  So
  every time you telneted to the server you'd get the same initial world
  generated.  I fixed that by reseeding before each world gen.

### 2016-08-07

* More [Silt2][] and [DCSS][], again.

### 2016-08-08

* Pretty much wrapping up [Silt2][].  Just need to balance it a bit and write up
  a little blog post and call it done.
* Split out the entity/aspect/system stuff from Silt into its own library called
  [beast][] ("Basic Entity/Aspect/System Toolkit").

### 2016-08-09

* Almost done with [Silt2][].  Might add a few more artifacts tomorrow but
  otherwise it's done.  Time to move on.

### 2016-08-10

* Added a [Links page](http://stevelosh.com/links/) to my website.  I've been
  meaning to do this for a while.  It's going to be a place for me to dump links
  to blogs/etc that I want to remember to check every now and then.
* Fixed the system redefinition clobbering bug in [beast][].

### 2016-08-11

* Submitted [Silt2][] to the game jam.  It's as done as it's ever gonna get.
  I'm pretty happy with how it turned out.
* Wrote up some docs for [beast][].  Gonna officially release it in the next
  couple of days.

### 2016-08-12

* Wrote up a postmortem blog post for the Lisp game jam.  Gonna post it on
  Monday.

### 2016-08-13

* Finally getting back to [Coding Math][].  Sadly I'm almost done with the
  entire series.
* Wrote up some real nasty `iterate` drivers to make looping over nested things
  easier.

### 2016-08-14

* Did the first two kinematics episodes of [Coding Math][].  Fun!
* Wrote a couple of horrifying macros in my utility library. 
* Ascended in [DCSS][] for the first time!

### 2016-08-15

* Posted my [Lisp Game Jam Postmortem](http://stevelosh.com/blog/2016/08/lisp-jam-postmortem/).
* Wrote another blog post about a particular Lisp macro.  Gonna let it stew for
  a couple of days before posting it.
* More [Coding Math][].

### 2016-08-16

* Spent a chunk of time at school finding and printing off General Game Playing
  research papers to look into.  Also downloaded some [IRDC talks][] and the
  [New England Lisp Games Conference talks][] to watch over the next week or
  two.
* More [Coding Math][].
* Built some
  [docs](https://github.com/sjl/cl-losh/blob/master/DOCUMENTATION.markdown) for
  [my utility library][cl-losh].
* Watched the Markov by Candlelight talk from IRDC and stayed up too late making
  a really simple Markov chain generator.

### 2016-08-17

* First day of school!  But it's not really too different for me because I'm not
  taking classes, jut going to be working on my thesis for the next two
  semesters.
* Made a hilarious Markov chain mashup bot.

### 2016-08-18

* Watched the IRDC talk about Dijkstra Maps and spent way too much time playing
  around with them.
* More [Coding Math][].
* Finished the [GGP Book][ggp-book].  It was pretty mediocre.
