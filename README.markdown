[TOC]

# January 2019

Happy new year!

## 2019-01-01

Started poking around at Fern again.  Need lots more thinking on this.  Slow and
steady wins the race.

## 2019-01-02

Had trouble booting my Ubuntu partition, it took forever and tossed me at a root
prompt with "You are in Emergency Mode".  Turns out the line I added to
`/etc/fstab` broke things when the external drive isn't plugged in.  Need to
figure out how to fix that.

## 2019-01-04

Did a good chunk of work on Fern.  Finally got all the official opcodes written
out after rewriting the addressing mode stuff three or four times.

## 2019-01-05

More work on Fern.  Got all of `nestest.nes` passing after lots of run, diff,
fix cycles.  On to pictures and sound!

## 2019-01-06

More work on Fern.  Did a lot of restructuring and didn't make much actual
progress, but I think it was helpful for wrapping my brain around stuff.

## 2019-01-07

Someone wanted me to take a look at getting my coding math repo running again.
It's bitrotted.  Need to install SDL first:

    sudo apt install libsdl2-dev libsdl2-ttf-dev libsdl2-image-dev libffi-dev

Pushed a commit to fix the most obvious brokenness, but something inside SDL
makes CCL shit itself and drop you into the kernel debugger and I just can't be
bothered to figure out the shitshow that is graphics programming.  Sorry.  Best
to look at my `coding-math` repo as a historical curiosity.

Did some research and thinking about the GUI for Fern.  Refreshed my memory on
all the inscrutable fucking acronyms:

* OpenGL: take triangles and textures and shaders, render pixels.
* GLU: utilities for OpenGL, probably outdated and not needed any more.
* GLUT: handles the OS-specific stuff about getting a window to draw into, getting keystrokes, etc.
* GLFW: competitor to GLUT that does the same things?
* SDL: competitor to GLUT/GLU that does the same things, plus other things like sound, networking, etc.
* GLEW: completely unrelated, handles OpenGL extensions (GL Extension Wrangler).

Looked into immediate mode GUI libs like IMGUI and Nuklear.  They're especially
weird in that you have to provide your own rendering backend and input support.
So you'd use them *in addition* to GLFW+OpenGL, for example, and you need to
wire up all the support yourself.

These might be good eventually but I think I can probably just get away with
GLFW for now, since I just want to display some god damn pixels in a window.
I can do sound with PortAudio like I did for `cl-chip8`.  That'll be a fun
learning experience and should work just fine for the NES.

## 2019-01-08

Started really wrapping my head around pattern tables for Fern.  Wrote some
janky code to render them as strings for now.

Started poking around with `cl-glfw3` and `cl-opengl`.  OpenGL is as much of an
inscrutable shitshow as I remember, though I have a little bit of a head start
in understanding it this time around.  Hopefully it won't take me too long to
remember everything.  I did manage to get the example running smoothly, so
that's nice.

Started going through <http://learnopengl.com> to try to remember how to do this
crap.  Spent lots of time fighting with object lifetimes because the examples
all just garbage collect with `exit()`.

## 2019-01-09

Started booking travel for the upcoming year.

