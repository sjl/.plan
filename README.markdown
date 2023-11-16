This is my personal notebook where I dump thoughts and notes for my future self.

**I make no guarantees about the accuracy of anything in here.  Read at your own
risk!**

[TOC]

# November 2023

## 2023-11-01

HG545 discussion section.

Made a little tornado plots demo with `p5.js` to be able to poke around and
confirm a couple of things:

* When you have two pause sites symmetric about an origin, there is *no* shift,
  but the coverage massively changes there.
* If you decrease the rate of both forks, you don't get a long skinny tornado,
  you get a shorter normal-looking one with higher coverage.

SAA Wednesday dance.

Got nerd sniped by Kate into adding calculation of the read counts to the
tornado plots instead of just abstracting that as a parameter itself and jesus,
that was a rabbit hole I didn't expect.  Most of it was easy — the dependence on
cell population and synthesis time was trivial, and undercutting was simple to
kludge in.

The problem was the last parameter in the equation: the firing rate of origins.
How do you even define this?  I came up with two options:

* Half-life based exponential firing, e.g. "after 5 seconds, the origin will
  have fired in half the cells".
* Per-cell linear rates, e.g. "this origin has a 5% chance of firing every
  second".

Looking at the results, I'm now more confused than ever — I'm not even sure the
second model is actually different from the first when applied to a population
of origins that can only fire once.

As I was implementing this, I initially started with proportion-based
computations, e.g. for a given timestep, how many of the remaining origins
fired?  But this immediately causes issues in the data if the timesteps are big:
in reality no two origins *ever* fire simultaneously, so this method produces
bands that wouldn't be there in reality when the timesteps are large.

So the obvious solution is to just shrink the timesteps, and that does help at
first, but it begins to break down in another way when the steps shrink small
enough. It helps to think about what the ideal timestep size should be: small
enough most individual firings are in separate timesteps instead of simultaneous
ones.  But when the time is small enough for this to happen at the beginning
(when firing is high), that means that later in the process you end up computing
things like "0.01 cells should fire" in a given step.  But you have to choose
some rounding method to turn that into an integer number of firings, and all of
them will fuck you:

* `round` and `floor` will always result in `0`, so your remaining population
  will never ever fire.
* `ceiling` will always fire at least one cell, which results in wildly-too-high
  rates near the end.

So eventually I realized this and did the ugly thing that should actually work:
turned the proportion into a probability and checked `random() < p` for every
remaining cell to actually simulate the individual firings instead of
abstracting them across the population.  This is noticeably slower in
pathological cases, but still not too bad most of the time, and is much more
realistic.

## 2023-11-02

BS521 exam.  Got a little tripped up on the paired t test question until
I realized that `(average (mapcar #'- as bs))` is algebraically equivalent
to `(- (average as) (average bs))`.

Met with advisor about classes to take next semester.  Need to register when
that becomes available in a few days.  Basic plan is to take:

* BIOSTAT-522: continues stats progression and completes that requirement.
* BIOINF-529: required for all bioinformatics people, cannot ever be waived, may
  as well get it out of the way now.
* BIOINF-602: journal club part 1 (no presenting).
* PIBS-800: continues.
* PIBS-504: round 2 of the ethics classes.

