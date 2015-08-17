# Session 1: Start Here
---
**This is lifted from the [AtariAge Forum](http://atariage.com/forums/topic/33233-sorted-table-of-contents/),
any content that I add will be bold**
**This page can be found [here](http://atariage.com/forums/topic/27186-session-1-start-here).**

---

## So, you want to program the Atari 2600 and don't know where to start?

Welcome to the first installment of "000001010 00101000 00000000 1100101" - which at first glance
is a rather odd name for a programming tutorial - but on closer examination is appropriate, as it is
closely involved with what it's like to program the Atari 2600. The string of 0's and 1's is actually
a binary representation of "2600 101".

I'm Andrew Davie, and I've been devloping games for various computers and consoles since the late 1970s.
Really! What I plan to do with this tutorial is introduce you to the arcane world of programming the '2600,
and slowly build up your skill base so that you can start to develop your own games. We'll take this in
slow easy stages, and I encourage you to ask questions - this will help me pace the tutorial and introduce
subjects of interest.

Developing for the Atari 2600 is much simpler today than it was when the machine was a force in the
marketplace (ie: in the 1980s). We have a helpful online community of dedicated programmers, readily
available documentation, tools, and sample code - and online forums where we can pose questions and get
almost instant feedback and answers. So don't be scared - with a bit of effort, anyone can do this!

It is this online community which makes developing for the machine 'fun' - though I use that in the
broadest sense of the word. My 'fun' may be another man's 'torture'. For, programming this machine is
tricky, at best - and not for the feint of heart. But the rewards are great - making this simple hardware
do anything at all is quite an achievement - and making it do something new and interesting gives one a
warm fuzzy feeling inside.

So, let's get right into it... here's your first installment of "2600 101". We're going to assume that
you know how to program *something*, but not much more than that. We'll walk through binary arithmetic,
hexadecimal, machine architecture, assemblers, graphics, and whatever else gets in our way. And we'll
probably divert on tangential issues here and there. But hopefully we'll come out of it with a greater
understanding of this little machine, and appreciation for the work of those brilliant programmers who
have developed the classics for this system.

## The Basics:

A game on the '2600 comes in the form of a cartridge (or "tape") which is plugged into the console itself.
This cartridge consists of a circuit board containing a ROM (or EPROM) which is basically just a silicon
chip containing a program and graphics for displaying the game on your TV set. This program (and graphics)
are really just a lot of numbers stored on the ROM which are interpreted by the CPU (the processor) inside
your '2600 just like a program on any other computer. What makes the '2600 special is... nothing. It's a
computer, just like any other!

A computer typically consists of a CPU, memory, and some input/output (I/O) systems. The '2600 has a CPU
(a 6507), memory (RAM for the program's calculations, ROM to hold the program and graphics), and I/O systems
(joystick and paddles for input, and output to your TV).

## The CPU

The CPU of the '2600 is a variant of a processor used in computers such as the Apple II, the Nintendo NES,
the Super Nintendo, and Atari home computers (and others). It's used in all these machines because it is
cheap to manufacture, it's simple to program, but also effective - the famous "6502". In this course we will
learn how to program the 6502 microprosessor... but don't panic, we'll take that in easy stages (and besides,
it's not as hard as it looks).

The '2600 actually uses a 6507 microprocessor - but this is really just a 6502 dressed in sheep's clothing.
The 6507 is able to address less memory than the 6502 but is in all other respects the same. I refer to the
'2600 CPU as a 6502 purely as a matter of convenience.


## Memory

Memory is severely restricted on the '2600. When the machine was developed, memory (both ROM and RAM) were
very expensive, so we don't have much of either. In fact, there's only **128 BYTES of RAM**
(and we can't even use all of that!) - and typically (depending on the capabilities of the cartridge
we're going to be using for our final game) only about **4K of ROM**. So, then, here's our first
introduction to the 'limitations' of the machine. We may all have great ideas for '2600 games, but we
must keep in mind the limited amount of RAM and ROM!

## Input/Output

Input to the '2600 is through interaction by the users with joystick and paddle controllers, and various
switches and buttons on the console itself. There are also additonal control devices such as keypads -
but we won't delve much into those. Output is invariably through a television picture (with sound) -
i.e.: the game that we see on our TV.


So, there's not really much to it so far - we have a microprocessor running a program from ROM, using RAM,
as required, for the storage of data - and the ouptut of our program being displayed on a TV set. What
could be simpler?


## The Development Process

Developing a game for the '2600 is an iterative process involving editing source code, assembling the code,
and testing the resulting binary (usually with an emulator). Our first step is to gather together the
tools necessary to perform these tasks.

'Source code' is simply one or more text files (created by the programmer and/or tools) containing a list
of instructions (and 'encoded' graphics) which make up a game. These data are converted by the assembler
into a binary which is the actual data placed on a ROM in a cartridge, and is run by the '2600 itself.

To edit your source code, you need a text-editor -- and here the choice is entirely up to you. I use
Microsoft Developer Studio myself, as I like its features - but any text editor is fine. Packages
integrating the development process (edit/assemble/test) into your text editor are available, and this
integration makes the process much quicker and easier (for example, Developer-Studio integration allows
a double-click on an error line reported by the assembler, and the editor will position you on the very
line in the source code causing the error).

To convert your source code into a binary form, we use an 'assembler'. An assembler is a program which
converts assembly language into binary format (and in particular, since the '2600 uses a 6502-variant
processor, we need an assembler that knows how to convert 6502 assembly code into binary). Pretty much
all '2600 development these days is done using the excellent cross-platform (ie: versions are available
for multiple machines such as Mac, Linux, Windows, etc) assembler 'DASM' which was written by Matt Dillon
in about 1988.

DASM is now supported by yours-truly, and is available at "http://www.atari2600.org/dasm" **(DASM is
no longer hosted by AtariAge, you can download at SourceForge
[here](http://sourceforge.net/projects/dasm-dillon/) I also have a copy in this repo,)** - it would
be a good idea now to go there and get a copy of DASM, and the associated support-files for
'2600 development. In this course, we will be using DASM exclusively. We'll learn how to setup and
use DASM shortly.

Development of a game in the '80s consisted of creating a binary image (ie: write source code,
assemble into binary) and then physically 'burning' the binary onto an EPROM, putting that EPROM
onto a cartridge and plugging it into a '2600. This was an inherently slow process (trust me, I
did this for NES development!) and it sometimes took 15 minutes just to see a change!

Nowdays, we are able to see changes to code almost immediately because of the availablility of good
emulators. An emulator is a program which pretends to be another machine/program. For example, a
'2600 emulator is able to 'run' binary ROM images and display the results just as if you'd actually
plugged a cartridge containing a ROM with that binary into an actual '2600 console. Today's '2600
emulators are very good indeed.

So, instead of actually burning a ROM, we're just going to pretend we've burned one - and look at
the results by running this pretend-ROM on an emulator. And if there's a problem, we go back and
edit our source code, assemble it to a binary, and run the binary on the emulator again. That's our
iterative development process in action.

There are quite a few '2600 emulators available, but two of note are

Z26 - available at [http://www.whimsey.com/z26/](http://www.whimsey.com/z26/)  
Stella - available at [http://stella.sourceforge.net/](http://stella.sourceforge.net/)  
**I use Stella on my Mac**

Stella is your best choice if you're programming on non-Windows platform. I use Z26 for Windows
development, as it is quite fast and appears to be very accruate. Either of these emulators is fine,
and it's handy to be able to cross-check results on either.

We'll learn how to use these emulators later - but right now let's continue with the gathering of
things we need...

Now that we have an editor, an assembler, and an emulator - the next important things are documentation
and sources for information. There are many places on the 'net where you can find information for
programming '2600, but perhaps the most important are

the Stella list - at http://www.biglist.com/lists/stella/
AtariAge - at http://www.atariage.com/

and finally, documetation. A copy of the technical specifications of the '2600 hardware (the Stella Programmer's Guide) is essential...

Stella Programmer's Guide
- text version at [http://stella.sourceforge.net/docs/index.html](http://stella.sourceforge.net/docs/index.html)
- (old) PDF version at [http://www.atarihq.com/danb/files/stella.pdf](http://www.atarihq.com/danb/files/stella.pdf)
- **I've put a copy of the old pdf guide in this repo [here](/docs/stella_guide.pdf)**


OK, that's all we need. Here's a summary of what you should have...

- Text editor of your choice.
- DASM assembler and '2600 support files.
- Emulator (Z26 or Stella)
- Stella Programmer's Guide
- bookmarks to AtariAge and the Stella mailing list.


That's it for this session. Have a read of the Stella Programmer's Guide (don't worry about
understanding it yet), and try installing your emulator (and play a few games for 'research' purposes).
Next time we will make sure that our development environment is setup correctly, and start to discuss
the principles of programming a '2600 game.

PS: I can't promise to complete this 'course' - but hopefully what I do write will be interesting and helpful. 

---
Now you can head to [Lesson 2: Television Display Basics](/docs/atariage/tvbasics.md)