Got my copy of [Programming the 65816](https://amzn.to/2RH8or0).  Gonna skim
through it for all the 6502-specific bits to hopefully fill in the gaps in my
brain for Fern.

## 2019-01-10

Finally got around to replacing `mkpass` with a version in Common Lisp.  My
collection of CL scripts is growing, now that I have Adopt to make writing their
UI less painful.  Need to dogfood it a bit more and eventually release it.

Did a bit more of the OpenGL tutorial.

## 2019-01-12

Did some more of the OpenGL tutorial.  Added some extra bits to cl-netpbm to
easily load an image into an array in the form OpenGL expects.  Started
sketching out the GUI structure in Fern.

## 2019-01-19

Got pattern tables rendering in Fern (finally).

## 2019-01-22

Got a first pass at the main GUI loop for Fern hashed out.  GUI programming is
fucking miserable.

## 2019-01-24

The saga of my keyboard disconnects continues.  Captured a `dmesg` log of it
happening:

    [88916.149078] usb 1-2.1-port1: disabled by hub (EMI?), re-enabling...
    [88916.152083] usb 1-2.1.1: USB disconnect, device number 29
    [88916.638190] usb 1-2.1.1: new full-speed USB device number 33 using xhci_hcd
    [88916.958196] usb 1-2.1.1: New USB device found, idVendor=1d50, idProduct=6122
    [88916.958199] usb 1-2.1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=0
    [88916.958200] usb 1-2.1.1: Product: Ultimate Hacking Keyboard
    [88916.958202] usb 1-2.1.1: Manufacturer: Ultimate Gadget Laboratories
    [88916.979576] hid-generic 0003:1D50:6122.002A: hiddev1,hidraw2: USB HID v1.10 Device [Ultimate Gadget Laboratories Ultimate Hacking Keyboard] on usb-0000:01:00.0-2.1.1/input0
    [88916.989417] input: Ultimate Gadget Laboratories Ultimate Hacking Keyboard as /devices/pci0000:00/0000:00:01.1/0000:01:00.0/usb1/1-2/1-2.1/1-2.1.1/1-2.1.1:1.1/0003:1D50:6122.002B/input/input45
    [88917.046540] hid-generic 0003:1D50:6122.002B: input,hidraw3: USB HID v1.10 Keyboard [Ultimate Gadget Laboratories Ultimate Hacking Keyboard] on usb-0000:01:00.0-2.1.1/input1
    [88917.056500] input: Ultimate Gadget Laboratories Ultimate Hacking Keyboard as /devices/pci0000:00/0000:00:01.1/0000:01:00.0/usb1/1-2/1-2.1/1-2.1.1/1-2.1.1:1.2/0003:1D50:6122.002C/input/input46
    [88917.114459] hid-generic 0003:1D50:6122.002C: input,hidraw4: USB HID v1.10 Device [Ultimate Gadget Laboratories Ultimate Hacking Keyboard] on usb-0000:01:00.0-2.1.1/input2
    [88917.124334] input: Ultimate Gadget Laboratories Ultimate Hacking Keyboard as /devices/pci0000:00/0000:00:01.1/0000:01:00.0/usb1/1-2/1-2.1/1-2.1.1/1-2.1.1:1.3/0003:1D50:6122.002D/input/input47
    [88917.182306] hid-generic 0003:1D50:6122.002D: input,hidraw5: USB HID v1.10 Device [Ultimate Gadget Laboratories Ultimate Hacking Keyboard] on usb-0000:01:00.0-2.1.1/input3
    [88917.194570] input: Ultimate Gadget Laboratories Ultimate Hacking Keyboard as /devices/pci0000:00/0000:00:01.1/0000:01:00.0/usb1/1-2/1-2.1/1-2.1.1/1-2.1.1:1.4/0003:1D50:6122.002E/input/input48
    [88917.194696] hid-generic 0003:1D50:6122.002E: input,hidraw7: USB HID v1.10 Mouse [Ultimate Gadget Laboratories Ultimate Hacking Keyboard] on usb-0000:01:00.0-2.1.1/input4
    [88917.258912] usb 1-2.1.2: reset full-speed USB device number 31 using xhci_hcd

Observations:

* It's only the keyboard disconnecting.  The mouse is also plugged into the same
  USB hub, and that doesn't seem to get disconnected (the "mouse" in that log
  output is the virtual one the UHK uses to do mouse stuff).
* I'm pretty sure this happens regardless of what USB port it's plugged into.
  I'm going to try plugging it into a different port on the hub, and if that
  fails, into the monitor hub, and maybe into the work laptop itself.
* My Realforce did the same thing, so it can't be specific to the keyboard.

What the fuck, man.

Added a skeleton of a nametable viewer to Fern.  The windowing works, but I've
hit a problem I'm not sure exactly how to solve.

For some reason, I thought it was the `poll-events` call that blocked til vsync.
That was incorrect — it's the `swap-buffers` that waits.  This exposes two
problems in my current design:

1. When we don't have to draw anything, we never call `swap-buffers`, and so
   never have a chance to block, and so busy loop and consume an entire CPU
   core.
2. If we have multiple windows open that all want to draw on the same frame,
   they'll vsync one after another and end up cutting our FPS down.

I could potentially solve 1 with something like "if you didn't draw anything,
sleep for 10ms" or something, but that doesn't fix problem 2, which is more of
an issue.

Problem 2 is trickier.  I searched around a little bit online and found a couple
of things I might want to try.

1. Disabling vsync and managing it myself with sleeps.  Folks warn that this
   could produce tearing, so it doesn't seem ideal.
2. Track which windows need to swap.  Enable vsync for the first and swap,
   disable it for the rest and swap them.  Sleep if nothing needs to swap.  This
   seems reasonable, though some folks said it might still produce tearing?
3. Run each window in its own thread, and vsync.  Does this work on MacOS?  Do
   I care?

Need to sleep on this.

## 2019-01-27

Took another two stabs at the Fern multiple windows things.  I basically ended
up going with option 2.  It seems to work.  Still need to do some actual work
on the nametable viewer, but at least it doesn't eat my CPU and/or take way too
long to do anything now.

# February 2019

Spent the first two weeks in SF for work.

## 2019-02-18

Back from SF.  Registered for ELS 2019.  Don't have anything to talk about this
time, but it'll be good to see folks again.

## 2019-02-22

Did some more Rosalind problems.  I'm up to 33 or so now.  These were fairly
straightforward, but there are some other trickier ones I need to think about
more.

## 2019-02-23

Did another Rosalind problem.  Spent some time dicking around with `format` to
try to figure out how to do the equivalent of the following:

    (format nil "~{~,VF~^ ~}" precision floats)

The intent is to print all the floats with the given precision.  This doesn't
work, because the `V` is inside the `~{~}` directive, and so `format` expects
two list items per iteration.  Options:

1. Generate a control string at runtime with a separate `format` (gross).
2. Define `print-float` to be a formatting function that uses a dynamic variable
   and use`~/print-float/` in the control string (awkward).
3. Interleave the precision in the list (wasteful).
4. Do something horrible.

I went with option 4:

    (defun float-string (float-or-floats &optional (precision 3))
      (with-output-to-string (s)
        (loop :for (float . more) :on (ensure-list float-or-floats)
              :do (format s "~,VF~:[~; ~]" precision float more))))

Finally wrote some documentation for
[cl-netpbm](https://sjl.bitbucket.io/cl-netpbm/) and sent a request to get it
into Quicklisp.  The project backlog continues to shrink.

Started reading the Bioinformatics Algorithms book.  Set up a new repo for it.
Did the first problem just to make sure all the pieces are hooked up.  The first
problem is trivial to do serially.  Dicked around with lparallel to exercise my
fancy machine a bit.  Learned a few things:

* You can give each lparallel worker thread its own thread-local bindings with
  `:bindings '((*foo* . (form to eval) …))`.  This is nice to give each thread
  its own random number generator so they can work concurrently.
* Generating ~32gb of random DNA is a *lot* faster when you do it on 16 cores
  instead of 1.
* Giving SBCL all of my 64gb of memory is a bad idea.  It will try to use *all*
  of it, and I usually have at least another few GB used, and the Linux OOM
  killer does not fuck around.
* I need a better interface for cl-pcg.  The current one blows.
* SBCL does appear to `free` memory back to the OS when it GCs, unlike the JVM.

Asked #sbcl for clarification on a couple of things:

    <sjl> Are there any thread safety guarantees for writing to separate elements of SIMPLE-ARRAYs?
    <sjl> Example: I want to initialize a large (~30gb) array with random data (DNA bases) for testing purposes.
    <sjl> If I make the array a (SIMPLE-ARRAY CHARACTER (*)) and initialize it using LPARALLEL:PDOTIMES to work in chunks, it appears to work fine, but I assume I can't rely on that behaviour.
    <sjl> I'm guessing if I switched to something more compact like (SIMPLE-ARRAY (INTEGER 0 3) (*)) this would no longer Just Work™.
    <sjl> Would I then need to use the CAS stuff to guarantee that one thread writing to (AREF FOO N) and another writing to (AREF FOO (1+ N)) don't step on each others' toes?
    <pkhuong> sjl: bytes and larger are safe.
    <pkhuong> there is no guarantee
    <pkhuong> except for the fact that it's implemented that way
    <pkhuong> threading is outside the spec. developing a formal memory model is expensive.
    <sjl> Yeah
    <sjl> It seems unlikely that "bytes and larger are safe" would stop being true in the future, right?
    <pkhuong> correct.
    <sjl> I think I can live with that.
    <sjl> Thanks.
    <pkhuong> don't run on itanium. I'd double check the disassembly on ARM.
    <sjl> Ah, not using either at the moment, but good to know.

## 2019-02-24

More Bioinformatics Algorithms problems.

# March 2019

## 2019-03-01

Did the `LONG` Rosalind problem while sitting in ORD.  Not completely happy with
it — I feel like I must be missing something that would make this cleaner.

## 2019-03-08

Did some more BIAL problems.  Spent way too much time writing iterate drivers to
make the problems themselves look clean.  Oh well, I'll use them again some day.

## 2019-03-09

Browsed through `st`'s code a little bit.  Seems fairly simple (at least as
simple as a language as weak as C can be).

