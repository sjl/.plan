[TOC]

# January 2018

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
