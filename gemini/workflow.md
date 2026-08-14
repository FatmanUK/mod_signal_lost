# `.mod` Creation Workflow

The Cold Boot workflow wasn't perfect, but it's yielded a great result. So here it is (the workflow). This was ChatGPT over several months (resource limits being what they are).

## Prompts

These are my prompts with brief explanations and summarised replies. I've also added excellent snippets of actual reply. LLMs tend to extremely long-winded replies.

---

Goal: Determine capabilities of LLM.

> Can you compose mod tunes?

I start with this. (It's becoming a tradition.) The answer is 'yes'.

---

Goal: Specify the task and establish the following:
  - Tempo
  - Mood
  - Influences
  - Structure
  - Authentic 4-channel ProTracker
  - Seamless loop or not?
  - 9 to 12 unique patterns
  - Heavy pattern reuse
  - High-level instrument map

> I want a suspenseful thumping two-minute looping load-screen tune in the style of Ray Norish or Alistair Brimble. It should be a four-channel ProTracker mod. Please generate source which I can convert into a playable MOD file myself.

Alter requirements and influences, obviously. Make it as descriptive as you like. I later realised precise time length is an irrelevant criterion and relaxed that constraint.

> Suggested samples
> | # | Purpose                     |
> | - | --------------------------- |
> | 1 | Deep synthetic kick/thump   |
> | 2 | Snare with short gated tail |
> | 3 | Closed hat                  |
> | 4 | Warm analog bass            |
> | 5 | Dark PWM synth pad          |
> | 6 | Bell/pluck lead             |
> | 7 | Noise sweep FX              |
> | 8 | Reverse cymbal              |

Both ChatGPT and Gemini independently recommended this exact instrument selection (with a few minor word variations). I wonder why, and will Claude do the same?

...

> The good news is that tracker music naturally reuses patterns. For a suspenseful loading tune in the Brimble/Norish vein, I'd intentionally lean into that. A plausible layout could look like this:
> 
> Pattern	Purpose
> 00	Intro pulse
> 01	Main groove A
> 02	Main groove B
> 03	Variation A
> 04	Build
> 05	Tension
> 06	Breakdown
> 07	Climax
> 08	Outro/loop transition

It's come up with a fairly standard pattern progression, but just wait. There's more to this.

---

Goal: Establish additional requirements:
  - Stay within genuine ProTracker constraints:
    - 4 channels only
    - No XM features
    - No more than 31 instruments
    - Effects compatible with original Amiga ProTracker
    - Realistic note ranges
    - Pattern reuse to conserve memory

> Let's go with that.

Agree to the bot's proposal. It put out more blather which happened to include the PT constraints. Maybe actively specify to conform with PT constraints.

---

Goal: Tell it what tools we're using.

> I'm using PikaOS, which is derived from Debian. I'm using MilkyTracker for input and testing.

I'm actually using ptgen for input, but I don't feel like explaining that to the bot.

---

Goal: Establish additional requirements:
  - Write patterns exactly as they appear in the tracker
  - Explain each effect the first time it appears
  - The end result could plausibly have appeared in the early 1990s

> Build the module incrementally over multiple responses. Begin with the instrument layout, then Pattern 00 onward. Explain any ProTracker effects the first time they appear. Compose as though it could have shipped on an Amiga around 1992. Favour atmosphere, tension, rhythmic pulse, and economical pattern reuse over flashy melodies, keeping the music suitable for a suspenseful game loading screen.

If it doesn't suggest these things itself.

---

Goal: Name that tune.

> Suggest some song names.

Every song needs a name. This sets a thematic 'seed'.

> Tracker musicians often named a tune very early, and the name subtly shaped its character. A loading tune called Shadow Circuit ends up feeling different from one called Cold Boot or Countdown, even if they're all suspenseful.
> 
> A few titles that fit the atmosphere we're aiming for:
> 
> Cold Boot
> Vector Lock
> Dark Loader
> Silent Sector
> Black Ice
> Awaiting Clearance
> Deadlock
> Zero Hour
> Signal Lost
> Terminal Phase
> 
> It doesn't have to be the final title, but I find having one helps keep the musical direction consistent. It gives the piece a little identity before the first pattern is even entered.

This last paragraph is prescient. The bot truly means it.

---

Goal: Plant a thematic 'seed'.

> I like Cold Boot.

Seemed like the best of the bunch.

> I like Cold Boot too. It immediately evokes a machine waking up into something slightly unsettling. It also fits the era. A lot of Amiga module names were short, evocative, and technical without being overly descriptive.
> ...
> Mood: The computer has powered on, but something isn't quite right. Not horror, not action, just a steadily growing sense of anticipation.
> 
> Musical character:
>   - A persistent, heartbeat-like kick that never lets go.
>   - Sparse bass that locks into the kick rather than wandering.
>   - A dark looping pad providing harmonic tension.
>   - A metallic bell motif that appears occasionally, almost like a diagnostic beep.
>   - A gradual build in density without ever becoming "epic."
> 
> The harmonic language will lean on minor keys with a touch of modal ambiguity. I'm thinking of using intervals like minor seconds and tritones sparingly, because they're very effective in tracker music without becoming melodramatic.
> 
> I'd also like to borrow a trick common in Amiga loading tunes: make the loop almost impossible to notice. Instead of ending with a flourish, the final pattern will quietly dissolve back into the opening pulse. If you let it play for ten minutes, it should feel like one continuous piece.

Where is all this coming from? How is a glorified spellchecker doing all this? It's witchcraft I tells ya!

---

Goal: Decide on samples.

> I'll use samples from the ST-XX archives.

I want small but decent samples. I've tried generating them but only ended up with roasted garbage.

> For Cold Boot, I’d use ST-01 only as the initial palette. It is small, historically appropriate, and the sample names are documented directly in the Aminet listing. The entire ST-01 archive has 126 files and unpacks to about 755 kB, which is still tiny by modern standards.
> ...
> Cold Boot - ST-01 sample map
> 
> 01  BassDrum1     kick / low thump
> 02  Snare4        tight electronic snare
> 03  CloseHiHat    short closed hat
> 04  PopBass       main bass
> 05  KorgString    dark pad / suspense bed
> 06  ExBells       metallic diagnostic chime
> 07  Stabs         synth accent
> 08  Sweep         transition / noise tension

Without prompting, it's gone ahead and selected samples from ST-01. Fine by me!

---

Goal: Let the bot take control now it knows what to do.

> Ok, I've written all that down. What's next?

We test the chosen samples next.

> Next: create the empty Cold Boot module, import the ST-01 samples into fixed slots, and make a tiny test pattern so we know the samples are mapped correctly before I give you the actual tune data.
> ...
> When you play it, you should hear:
> 
> Ch1: kick thumps
> Ch2: bass alternates C and G
> Ch3: string/pad sustains
> Ch4: bell, stab, and sweep samples appear one by one
> 
> You are checking four things:
> 
> 1. Does each sample slot trigger the right sound?
> 2. Is any sample absurdly loud or quiet?
> 3. Does PopBass make a usable bass note around C-2/G-2?
> 4. Does KorgString sustain or loop cleanly enough for a pad?

Give responses to all criteria, or it'll sulk quietly.

---

Goal: Enforce PT constraints.

> Wait: remember PT doesn't allow notes below octave 3 or above octave 5.  Also, that order list is boring. Mix it up a little bit.

Oopsie! I had to remind it of the PT constraints.

> For the order list, agreed: 00 01 02 03 04 05 06 07 08 is too much like a filing cabinet learning to dance. We’ll use a more tracker-authentic reuse structure.

Did it just crack a joke?

---

Goal: Test sample selection and grow thematic seed into pattern00.

> Ok, I'll download the samples, prepare the mod file, and run the test pattern in MT to see how it sounds. When I come back, I'll either say "Ready" to confirm everything is fine and I'm ready to proceed to the next step, or I'll relate any issues discovered which need to be fixed.

It was all good, so I said:

> Ready.

It gave me pattern00. At this point I realised I'd forgotten about sample loops.

---

Goal: Establish sample loop settings.

> I forgot to ask if any of the samples should be looped? And if so, which ones and which type of loop?

> Looping:
> 
> * Loop only PopBass and KorgString
> * Use forward loops only
> * All other samples remain one-shot
> 
> Important rules:
> 
> * Keep all notes within the ProTracker-safe range C-3 to B-5.
> * Stay compatible with MilkyTracker and ProTracker-style MOD behavior.
> * Make the tune feel like a tense machine waking up: pulse, bass, pad, chimes, buildup, seamless loop.

---

Goal: Save progress.

> Summarize our progress into a single 'Bootstrap Markdown Manifest'. Include:
> 1. **Current Goal:** The immediate objective.
> 2. **State of Play:** Where we are, including key logic, architectures, or decisions made.
> 3. **Dependency Map:** What libraries/versions are in use, if any.
> 4. **Open Issues:** Known bugs or blockers.
> 5. **"Golden" Code Blocks:** The most current versions of essential files or core logic blocks. Don't include previous failed attempts. 
> 6. **Testing State:** Confirmation that the current code passes testing.
> 7. **Next Steps:** A bulleted list of the exact next 3 actions I should take.

This is a good time for a snapshot.

---

Now we just enter a loop of creating and auditioning patterns. And that's it.
