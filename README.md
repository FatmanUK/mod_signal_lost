# mod_signal_lost
Repeated my Cold Boot experiment, but this time with Gemini instead of ChatGPT.

The name was prophetic. The project lost cohesion at one point, but I hauled it back from the brink of complete dissolution by selecting a new roster of instruments and reminding Gemini about the patterns it had already written. (Context window corrupted?)

Then I decided patterns 00 and 08 sucked very hard, so I ditched them and asked Gemini for two new patterns. For some reason best known to itself, it gave me four. I added them all.

## result
Compared to ChatGPT and Claude's efforts, I had to intervene a lot. Gemini is definitely the least usable and most annoying of the three LLMs. I don't have a paid account for Gemini, so it's possible this puts it at a disadvantage against the other two LLMs. Maybe I'm not seeing the best Gemini has to offer.

The annoyance factor of Gemini can be dialled way down if you give it instructions to change its interaction style, such as "ask for missing data; don't guess it" or "give only precise and accurate answers" or "don't suggest next steps", or whatever else you find irritating.

Considering what this `.mod` went through, I think it sounds great. It would work fine as a loading-screen tune, which after all was the brief. I might still replace the `DigDug` sample.

The next step is to repeat the experiment with a smaller model (ie. a stupider LLM thinking-brain), see what it can produce when it's not constantly juiced.

## build notes
To get the ST-01 and ST-02 archives on Debian-based Linux, issue these commands:
   
    ❯ sudo apt update
    ❯ sudo apt install lhasa wget
    ❯ install -d mod_cold_boot/stxx
    ❯ cd mod_cold_boot/stxx
    ❯ wget -O st-01.lha https://aminet.net/mods/inst/st-01.lha
    ❯ lha x st-01.lha
    ❯ wget -O st-01.lha https://aminet.net/mods/inst/st-02.lha
    ❯ lha x st-02.lha

These samples are in IFF format and AmigaOS doesn't use file extensions, so to make MilkyTracker see them you have to rename the ones you want with '.iff' extensions. Like this:
   
    ❯ mv Stabs Stabs.iff