I can consider adding one more class to the mix if those feel too light
(compared to HG545 they'll probably both be easier).  Might pick from one of:

* BIOINF-545: classical bioinformatics, done in R.
* EECS-551/553: machine learning, probably really hard to get into.
* BIOINF-597: AI class, I lack the prereqs now but might be able to convince
  them to let me in because I'm a CS person.  Or just wait until I take
  BIOINF-580 in the fall and do this next winter.
* CANCBIO-554: would be good for Prensner lab, possibly also for a training
  grant.

## 2023-11-03

HG545 review session.  Didn't manage to get in at 8 AM so I'll have to watch
the recording some time this weekend.

Finally got around to adding the bash version of Z to my remote dotfiles so
I don't lose my mind trying to work on servers/VMs.

Also finally got around to properly mapping the numpad keys and rotary encoder
on my Sinc with StumpWM:

    ("KP_End"       "gselect 1")
    ("KP_Down"      "gselect 2")
    ("KP_Page_Down" "gselect 3")
    ("KP_Left"      "gselect 4")
    ("KP_Begin"     "gselect 5")
    ("KP_Right"     "gselect 6")
    ("KP_Home"      "gselect 7")
    ("KP_Up"        "gselect 8")
    ("KP_Page_Up"   "gselect 9")

    ("H-F1" "mute")
    ("H-F2" "volume-down")
    ("H-F3" "volume-up")
    ("XF86AudioMute" "exec mute")
    ("XF86AudioRaiseVolume" "volume-down") ; todo unfuck the backwards mapping in qmk
    ("XF86AudioLowerVolume" "volume-up")

Also realized that I've mapped the raise/lower to the opposite directions on the
encoder in QMK, welp.  Should fix that at some point…

Did a bit of dotfile cleanup.  Realized I can also sync `htoprc` which is nice.
Also discovered `htop` has an option for highlighting new processes and
recently-killed ones, which will be *really* handy.

## 2023-11-04

Poking around at getting my Pine64 working again.  Dug out what I think is power
suppy (5V 3A), and it seems to work, so that's good.  Booted it with the tiny
screen and one of my old UHK's, but couldn't remember the password I had set
(and apparently I never bothered saving it in my password manager, which is
bizarre for me).  Oh well, probably a good idea to do a fresh install of Armbian
on it anyway.  Attempted this and no matter what I try, the board just doesn't
ever boot.  Tried multiple different SD cards, no luck.  Linux is such a goddamn
mess some times.

Eventually I realized that I was trying to use the Pine64 images from Armbian
because the page is titled "Pine64 and LTS" and I have a Pine A64-LTS.  But
apparently the A64-LTS needs to use the SOPINE images, even though I don't have
a SOPINE.  Christ, what a mess. Got SSH set up, dotfiles synced easily.

Starting to look at the GPIO stuff now.  Useful links:

* <https://web.archive.org/web/20230501084346/https://synfare.com/599N105E/hwdocs/pine64/index.html>
* <https://files.pine64.org/doc/Pine%20A64%20Schematic/Pine%20A64%20Pin%20Assignment%20160119.pdf>
* <https://www.ics.com/blog/gpio-programming-using-sysfs-interface>

HelLEDo, world:

    echo 77 >/sys/class/gpio/export
    cd /sys/class/gpio77
    echo 1 > direction
    echo 1 > value
    echo 0 > value
    echo 77 >/sys/class/gpio/unexport

    (defparameter *f*
      (open "/sys/class/gpio/gpio77/value" :direction :output :if-exists :supersede))
    (write-char #\0 *f*)
    #\0
    (force-output *f*)

Neat.  Dug around and tried to figure out how to use hardware PWM, but the
documentation is… a mess, so I janked together PWM in software instead.  That…
kind of worked.  I (much) later realized the site that gave me the duty cycle
timings lied to me (it said 1ms-2ms when it's really much closer to 0.5ms-2.5ms
according the manufacturer).  But even so, it's still really janky to try to
software PWM from an SBC, so everyone seems to recommend breaking out an Arduino
to make *that* control the servos, and then have the SBC drive that.  Poked
around a bunch more and eventually got that working too.

Next step is to get a web server running, which wasn't too hard with
Hunchentoot.  Looked at various routing libraries and went with `easy-routes`
for now.  Seems okay, though there are a few parts I don't love.  But it's good
enough for now.  And with that I can `curl` and move the arm.  Neat.

## 2023-11-05

HG545 review session.

Continued poking around at the Arduino stuff.

## 2023-11-06

HG545 test and literally nothing else.

## 2023-11-07

BS521.  Finished up Χ² testing.

BI500.  Talked about visualization and Adobe Illustrator.

PIBS800.  "House" meeting, talked about various stuff.

Figured out how to jank together SSH tunneling between my server and my Pine SBC
to expose a server running on the Pine to the internet.  Basically need to do
two legs of SSH tunneling for this:

    ssh -NTR '*:12345:localhost:8888' sl
    ssh -NTL    '8888:localhost:80'   pine

The first line makes anything connecting to port `12345` on the remote machine
actually connect to what my intermediate machines sees as `localhost:8888`.
Unfortunately that `localhost` hostname is indeed a hostname, and I can't use an
SSH server name there to automagically jump around that way.  So anything
hitting `12345` on the server will now hit `8888` on my intermediate machine.
Then we use the second tunnel to forward *that* to whatever `pine` thinks
`localhost:80` is.  Also note you need to enable `GatewayPorts` on the remote
server and restart `sshd` for this to ever work at all.

Read a bit for 503.  Need to do a bunch more.

Backpacked classes for next semester.  Can't register yet, but I think that's
because registration doesn't open until Nov 13?

## 2023-11-08

HG545 this morning, about recombination.

BS521 homework.  Finally figured out how to get rid of the stupid
`\begin{description}` hanging indent:

    \usepackage{enumitem}
    \setlist{leftmargin=!,labelwidth=2em}

and how to tell LaTeX where to put page breaks:

    \pagebreak[1] % Meh.
    \pagebreak[2] % This would be a reasonable place to break.
    \pagebreak[3] % Prefer to page break here unless it seems ridiculous not to.
    \pagebreak[4] % Page break here, dammit.

Played around with some of the recombination stuff.  I think I finally
understand the junction resolution.  The key was that when you cut "vertically"
at a Holliday junction you cut the *outside* strands, *not* the inside ones.
Once I drew that out, it's obvious how you can unwind it.

Reading for 503 discussion thing tomorrow.

Reading for BS521 tomorrow, linear regression p-values.

Started reading the HG545 paper but feeling a bit overwhelmed by it.  Will try
again tomorrow (need to print it out tomorrow afternoon too, reading on a laptop
sucks).

## 2023-11-09

Looked into 3D printing and there's actually [a
lab](https://www.lib.umich.edu/visit-and-study/creation-and-learning-spaces/shapiro-design-lab/workshop)
here with that and a lot more.

Looked into why my enter and backspace keys on my laptop seem to intermittently
stop working.  Turns out it's a common issue with this model of T14s.  Ugh.  The
laptop is ~4 years old so I guess I could potentially justify getting a new one,
but I'd really rather not.  80% of the time I'm using this with an external
keyboard anyway, so maybe I'll just jank together some shortcuts in case this
happens during a presentation or something.  If a computer could ever Just Work
for me I'd be so happy.

BS521 about linear regression.  The clock is broken in the classroom now.

Poked around a little at Parenscript.  Need to figure out a way to get it
working standalone which is *not* clear at all from the documentation, but
I managed to find <https://app.leby.org/post/fun-with-parenscript/> that gave me
somewhere to start.

Yet another ethics/rigor meeting.

Wired up `super-m` and `super-del` to deal with the Thinkpad keyboard crap.

## 2023-11-10

HG545.  A little worried, this section feels super rushed and I still feel very
lost looking at the paper.

## 2023-11-11

Finally managed to get through the HG545 paper.  Still don't grok it in
fullness, but at least I'm not totally bewildered.

## 2023-11-12

HG545 homework.  This was *rough*.

## 2023-11-13

HG545 discussion.  At least it's good to know everyone had a rough time with
this one.

The dying Thinkpad keys are really getting on my nerves.  Might be time to get
a new Thinkpad so I've got two laptops in case one dies.  Looked at Lenovo's
site but they just released Gen 4 of the AMD T14's, and I think I'd rather get
one generation back so that Debian supports it.  Looks like I'll need to buy
refurbished if I want that, unfortunately, but it might end up saving me some
money anyway.

Yet Another PIBS 503 research/responsibility/ethics meeting, this time on
conflicts of interest.

Looked into the new laptop thing a bit more.  Tried to find some Gen 3 AMD T14's
but there's not any available from Lenovo themselves, only eBay.  Eventually
I realized the P14s is essentially a T14 with a few tiny changes, and Lenovo
*did* have a Gen 3 one of those available on a clearance, so I just went ahead
and grabbed it.  Not looking forward to porting everything over again, but it'll
be a good exercise I guess.

Reviewed materials for Yet *Another* R/R/E meeting tomorrow.

## 2023-11-14

The dead keys are getting *really* annoying.  Glad I ordered the P14s.  Maybe
I'll turn this into a little home assistant server or something.  Could be fun.

Got an email this morning that the R/R/E meeting is rescheduled for Friday.
Welp.  Good to know they can just change them out from under you, I guess.

BS521.

Chatted with another PI about my third rotation.  Going to chat with some of
their grad students later this week.

PIBS800.

Finished the 3D printing course on the library site so I can potentially use the
3D printers there now.  Still need to learn how to make stuff in e.g. TinkerCAD
first I think.

Read the review papers for HG545 tomorrow to prime my brain.  I'm still
expecting it to be a lot to take in.

Started the TinkerCAD tutorials.  Seems simple enough so far.

## 2023-11-15

HG545, start of the Epigenetics module.

Registered for classes.  Mostly went smoothly except for two:

* Needed to swap out the BS521 lab for a lab session on Mondays.  Given that
  I haven't been really using the lab sessions much at all, this is fine.
* Need instructor permission for BIOINF-545, and also apparently it's Tuesday
  and *Friday*?  Strange set of days.  So much for my free Fridays.  Oh well, at
  least Thursdays will be less wild I guess.

Went to a talk by a professor I chatted with during Matchathon about Denisovans
and population genetics.

## 2023-11-16

Unfortunately had to miss the BS521 class today to sign for my laptop so it
wouldn't get returned.  I hope they recorded it.  I guess I know what I'm
spending the weekend on: setting up another goddamn computer.  Ugh.

Finish BS521 lab 3.

Downloading a Debian installation image while I have fast internet so I can
install that this weekend.  Cleaned up my downloads folder with the janky-ass
file manager I installed to avoid having to install all of Gnome, but it… kind
of sucks.  I wonder if it's worth poking around at making my own with McCLIM.
Probably not, given how flaky McCLIM seems and how painful working with files in
in CL.

ieure helped me track down the replacement part I'd want to get for my broken
Thinkpad keyboard: `5M10Z41656`.  Not sure whether I want to spend $200 on
fixing the keyboard, but at least it's an option if I decide I want to.
