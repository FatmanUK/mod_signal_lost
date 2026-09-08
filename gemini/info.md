# Design Lessons

## Choice of AI Models

Which model is required for the work of composing `.mod` tunes?

I was able to debug a horrible spec bug using Claude Sonnet 5 (Medium) which Gemini Pro couldn't figure out. Sonnet 5 is impressive. It might be able to compose.

Here's Gemini's opinion:

> For tracking musical notation and hexadecimal effects tables, **Gemini Pro with the "Extended" thinking level enabled** is going to be your absolute best tool.
> 
> Here is why:
> 
> * **Why Pro (over Flash or Flash-Lite):** Pro models are built for deep reasoning, structural logic, and strict formatting. Composing tracker modules requires aligning text characters perfectly into rigid vertical columns (Note | Instrument | Volume | Effect). Pro handles this spatial formatting vastly better than the faster, lighter models, which are prone to drifting or getting column alignments wrong.
> * **Why the "Extended" thinking level (over Standard):** Standard thinking is great for fast text generation or quick answers. However, translating a musical idea into abstract hexadecimal command codes (like calculating pitch slides, arpeggios, or sample offsets) is highly analytical. Giving the model the extra time to use "Extended" thinking allows it to double-check its math and pattern length before it outputs the code block, ensuring your tracker patterns actually make musical sense when you play them back.

Also, Flash-Lite is as stupid as mud. It's not even reliable to summarise its own conversations. It's great for quick opinions, but not accurate writing. Non-Lite Flash is good for summaries.

## Git

The entire `.mod` can be represented as text, so a Git repository is a perfect match for version control.

> I approve of that blend of eras. 😄
> 
> You're essentially giving a 1992 workflow a 2026 safety net.

## Samples Before Patterns

Define your sample roster first. Then write patterns for them. I got this wrong with Signal Lost and sacrificed greatness.

## Quality Pass

(Optional, from branch):
Check:

- four-channel voice leading,
- note stealing,
- impossible overlaps,
- pattern transitions,
- seamless loop,
- whether it actually sounds like Cold Boot rather than just "generic Amiga."

That quality pass is likely to catch little issues that would otherwise have you editing patterns later.

(From the branch. I don't know what any of these mean. I suspect it's not needed.)

## Composer's Pass

Don't do this before version 1 is finalised. Best not use the bot for this.

## Useful Prompts

### Too Eager with the Bootstrap Files

`Don't show me a bootstrap file until I ask for it, please.`

### Scold Bot for Coyness

After many attempts at a simple task and finally admitting it was missing some vital data (which I immediately uploaded):

`When this kind of issue occurs you need to be completely honest and say so up front. Then I can fix it. If you keep it secret I can't.`

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

The cheat's way to sort out finetune is to look up historically used values, if using well-known samples such as those from ST-01 and ST-02.

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

## Notes

Deep bass instruments should probably not be used in octave 3 as they're likely too low. The converse is probably true of high instruments.

Of course, the bot doesn't have ears and can't tell what sounds good. This suggests that we should limit octave ranges per instrument before composing.

Also, loopability should be established first. If a sample proves unloopable, it should be known before composition begins.
