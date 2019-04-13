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
