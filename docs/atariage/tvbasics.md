# Session 2: Television Display Basics
---
The original page can be found [here](http://atariage.com/forums/topic/27187-session-2-television-display-basics)

---

Hopefully you've been through the first part and have your editor, assembler, emulator and documentation
ready to go. What we're going to look at now is a basic overview of how a television works, and why this is
absolutely necessary pre-requisite knowledge for the '2600 programmer. We're not going to cover a lot of
'2600 specific stuff this time, but this is most defintely stuff you NEED TO KNOW!

Television has been around longer than you probably realise. Early mechanical television pictures were
successfully broadcast in the '20s and '30s (yes, really! - see http://www.tvdawn.com/index.htm).
The mechanical 'scanning' technology utilised in these early television systems are no doubt the
predecessors to the 'scanning' employed in our modern televisions.

A television doesn't display a continuous moving image. In fact, television displays static
(non-moving) images in rapid succession - changing between images so quickly that the human eye
percieves any movement as continuous. And even those static images aren't what they seem - they are
really composed of lots of separate lines, each drawn one after the other by your TV, in rapid succession.
So quick, in fact, that hundreds of them are drawn every image, and many images are drawn every second.
In fact, the actual numbers are very important, so we'll have a look at those right now.

The Atari 2600 console was released in many different countries around the world. Not all of these
countries use the same television "system" - in fact there are three variations of TV systems (and there
are three totally different variations of Atari 2600 hardware to support these systems). These systems are
called NTSC, PAL, and SECAM. NTSC is used for the USA and Japan, PAL for many European countries, and
Australia, and SECAM is used in France, some ex-French colonies (e.g.: Vietnam), and Russia. SECAM is
very similar to PAL (625/50Hz), but I won't spend much time talking about it, as Atari SECAM units are
incredibly rare, and little if any development is done for that format anyway. Interestingly, the differences
in requirements for displaying a valid TV image for these systems leads to the incompatibility between
cartridges made for NTSC, PAL and SECAM Atari units. We'll understand why, shortly!

A television signal contains either 60 images per second (on NTSC systems) or 50 images per second
(on PAL systems). This is closely tied to the frequency of mains AC power in the countries which use
these systems - and this is probably for historical reasons. In any case, it's important to understand
that there are differences. Furthermore, NTSC images are 525 scanlines deep, and PAL images are 625
scanlines deep. From this, it follows that PAL images have more detail - but are displayed less frequently
- or alternatively, NTSC images have less detail but are displayed more often. In practise, TV looks
pretty much the same in both systems.

But from the '2600 point of view, the difference in frequency (50Hz vs. 60Hz) and resolution
(625 scanlines vs. 525 scanlines) is important - very important - because it is the PROGRAMMER who has
to control the data going to the TV. It is not done by the '2600 (!!) - the '2600 only generates a
signal for a single scanline.

This is completely at odds with how all other consoles work, and what makes programming the '2600 so
much *'fun'*. Not only does the programmer have to worry about game mechanics - but she also has to
worry about what the TV is doing (ie: what scanline it is drawing, and when it needs to start a new
image, etc., etc).

Let's have a look at how a single image is drawn by a TV...

A television is a pretty amazing piece of 1930's technology. It forms the images we see by shining an
electron beam (or 3, for colour TVs) onto a phosphour coating on the front of the picture tube. When
the beam strikes the phosphour, the phosphour starts to glow - and that glow slowly decreases in brightness
until the phosphour is next hit by the electron beam. The TV 'sweeps' the electron beam across the
screen to form 'scanlines' - at the same time as it sweeps, adjusting the intensity of the beam, so
the phosphour it strikes glow brighly or dimly. When the beam gets to the end of a scanline, it is
turned off, and the deflection circuitry (which controls the beam) is adjusted so that the beam will
next start a little bit down, and at the start (far left-hand-side) of the next scanline. And it will
then turn on, and sweep left-to-right to draw the next scanline. When the last scanline is drawn, the
electron beam is turned off, and the deflection circuityr is reset so that the beam's position will next
be at the top left of the TV screen - ready to draw the first scanline of the next frame.

This 'turning-off' and repositioning process - at the end of a scanline, and at the end of an image -
is not instantaneous - it takes a certain amount of time for the electronics to do this repositioning,
and we'll understand this when we come to talk about the horizontal blank (when the beam is resetting
to the left of the next scanline) and the vertical blank (when the beam is resetting to the top left
scanline on the screen). I'll leave that for a later session, but when we do come to it, you'll
understand what the TV is doing at these points.

A fairly complex - but nonetheless simple-to-understand analog signal controls the sweeping of the
electron beam across the face of the TV. First it tells the TV to do the repositioning to the start of
the top left line of the screen, then it includes colour and intensity information for the electron beam
as it sweeps across that line, then it tells the TV to reposition to the start of the next scanline,
etc., right down to the last scanline on the screen. Then it starts again with another reposition to
the start... That's pretty much all we need to know about how that works.

The Atari 2600 sends the TV the "colour and intensity information for the electron beam as it sweeps
across that line", and a signal for the start of each new line. The '2600 programmer needs to feed the
TV the the signal to start the image frame.

A little side-track, here. Although I stated that the vertical resolution of a TV image is 625 lines
(PAL) and 525 lines (NTSC), television employs another 'trick' called interlacing. Interlacing involves
building up an image out of two separate 'frames' - each frame being either the odd scanlines, or the
even scanlines of that image. Each frame is displayed every 1/30th of a second (ie: at 30HZ) for NTSC,
or every 1/25th of a second (25Hz) for PAL. By offsetting the vertical position of the start of the first
scanline by half a scanline, and due to the persistance of the phosphour coating on the TV, the eye/brain
combines these frames displaying alternate lines into a single image of greater vertical resolution
than each frame. It's tricky and messy, but a glorious 'hack' solution to the problem of lack of bandwidth in a TV signal.

The upshot of this is that a single FRAME of a TV image is actually only half of the vertical resolution
of the image. Thus, a NTSC frame is 525/2 = 262.5 lines deep, and a PAL frame is 625/2 = 312.5 lines deep.
The extra .5 of a line is used to indicate to the TV if a frame is the first (even lines) or second
(odd lines) of an image. An aside: about a year ago, the #stella community discussed this very aspect
of TV images, and if it would be possible for the Atari to exploit this to generate a fully interlaced
TV frame - and, in fact, it is possible. So some 25 years after the machine was first released, some
clever programmers discovered how to double the resolution of the graphics.

Back to basics, though. We just worked out that a single frame on a TV is 262.5 (NTSC) and 312.5
(PAL) lines deep. And that that extra .5 scanline was used to tell the TV if the frame was odd or even.
So the actual depth of a single frame is 262 (NTSC) and 312 (PAL) lines. Now, if TV's aren't told that a
frame is odd, they don't offset the first scanline by half a scanline's depth - and so, scanlines on
successive frames are exactly aligned. We have a non-interlaced image, displayed at 60Hz (NTSC) or
50Hz (PAL). And this is the 'standard' format of an Atari 2600 frame sent to a TV.

In summary, an Atari 2600 frame consists of 262 scanlines (NTSC) or 312 scanlines (PAL), sent at 60Hz
(NTSC) or 50Hz (PAL) frequency. It is the job of the '2600 programmer to make sure that the correct number
of scanlines are sent to the TV at the right time, with the right graphics data, and appropriate control
signals to indicate the end of the frame are also included.

One other aspect of the difference between TV standards - and a consequence of the incremental development
of television technology (first we had black and white, then colour was added - but our black and white
TVs could still display a colour TV signal - in black and white) - is that colour information is encoded
in different places in the signal for NTSC and PAL (and SECAM) systems. So, even though the programmer is
fully-responsible for controlling the number of scanlines per frame, and the frequency at which frames
are generated, it is the Atari itself which encodes the colour information into the TV signal.

This is the fundamental reason why there are NTSC, PAL, and SECAM Atari systems - the encoding of the
colour information for the TV signal! We get some interesting combinations of Atari and games, for example...

If we plug a NTSC cartridge into a PAL '2600, then we know that the NTSC game is generating frames
which are 262 lines deep, at 60Hz. But a PAL TV expects frames 312 lines deep, at 50Hz. So the image is
only 262/312 of the correct depth, and also images are arriving 60/50 times faster than expected. If we
were viewing on a NTSC TV, then the PAL console would be placing the colour information for the TV signal
in a completely different place than the TV is expecting - so we would see our game in black and white.

There are several combinations you can play with - but the essence is that if you use a different '2600
variant than TV, you will only get black and white (eg: NTSC '2600 with PAL TV or PAL '2600 with NTSC TV)
as the colour information is not in at the correct frequency band of the signal. And if you plug in a
different cartridge than TV (eg: NTSC cart with PAL TV or vice-versa) then what you see depends on the
television's capability to synchronise with the signal being generated - as it is not only the incorrect
frequency, but also the incorrect number of scanlines.


All of this may sound complicated - but really all we need to do is create a 'kernal' (which is the name
for your section of an Atari 2600 program which generates the TV frame) which does the drawing correctly -
and once that's working, we don't really need to worry too much about the TV - we can abstract that out and
just think about what we want to draw.

Well, I lie, but don't want to scare you off TOO early ;)

Next time, let's have a look how the processor interacts with hardware, I/O and memory.

---
And next: [Session 3: The TIA and the 6502](/docs/atariage/tia6502.md)
