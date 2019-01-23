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

