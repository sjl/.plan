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