More BIAL problems.  Spent a bunch of time screwing around with iterate and
lparallel for not a lot of benefit.  Oh well.

Finished The Character of Physical Law by Feynman.  A bunch went over my head,
but it was still a good read.

# April 2019

## 2019-04-12

My [MakerLisp Machine](https://makerlisp.com/) arrived.  Going to put it
together and brain dump along the way.

I had previously downloaded and extracted `makerlisp.zip`, and committed the
result into a Mercurial repo.  Just to be safe I wanted to see if it had been
updated since a couple of days ago.  I downloaded it again, moved it into the
repo, and then `rm -rf src doc RELEASE` and `unzip makerlisp.zip`.  Then an `hg
diff` showed me the changes.  Maybe this process could be made easier (e.g. by
just letting me clone the git repo?) but it's easy enough to script up if
necessary.

Used my new SD card reader to get at the SD card.  It was FAT32 as expected, so
nothing to mess around with there.  Had to first get it mounted, and of course
mounting anything is a giant pain in the ass on Linux.  I miss MacOS.  Ended up
using `udisksctl mount -b /dev/sdc1` to mount the thing without dicking around
with `fstab`.  Then `cp -rt /media/sjl/…mountpoint…/ src/uSDimage/*` to actually
copy the files.  It was pretty fast.  `udisksctl unmount -b /dev/sdc1` to eject.

Installed the battery.

Wiring up the VGA controller and USB keyboard controller.  Almost messed up
— the RX pin goes to PD0 and the C pin goes to PB1.  Note it's D and B, not the
same letter!

VGA cable is quite beefy, not perfect for routing around everything.  But it
does the job.

After connecting everything and plugging it in, it works!  The screen looks
a little odd because there appear to be two prompts.  I wonder if the graphics
mode is wonky.

Had some issues getting the keyboard working:

* The documentation says to make sure the RX jumper isn't connected.  The board
  came this way, so that was fine.
* But the board came with the TX jumper jumped, and I had to *remove* that to
  get the keyboard to work.
* Then I tried to use some other USB keyboards, because the 40% one is just too
  painful to type on.  The Realforce 104 worked fine, but my HHKB and my UHKs
  didn't work at all.  They're getting power (they light up) but typing doesn't
  work at all.

Setting the time and date worked great.  They persist across restarts and such.

After evaluating some stuff, the screen seems to be garbled.  Not sure exactly
what I need to do/configure to get the screen working properly.  Evaluating
`(cls)` does clear the screen back to the beginning, so I can use that for now.

## 2019-04-13

Trying to get my code-to-PDF thing ported to Linux.  Random notes:

No idea where my header file is.  Probably forgot to commit it.

`pstopdf` is called `ps2pdf` on Linux and has different options, because fuck
you.

To list fonts and their files on the system: `fc-list`.

`enscript` on Linux can't just take one of these fonts because fuck you.  It
needs an "AFM" file for some reason.

Can generate an `afm` file with `ttf2afm` which is in the `texlive-binaries`
package along with a whole other pile of bullshit I don't need.  Cool:

    sudo apt install texlive-binaries
    ttf2afm /usr/share/fonts/truetype/ubuntu/UbuntuMono-R.ttf | sudo tee /usr/share/enscript/afm/umr.afm`

Then I need to edit `/usr/share/enscript/afm/font.map` because this program is
incapable of `ls`ing a directory to find all the font maps in it or something.
Note that the font name here needs to match the font name in the generated AFM
even though you're explicitly telling the stupid program which AFM to use with
a given font name, because once again: fuck you.

Found the `sjl.hdr` file on my old machine.  It was just in `/usr/local` because
I was lazy.  Committed it to my dotfiles this time.

I also had a `clisp.st` highlighting file in there.  Need to symlink that into
`/usr/share` too, and also update the `enscript.st` file to add it.

Also need to hack `enscript.st` to tell enscript how to find the proper variants
of my font.  Jesus:

    else if (is_prefix ("UbuntuMono", font))
      {
        bold_font = "UbuntuMono-Bold";
        italic_font = "UbuntuMono-Italic";
        bold_italic_font = "UbuntuMono-BoldItalic";
      }

Now the thing finally fucking runs again.  So now I can get started printing the
MakerLisp code.  However, if I do my usual one-page-per-file style it ends up
being 198 pages, and many of them are almost entirely blank.  So instead I can
cat the various groups of files together with something like:

    cd bin
    ffindext l | sort | xargs -I file sh -c "cat file; echo" > ../bin.l
    cd ../..

    cd l/lang
    ffindext l | sort | xargs -I file sh -c "cat file; echo" > ../lang.l
    cd ../..

    cd l/clib
    ffindext l | sort | xargs -I file sh -c "cat file; echo" > ../clib.l
    cd ../..

    cd l/ez80
    ffindext l | sort | xargs -I file sh -c "cat file; echo" > ../ez80.l
    cd ../..

And then generate the PDF with something like:

    ffindext l | sort | grep -v /lang/ | grep -v /bin/ | grep -v /clib/ | grep -v /ez80/ | xargs code-to-pdf "MakerLisp"

Now we're down to 64 pages, which is much more reasonable.  The `demo` and
`util` directories have some beefier programs, so I'll leave those alone.  And
I *finally* have a PDF I can print.  I hate computers.

Booted up the lisp machine again and today the TX jumper seems to work as
documented.  I tried debugging the display corruption with the info from the
email Luther sent (getting a bunch of text on the screen and pressing the Auto
button) but that didn't seem to help.  Emailed back.

## 2019-04-14

More troubleshooting of the Lisp machine video issues.  Borrowed a miniDP/VGA
dongle and TV with a VGA input (apparently they still exist) from a friend, and
got a new VGA cable.  The results are very confusing:

* Cable makes no different in any scenario.
* WORKS: Macbook miniDP to dongle to Elecrow VGA
* WORKS: Thinkpad miniDP to dongle to Elecrow VGA
* WORKS: Lisp Machine VGA to TV VGA
* BORKED: Lisp Machine VGA to Elecrow VGA

Emailed the author back with my results.  This is really strange… I would have
expected either the monitor or the Lisp Machine were the problem, but they only
seem to not work *together*.

## 2019-04-16

The Makerlisp author received an updated version of the monitor and he's now
seeing the same thing I am, so it's nothing I did wrong.  He's mailing me his
old/good monitor and I'm mailing him my bad new one, which was very kind of him.

Spent a while getting Vim set up to work with a Makerlisp REPL.  Mostly got it
working, except the newline handling is going to be kind of a pain.  But I can
live with that for now, in exchange for being able to edit in Vim with Paredit
and sending to a REPL easily.

## 2019-04-18

More poking around at MakerLisp.

I know I'm going to need user input for a game, so my first idea is to see if
I can make some reading functions.  `read-line` would be good for a text
adventure.  I found an example implementation in the shunting yard demo, but
also tried writing my own.  I wrote a bunch of other stuff along the way too.
Did `read-byte` and `read-char`.  Not sure how to go about making the `-no-hang`
variants.

Is there something like CL's `macroexpand-1` that will only do one level of
macroexpansion?  It's a bit hard to read when *everything* gets expanded…

Symbols don't seem to be printed readably.

Spent 15+ minutes wondering why my `defmacro` macro would go into an infinite
loop on the second and further tries.  Realized it's because I was using the
file as a scratch space, and so when it would `forget` itself and autoload it
would be evaling the `expand` call over and over.  I'm so dumb.

`cadr` is a macro, so I can't map it (or, rather, I can with *very* strange
results).

`print` and friends don't return their argument, which means you can't just wrap
a `(print …)` around something when debugging.

## 2019-04-19

New screen arrived today.  It works!  Then I needed to sync the SD card again.
Commands to do that (eventually I'll script these):

    udisksctl mount -b /dev/sdc1
    rsync -avd ./ --copy-unsafe-links --exclude=.hg  /media/sjl/3831-6133
    udisksctl unmount -b /dev/sdc1 

(Aside: why don't I always just pipe `histgrep` into `nvim -`?)

Narrowed down my macro troubles to a couple of bugs in MakerLisp itself.  He's
going to take care of them.

## 2019-04-20

Need a random number generator for the MakerLisp machine.  I could FFI out, but
it'll be more fun to write a PCG for it.  This turned out to be a hell of
a rabbit hole.

I've written PCGs before, of course, but on normal computers where I could just
use the bit sizes and multiplier of the reference implementation.  Here I can't
do that, so I had to try to come up with something that would work with 24 bit
integers.  Turns out not many folks have done much LCG research on 24-bit
machines (go figure).  All the test suites (e.g. TestU01 and PractRand)
immediately fail small PRNGs, so it's hard to know if I've got something decent
or not.  Oh well, it's just for games, it's not life and death.

Random notes:

* The "Randograms" in the blog post are confusing because they're sampling the
  entire period of the generator, but still get odd-numbered occurence counts.
  This confused the hell out of me until I realized that by "pair up the
  numbers" they mean a sliding two element window: `(1 2 3 4)` produces `((1 2)
  (2 3) (3 4))`.
* The 256x256 size works perfectly for the 8-bit generators.  I wasn't able to
  extend it for 16-bit generators because exhausting their period would take
  *much* longer.
* It's still not clear to me how to decide what's a "good" multiplier for
  smaller-sized PRNGs.  They fail the tests right away because they're so small,
  so I can't really go by that.

## 2019-04-30

Started playing/rating the lisp jam games.  Wanted to install a VM to safely
play the non-web ones, which led to a big old rabbit hole:

* Need to enable CPU virtualization in the BIOS to get VirtualBox to work.
* When I rebooted my desktop crashed right after logging in.
* Took me a while to find my display manager logs because I can never remember
  its fucking name (and can never remember that it's "display manager" and not
  "desktop manager").  Hey idiot future self: you use XDM.
* Thought the problem was maybe because I just upgraded SBCL and didn't rebuild
  Stump.  Tried that, didn't help.
* Saw some errors in the XDM log about the config file not parsing properly.
  Fixed those.  Didn't help.
* Opened `.xsessionrc` and immediately saw the problem: the `gpg-agent` shit
  I added on my work machine and pulled down here.  Christ.  Removed that for
  now because I can't remember the magic systemd incantation required to get it
  to quit fucking autostarting the agent whenever anything looks in the general
  direction of its ports and I want to move on with my fucking life tonight.

# May 2019

## 2019-05-20

Going to try to reboot this plan.  I know I haven't kept up with it very well
(though my work `.plan` has been going strong every day since October).  Oh
well, no time like the present to restart.

Added a couple of type checks to Adopt.  The only main thing left is to rewrite
the unit tests to work in the new style.  Then it should be ready for Quicklisp,
I think.

Continued learning how to sew.  Hemmed my second pair of pants.  Kind of
a miserable experience, but I'm getting better.  It's weird that the machine
will happily let you forget to put the foot down before letting you sew, happily
fucking up your shit into a giant bird's nest instead of having some kind of
switch you need to press to let yourself fuck it all up.  Oh well, I'll just
learn to not make mistakes I guess.

Finally figured out what all the `/dev/loopNN` bullshit on Ubuntu is.  Seems to
be their app store thing "snap".  I removed some of the garbage "snaps" I never
installed in the first place, but there's still some installed with scary names
like "core" so I guess I'll just have to live with them if I don't want to take
the risk of breaking something.  I did make a little `disks` script to show me
the output I care about using a combination of `lsblk` and `du` and `grep`.
It'll do for now.

New UHK came.  I now own three: one with browns, one with browns plus
stabilizers, and one with blues.  The blues are even clickier than I remember.
I think I still prefer the unsilenced browns though.  They have a nice clunk to
them instead of the clickiness of the blues.  I think I'm finally done buying
keyboards — 2 at home and one at the office is plenty.

Need to figure out how many hard drive bays I've got left in my tower and
motherboard.  I'm running out of room on my Windows partition, and I'm thinking
of using Lightroom on Windows to finally move one more thing away from MacOS.
Sacrilege.  Then DJ'ing for blues and Lindy dances will be the only thing
I still need the Mac for.  I can live with that.

The polydivisibility search I wrote over the weekend is still churning away.
It's searching base 41 now.  Checking base 39 took about 4.6 hours.  Base 40
took around half that.  We'll see how long 41 takes.  Still no results,
unfortunately.  I wonder if I could prove that odd bases never work.  I played
around on the whiteboard but couldn't come up with anything (and if Parker
didn't I almost certainly won't, so I don't feel *too* bad about that).  At
least my cores are getting some use.  It's fun to see all 32 bars full in
`htop` for a change.  Memory usage is pretty constant at about 3-4gb, though it
churns through a lot of garbage thanks to all the bignum arithmetic (~182tb
allocated for base 39).  Is there a way to avoid all the bignum division maybe?

## 2019-05-21

Figured out why my alt key wasn't working.  What a gross rabbit shave:

1. Alt key doesn't seem to be working (e.g. `alt-a` in Zoom doesn't work).
2. Open `xev` and look.  Pressing `alt` shows keycode `133` and keysym `F17`.
3. Open `.xmodmaprc`, which has `keycode 133 = Alt_L` and nothing else listed
   for `133`.
4. Source the file, then run `xmodmap -pke | grep 133` to see if it's working.
5. This gives `keycode 133 = F17 NoSymbol F17`.  But all the *other* mappings in
   the rc file are working, so what the fuck?
6. Eventually I get the idea to look for `F17` instead.  Realize I have a bunch
   of lines like `keycode 900 = F16`, `keycode 901 = F17`, `keycode 902 = F18`,
   etc in the rc file.
7. Tried commenting out the line that maps `F17`, and now everything works.
8. But that was mapping keycode `901`, not `133`.  Why was it overwriting the
   alt mapping?
9. Because `901 ≡ 133 mod 256`.  Fucking kill me.

Pushed my verbose-assertion patch for 1am to Github so I can get to it from
other machines.

Did some work to get Adopt's test suite running again.  Also added duplicate
option detection.  Tests pass in SBCL and CCL.

Tried to install ECL to see if I could run the tests there too.  Problem:
there's no installation link/guide on the ECL page.  Really.  Here's what I did:

    git clone https://gitlab.com/embeddable-common-lisp/ecl.git
    cd ecl
    git checkout ECL-16.1.3
    ./configure --prefix=/usr/local
    make
    sudo make install

Seems to work.  Adopt tests all pass just fine on SBCL, CCL, ECL, and ABCL.

I thought about testing with CLASP, but looking at the installation process it
says it'll take a couple of hours to install.  Maybe once my cores aren't busy
on the polydivisibility checks I'll give it a go, but I don't want to stop it
after many hours and waste all that progress, and I don't know how to make
lparallel interrupt all the threads at once.

Also finally added some docstrings for all the functions in the API.

Anyway, I think Adopt is finally ready (or at least as ready as it's ever gonna
be) for Quicklisp.  I submitted it.  It's a shame I just missed this month's
dist.  Oh well, move slow and make things.

## 2019-05-23

There are no polydivisible numbers in base `41`.  The search continues.

## 2019-05-24

There are no polydivisible numbers in base `42` (what a shame).  Once again,
even bases finish an order of magnitude faster than odd bases, and so far only
even bases work.  I'm going to focus the search on the next couple of even bases
to save time.  I wish I could figure out *why* even bases were more promising.
Or just a better way to search.

# June 2019

## 2019-06-09

Restarted work on Flax.  I want to be able to lay out my l-system nonaptychs
entirely in Lisp, without having to dick around in Inkscape manually.  This
requires two yaks to be shaved:

1. A nice way to say "take this group of drawing objects and translate/scale
   them into this specific bounding box".
2. A way to render text without having to do it manually via Hersheytext.

Implementing 1 was pretty easy.

Implementing 2 is going to require bezier curves, so I went ahead and
implemented those.  I ended up extending the `path` primitive to accept points
with control points attached to draw the nice curves.  This was easy in SVG, but
kind of a pain to do ergonomically in PNG.  I did eventually finish that though.
So now I just need to find/make a font that I can render with those curves.

Ended up just making my own "font" with only the characters I need for the
L-systems (`+-()LR→ `).  Did a bit more and got string rendering working.  Still
probably need to handle multiple lines, but this was a productive day.

# July 2019

## 2019-07-02

My Linux machine has been randomly hanging completely when playing Youtube
videos in Firefox.  I have to hard reboot the machine to get it back.  I have no
idea how to debug this.

Then, today, after one of these reboots the machine wouldn't even get to the
BIOS at all.  Fantastic.  Looking inside at the motherboard's debug screen
showed `C0`.  This code isn't mentioned in the manual at all.  Searching online
showed a bunch of children flailing around in forums, but there was one useful
nugget: resetting the CMOS.  Apparently you're supposed to do this when you
install new RAM, and I did not.  It's worked fine for months, but oh well, may
as well give it a try.  The button on the x399 is just to the left of the debug
screen, and the computer needs to be completely unplugged for it to work.  After
resetting the CMOS the machine took a long time to boot, but did eventually POST
to the BIOS and boot normally.

I think I want to update the BIOS at some point, but for now I'm just happy to
have the machine back and working again.

## 2019-07-09

To get a black new tab page in Firefox, add the following to
`~/.mozilla/firefox/*/chrome/userChrome.css`:

    .browserContainer { background-color: #000000 !important; }

And in `about:config` set `browser.display.background_color` to black.

# August 2019

## 2019-08-27

BitBucket is shitcanning Mercurial support next year, so I have to run on the
Hamster Wheel of Backwards Incompatibility and fix all my repositories and
documentation.

Started by setting up <http://docs.stevelosh.com> to serve the repo that was
formerly served by BitBucket pages.  Added a hook into `.hg/hgrc` on the remote
repo to autoupdate when pushed:

    [hooks]
    changegroup = hg update

Then reconfigured nginx to serve the repo (which is full of plain old HTML files
so it Just Works).  Decided to be lazy and just use `autoindex on` to generate
the index page.  Good enough.

Added `docs.stevelosh.com` to DNS.

I still need to update all my `pubdocs` make targets, and also update all the
links everywhere, but that can wait.  One step at a time.

# December 2019

## 2019-12-23

Enabled HTTPS for `stevelosh.com` and `docs.stevelosh.com` and
`learnvimscriptthehardway.stevelosh.com`.  Used Let's Encrypt which was… okay
I guess.  Hopefully the cron machinery works and I don't have to dick around
with it again in the future.

Spent some time migrating all my Bitbucket repos to Source Hut and updating the
links, so that when Atlassian tells us all to eat shit next year I don't have to
scramble.

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
