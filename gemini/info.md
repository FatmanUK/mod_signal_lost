# Design Lessons

## Story

Before composing any patterns, have the bot write a simple one-line story outline matching each pattern, based on the song title. I know that sounds crazy, but it provides a seed for thematic structure. ChatGPT did this for Cold Boot without being asked, and as a result the mod sounds thematically consistent, unlike Signal Lost which sounds completely unconnected.

## Channel Characterisation

We might characterise the channels as:

1. Bass Engine
2. Percussion Engine
3. Atmosphere and Lead
4. Rhythm and Effects

Why this layout? Well...

### "Hard Left" and "Hard Right"

On standard modern audio gear, you can "pan" a sound anywhere between left and right (e.g., 20% left, center, 70% right).

The original A500/1200 hardware did not have panning controls. Its audio outputs were hard-wired directly to the physical stereo RCA jacks on the back of the computer.

Left RCA Output (Hard Left): Channels 1 and 4.

Right RCA Output (Hard Right): Channels 2 and 3.

Because there was no middle ground, Channel 1 and 4 are 100% in your left ear, and Channel 2 and 3 are 100% in your right ear!  That's why tracker coders had to be strategic: if you put the Kick drum on Channel 4 (Left), you had to put the Snare on Channel 2 (Right) so the drum kit felt balanced across both ears instead of lopsided.

## Finetune

Here is the easiest way to understand finetune: think of it like tuning a guitar string.

When the creators of the ST-01 and ST-02 disks made these samples in the late 1980s, they literally just plugged a synthesizer (like a Roland D-50 or Minimoog) into the Amiga and hit "Record."

Because they were recording raw audio from analog gear, the pitch wasn't always perfectly calibrated to standard digital tuning.

    If you tell ProTracker to play a C-3 note using the DigDug sample, it might naturally sound like a slightly sharp C.

    If you play a C-3 note using PolySynth, it might sound like a slightly flat C.

If you play them together, they will clash and sound terribly out of tune, even though you typed the exact same note (C-3) into your pattern!

### What Finetune Does

Finetune is a setting in the instrument header that lets you subtly nudge the pitch of a sample up or down by a fraction of a semitone.

It fixes the recording errors. You are essentially telling the tracker: "Whenever I play a note with this sample, automatically twist the tuning peg down just a tiny bit so it actually hits a perfect C."

### How it Works in ProTracker

In standard Amiga trackers, Finetune is measured on a scale from -8 to +7.

- 0 means no change (plays the raw recording as-is).
- +1 to +7 nudges the sample slightly sharper (higher).
- -1 to -8 nudges the sample slightly flatter (lower).

(Note: In the tracker's hexadecimal interface, these values are often displayed as 0 to F, where 8 to F represent the negative numbers).

### The "Anchor" Method for Mixing

You only need to finetune melodic instruments (Bass, Pad, Lead). Drums and noise sweeps (BassDrum1, Snare1, swoop) don't have a strict musical key, so their finetune is just left at 0.

To get DigDug, Heaven, and PolySynth playing nicely together, you don't need absolute perfect pitch—they just need to be in tune with each other. Here is how tracker musicians do it:

1. Pick an Anchor: Choose your Bass (DigDug) as the master tuning reference. Leave its Finetune at 0.
2. Play a Drone: Go to a blank pattern, put a continuous C-3 note on Channel 1 using DigDug. Let it loop over and over.
3. Tune the Pad: Put a continuous C-3 note on Channel 2 using Heaven. Listen to them together. If it sounds "wobbly" or dissonant, adjust the Finetune on Heaven up or down one notch at a time until the wobble disappears and they sound locked together.
4. Tune the Lead: Repeat the process for PolySynth.
